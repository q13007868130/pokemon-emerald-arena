# Emerald Arena 简体中文汉化工作区

本分支 `l10n/zh-CN` 基于上游 `GBurgardt/pokemon-emerald-arena` 的 `main` 创建。原作者实时战斗代码保持原样，汉化代码与资料先全部放在 `localization/` 目录。

## 当前状态

- ✅ 建立独立汉化分支，不修改 fork 的 `main`。
- ✅ 从 `q13007868130/git-demo` 的 `meowth-gba-custom-api-gui` 分支复制之前改过的 Meowth 自定义 API GUI 文件（位于 `localization/tools/Meowth-GBA-Custom-API/`）。
- ✅ 已确认不能直接将传统绿宝石中文字体二进制补丁应用到 Emerald Arena 0.13.0；它会写入本作已有数据的 ROM 区域。
- ⏳ 适配源码层中文字形绘制、宽度与字符编码；尚未完成。
- ⏳ 导入已翻译的文本；本次 Git 提交没有包含历史 `texts_translated.json` 文件，需单独导入、校验。
- ❌ 暂无可正常战斗的中文 ROM；移植的 Meowth GUI 也没有完成真实 API / Windows 端到端测试。

## 最重要的原则

1. **从源码入手**：参考根目录 `BUILD.md`，使用锁定版本的 `pret/pokeemerald` 和本项目的 `game/native-engine.patch` + `game/overlay` 构建；不要直接往发行版 ROM 写入通用字库补丁。
2. **先单字符、后全量文本**：先测试 ASCII + 一个中文字符能正常显示，且实时战斗/经典战斗/存档均不受影响，再批量添加文字。
3. **禁止在公开仓库提交** `*.gba`、存档、API Key 或未经允许的密钥；上游 `.gitignore` 已排除 ROM。
4. **每次功能变更都可回退**：使用小提交；不强制合并到 `main`；跟进上游更新时先检查补丁冲突。
5. **保留旧成果**：不删除 `git-demo` 原分支，Meowth 补丁按原样迁移并注明来源。

## 目录

- `tools/Meowth-GBA-Custom-API/`：历史 Meowth GUI 自定义 API 补丁（**不是** Emerald Arena 引擎的一部分）。应在独立的 Meowth 上游源码环境中安装。
- `FONT_COMPATIBILITY.md`：中文字库导致白屏的已知风险与修复策略。
- `translations/`：将来存放人工审核、适合源码导入的简体中文翻译数据；不要直接写入 ROM 的绝对偏移。

## 来源

- [Emerald Arena 原作者](https://github.com/GBurgardt/pokemon-emerald-arena)
- [Meowth 上游](https://github.com/Olcmyk/Meowth-GBA-Translator)
- [旧 demo 工作分支](https://github.com/q13007868130/git-demo/tree/meowth-gba-custom-api-gui)

本目录是第三方汉化工作区，不代表游戏原作者提供了中文官方版本。
