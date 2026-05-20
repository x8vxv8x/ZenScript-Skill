# Nyx CraftTweaker API 参考

> Mod ID: `nyx`
> 前置条件: Roids-Tweaker
> 导入: 无需额外导入

## API 列表

### IWorld 扩展

可在任何 IWorld 上调用，用于检测 Nyx 模组的月相事件。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.isBloodMoon()` | boolean | 是否为血月 |
| `.isStarShower()` | boolean | 是否为流星雨 |
| `.isFullMoon()` | boolean | 是否为满月 |
| `.isHarvestMoon()` | boolean | 是否为丰收之月 |
