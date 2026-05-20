# FTB Money CraftTweaker API 参考

> Mod ID: `ftbmoney`
> 前置条件: Roids-Tweaker
> 导入: 无需额外导入

## API 列表

### IPlayer 扩展

可在任何 IPlayer 上调用，用于操作玩家的 FTB Money 余额。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getFtbMoney()` | 无 | long | 获取玩家余额 |
| `.setFtbMoney(long amount)` | amount | void | 设置玩家余额 |
