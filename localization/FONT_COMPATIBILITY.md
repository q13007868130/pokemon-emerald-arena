# Emerald Arena 0.13.0：中文字库与白屏问题

## 已知事实（静态二进制检查）

检查对象：
- 干净的 Emerald Arena 0.13.0 ROM（32 MiB）。
- 一份打了中文字体补丁、并翻译了部分文本的 ROM（32 MiB）。

`Pokemon_GBA_Font_Patch` 的绿宝石方案将 `HackFunctionAddresses` 固定在 GBA 地址 `0x09FD0000`（ROM 文件偏移 `0x01FD0000`），同时更改文本渲染和宽度函数等入口。

干净的 Emerald Arena 0.13.0 ROM 在偏移 `0x01FD0000` 到 `0x01FF0633` 存在大量非空内容；比较发现该区域被中文补丁大量改写。示例：`0x01FF0000` 的原始数据与汉化 ROM 不同。因此，该区域 **不是安全的通用字库插入空间**。

**重要**：此结果是静态覆盖证据，不代表白屏的唯一根因已被运行时断点确认。文字替换、指针与字体 Hook 都需要进一步分析。

## 正确路线

1. 不以打过旧字库的 ROM 作为源码基础；先使用原作者 `BUILD.md` 指定的源码构建方法。
2. 在 `pret/pokeemerald` 源码层实现/适配中文字形和文本控制码；不要硬写 `0x09FD0000`。
3. 先用一个中文字符串做最小验证，确保主菜单、地图文本、**实时野战**、**经典战斗**均能运行。
4. 对照二进制字节、运行时字体缓存与图形内存/栈使用情况，检查是否有 VRAM/OAM/DMA 冲突。
5. 最后逐步引入翻译文件，核对文本宽度、指针、保存与战斗结算。
6. 每轮编译后保留 ROM 哈希与 mGBA 实际测试记录。

## 资料

- `game/native-engine.patch`：Emerald Arena 原有战斗入口补丁
- `game/overlay/src/realtime_arena.c`：实时战斗控制器
- [Pokemon_GBA_Font_Patch](https://github.com/Olcmyk/Pokemon_GBA_Font_Patch)
- [BUILD.md](../BUILD.md)

**现在不应声称已经修好白屏。** 需要实际编译并在模拟器中验证。
