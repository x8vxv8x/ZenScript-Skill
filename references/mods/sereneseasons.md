# Serene Seasons CraftTweaker API 参考

> Mod ID: `sereneseasons`
> 前置条件: Roids-Tweaker
> 导入: 见各章节

## API 列表

### IWorld 扩展

可在任何 IWorld 上调用。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getSeasonState()` | ISeasonState | 获取季节状态对象 |

### ISeasonState

通过 `IWorld.getSeasonState()` 获取。以下均为 ZenGetter。

| 属性 | 类型 | 说明 |
|------|------|------|
| `dayDuration` | int | 白天时长 |
| `subSeasonDuration` | int | 子季节时长 |
| `seasonDuration` | int | 季节时长 |
| `cycleDuration` | int | 周期时长 |
| `seasonCycleTicks` | int | 季节周期 tick 数 |
| `day` | int | 当前天数 |
| `season` | int | 当前季节编号（0=春, 1=夏, 2=秋, 3=冬） |
| `subSeason` | int | 当前子季节编号（0=早春 至 11=晚冬） |
| `seasonName` | string | 季节名（SPRING, SUMMER, AUTUMN, WINTER） |
| `subSeasonName` | string | 子季节名（EARLY_SPRING, MID_SPRING, LATE_SPRING 等） |
| `tropicalSeason` | int | 热带季节编号（0=早旱 至 5=晚雨） |
| `tropicalSeasonName` | string | 热带季节名 |
