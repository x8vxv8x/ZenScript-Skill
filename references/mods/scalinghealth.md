# Scaling Health CraftTweaker API 参考

> Mod ID: `scalinghealth`
> 前置条件: Roids-Tweaker
> 导入: `import mods.ctintegration.scalinghealth.DifficultyManager;`

## API 列表

### DifficultyManager

> `import mods.ctintegration.scalinghealth.DifficultyManager;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setDifficulty(IPlayer player, double value)` | void | 设置玩家难度 |
| `.addDifficulty(IPlayer player, double value)` | void | 增加玩家难度 |
| `.addDifficulty(IPlayer player, double value, boolean affectWorldDifficulty)` | void | 增加玩家难度（可选是否影响世界难度） |
| `.getDifficulty(IPlayer player)` | double | 获取玩家难度 |
| `.getWorldDifficulty(IWorld world)` | double | 获取世界难度 |
| `.setWorldDifficulty(IWorld world, double value)` | void | 设置世界难度 |
| `.addWorldDifficulty(IWorld world, double value)` | void | 增加世界难度 |
| `.getLastTimePlayed(IPlayer player)` | IDate | 获取最后游玩时间 |
| `.getMaxHealth(IPlayer player)` | float | 获取最大生命值 |
| `.setMaxHealth(IPlayer player, float value)` | void | 设置最大生命值 |
| `.addMaxHealth(IPlayer player, float value)` | void | 增加最大生命值 |
| `.getAreaDifficulty(IPlayer player)` | double | 获取区域难度 |
| `.getAreaDifficulty(IWorld world, IBlockPos pos)` | double | 获取指定位置的区域难度 |

### IPlayer 扩展

可在任何 IPlayer 上调用。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getScalingHealthMaxHealth()` | 无 | double | 获取最大生命值 |
| `.setScalingHealthMaxHealth(double value)` | value | void | 设置最大生命值 |
| `.getAreaDifficulty()` | 无 | double | 获取区域难度 |
| `.getLastTimePlayed()` | 无 | double | 获取最后游玩时间 |

### IWorld 扩展

可在任何 IWorld 上调用。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getWorldDifficulty()` | 无 | double | 获取世界难度 |
| `.setWorldDifficulty(double value)` | value | void | 设置世界难度 |
| `.getAreaDifficulty(IBlockPos pos)` | pos | double | 获取指定位置的区域难度 |
