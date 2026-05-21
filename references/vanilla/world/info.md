# 世界信息 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 部分需要 ZenUtils
> 导入: `import crafttweaker.world.IWorldInfo;`、`import crafttweaker.world.IWorldProvider;`、`import mods.zenutils.GameRuleHelper;`

IWorldInfo、IWorldProvider、GameRuleHelper 世界信息 API。

---

## API 列表

### IWorldInfo（世界信息）

> `import crafttweaker.world.IWorldInfo;`

IWorldInfo 用于获取 IWorld 的更多详细信息，通过 `world.worldInfo` 获取。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `commandsAllowed` | bool | 是否允许命令 |
| `borderCenterX` | double | 边界中心 X |
| `borderCenterZ` | double | 边界中心 Z |
| `borderDamagePerBlock` | double | 边界每格伤害 |
| `borderSafeZone` | double | 边界安全区 |
| `borderSize` | double | 边界大小 |
| `borderWarningDistance` | int | 边界警告距离 |
| `borderWarningTime` | int | 边界警告时间 |
| `cleanWeatherTime` | double | 晴天时间 |
| `difficulty` | string | 难度 |
| `generatorOptions` | string | 世界生成器选项 |
| `lastTimePlayed` | long | 上次游玩时间 |
| `rainTime` | int | 下雨时间 |
| `saveVersion` | int | 存档版本 |
| `seed` | long | 种子 |
| `spawnX` | int | 出生点 X |
| `spawnY` | int | 出生点 Y |
| `spawnZ` | int | 出生点 Z |
| `thunderTime` | int | 雷暴时间 |
| `versionId` | int | 版本 ID |
| `versionName` | string | 版本名称 |
| `worldName` | string | 世界名称 |
| `worldTotalTime` | long | 世界总时间 |
| `boderLerpTarget` | double | 边界插值目标 |
| `boderLerpTime` | long | 边界插值时间 |
| `difficultyLocked` | bool | 难度是否锁定 |
| `hardcoreModeEnabled` | bool | 是否启用极限模式 |
| `initialized` | bool | 是否已初始化 |
| `mapFeaturesEnabled` | bool | 是否启用地图特征 |
| `thundering` | bool | 是否雷暴 |
| `versionSnapshot` | bool | 是否为快照版本 |

### IWorldProvider（世界维度提供者）

> `import crafttweaker.world.IWorldProvider;`

IWorldProvider 用于获取 IWorld 的更多维度信息，通过 `world.provider` 获取。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `IWorldProvider.getFromID(int)` | IWorldProvider | 通过维度 ID 获取 WorldProvider（需在游戏运行时调用） |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `actualHeight` | int | 实际高度 |
| `actualGroundLevel` | int | 平均地面高度 |
| `cloudHeight` | float | 云层高度 |
| `currentMoonPhaseFactor` | float | 当前月相因子 |
| `dimensionID` | int | 维度 ID |
| `height` | int | 世界高度 |
| `horizon` | double | 地平线高度 |
| `lightBrightnesTable` | float[] | 亮度表 |
| `movementFactor` | double | 移动因子 |
| `randomizedSpawnPoint` | IBlockPos | 随机出生点 |
| `saveFolder` | string | 存档文件夹名 |
| `seed` | long | 种子 |
| `spawnCoordinate` | IBlockPos | 出生坐标 |
| `spawnPoint` | IBlockPos | 出生点 |
| `voidFogYFactor` | double | 虚空迷雾 Y 因子 |
| `worldTime` | long | 世界时间 |
| `canRespawnHere` | bool | 是否可以在此重生 |
| `waterVaporize` | bool | 水是否蒸发（地狱） |
| `skylight` | bool | 是否有天空光照 |
| `daytime` | bool | 是否白天 |
| `nether` | bool | 是否为地狱 |
| `skyColored` | bool | 天空是否有颜色 |
| `surfaceWorld` | bool | 是否为地表世界 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getBiome(IBlockPos)` | IBiome | 获取指定位置的生物群系 |
| `.getMoonPhase(long)` | int | 获取指定时间的月相 |
| `.getRespawnDimension(IPlayer)` | IWorldProvider | 获取玩家的重生维度 |
| `.getStarBrightness(float)` | float | 获取星星亮度 |
| `.getSunBrightness(float)` | float | 获取太阳亮度 |
| `.getSunBrightnessFactor(float)` | float | 获取太阳亮度因子 |
| `.isBlockHighHumidity(IBlockPos)` | bool | 检查方块是否处于高湿度环境 |

### GameRuleHelper（游戏规则）

> `import mods.zenutils.GameRuleHelper;`

通过 `world.gameRuleHelper` 或 `world.getGameRuleHelper()` 获取。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGameRule(String key, String value, String type)` | void | 添加自定义游戏规则。type 必须为 `"Any"`、`"Numeric"` 或 `"Boolean"` |
| `.hasRule(String)` | bool | 检查规则是否存在 |
| `.getRules()` | String[] | 获取所有规则名 |
| `.getBoolean(String)` | bool | 获取布尔值规则 |
| `.getInt(String)` | int | 获取整数规则 |
| `.getString(String)` | String | 获取字符串规则 |
