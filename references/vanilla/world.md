# World API

## IWorld

> `import crafttweaker.world.IWorld;`

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `remote` | bool | 是否为客户端 |
| `dimension` | int | 维度 ID |
| `dimensionName` | string | 维度名称 |
| `worldType` | string | 世界类型 |
| `difficulty` | string | 难度 |
| `isDaytime` | bool | 是否白天 |
| `isRaining` | bool | 是否下雨 |
| `isThundering` | bool | 是否雷暴 |
| `rainStrength` | float | 雨强度 |
| `thunderStrength` | float | 雷强度 |
| `time` | long | 世界时间 |
| `totalTime` | long | 总时间 |
| `seed` | long | 种子 |
| `seaLevel` | int | 海平面高度 |
| `spawnPoint` | IBlockPos | 出生点 |
| `borderCenterX` | double | 边界中心 X |
| `borderCenterZ` | double | 边界中心 Z |
| `borderSize` | double | 边界大小 |
| `borderDamagePerBlock` | double | 边界每格伤害 |
| `borderWarningDistance` | double | 边界警告距离 |
| `borderWarningTime` | double | 边界警告时间 |
| `maxHeight` | int | 最大高度 |
| `minHeight` | int | 最小高度 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getBlock(IBlockPos)` | IBlockPos | IBlock | 获取方块 |
| `.getBlock(int, int, int)` | int, int, int | IBlock | 获取方块 |
| `.setBlockState(IBlockState, IBlockPos)` | IBlockState, IBlockPos | bool | 设置方块状态 |
| `.setBlockState(IBlockState, IData, IBlockPos)` | IBlockState, IData, IBlockPos | bool | 设置方块状态并指定 TileEntity NBT 数据 |
| `.getBlockState(IBlockPos)` | IBlockPos | IBlockState | 获取方块状态 |
| `.getBlockState(int, int, int)` | int, int, int | IBlockState | 获取方块状态 |
| `.getTileEntity(IBlockPos)` | IBlockPos | ITileEntity | 获取 Tile Entity |
| `.getLightFor(EnumSkyBlock, IBlockPos)` | EnumSkyBlock, IBlockPos | int | 获取光照 |
| `.getLightValue(IBlockPos)` | IBlockPos | int | 获取光照值 |
| `.getBrightness(int, int, int)` | int, int, int | int | 获取指定坐标的亮度 |
| `.getBrightness(IBlockPos)` | IBlockPos | int | 获取指定位置的亮度 |
| `.isAirBlock(IBlockPos)` | IBlockPos | bool | 是否空气方块 |
| `.isBlockLoaded(IBlockPos)` | IBlockPos | bool | 方块是否已加载 |
| `.isBlockModifiable(IPlayer, IBlockPos)` | IPlayer, IBlockPos | bool | 玩家是否可修改方块 |
| `.canSeeSky(IBlockPos)` | IBlockPos | bool | 是否能看到天空 |
| `.canBlockSeeSky(IBlockPos)` | IBlockPos | bool | 方块是否能看到天空 |
| `.isBlockNormalCube(IBlockPos)` | IBlockPos | bool | 是否普通方块 |
| `.isBlockFullCube(IBlockPos)` | IBlockPos | bool | 是否完整方块 |
| `.isBlockFullBlock(IBlockPos)` | IBlockPos | bool | 是否完整方块 |
| `.getStrongPower(IBlockPos, EnumFacing)` | IBlockPos, EnumFacing | int | 获取强红石信号 |
| `.getRedstonePower(IBlockPos, EnumFacing)` | IBlockPos, EnumFacing | int | 获取红石信号 |
| `.isBlockIndirectlyGettingPowered(IBlockPos)` | IBlockPos | bool | 是否间接被红石充能 |
| `.createExplosion(IEntity, double, double, double, float, bool, bool)` | IEntity, double, double, double, float, bool, bool | IExplosion | 创建爆炸对象（不执行）。参数：放置者、坐标、大小、是否引火、是否破坏地形 |
| `.performExplosion(IEntity, double, double, double, float, bool, bool)` | IEntity, double, double, double, float, bool, bool | IExplosion | 创建并执行爆炸。参数：放置者、坐标、大小、是否引火、是否破坏地形 |
| `.performExplosion(IExplosion)` | IExplosion | IExplosion | 执行已有的爆炸对象 |
| `.createLightningBolt(double, double, double, @Optional bool)` | double, double, double, bool（可选） | IEntity | 在指定坐标创建闪电 |
| `.addWeatherEffect(IEntity)` | IEntity | bool | 添加天气效果 |
| `.spawnEntity(IEntity)` | IEntity | bool | 生成实体 |
| `.removeEntity(IEntity)` | IEntity | bool | 移除实体 |
| `.removeEntity(int)` | int | void | 移除实体 |
| `.getEntity(int)` | int | IEntity | 获取实体 |
| `.getEntitiesWithinAABB(Class, IAxisAlignedBB)` | Class, IAxisAlignedBB | List | 获取 AABB 内实体 |
| `.addBlockEvent(IBlockPos, Block, int, int)` | IBlockPos, Block, int, int | void | 添加方块事件 |
| `.getBiome(IBlockPos)` | IBlockPos | IBiome | 获取生物群系 |
| `.getBiome(IPosition3f)` | IPosition3f | IBiome | 获取生物群系 |
| `.getTopSolidBlock(IBlockPos)` | IBlockPos | IBlockPos | 获取最高实心方块 |
| `.getActualHeight()` | 无 | int | 获取实际高度 |
| `.getChunks()` | 无 | List | 获取所有区块 |
| `.getPlayers(Class, Predicate)` | Class, Predicate | List | 获取玩家列表 |
| `.getGameRules()` | 无 | IGameRules | 获取游戏规则 |
| `.setRainStrength(float)` | float | void | 设置雨强度 |
| `.setThunderStrength(float)` | float | void | 设置雷强度 |
| `.setTime(long)` | long | void | 设置时间 |
| `.setTotalTime(long)` | long | void | 设置总时间 |
| `.setSpawnPoint(IBlockPos)` | IBlockPos | void | 设置出生点 |
| `.setBlock(int, int, int, Block)` | int, int, int, Block | void | 设置方块 |
| `.setBlock(int, int, int, Block, int, int)` | int, int, int, Block, int, int | void | 设置方块 |
| `.destroyBlock(IBlockPos, bool)` | IBlockPos, bool | bool | 破坏方块 |
| `.destroyBlock(int, int, int, bool)` | int, int, int, bool | bool | 破坏方块 |
| `.playSound(IPlayer, IBlockPos, string, string, float, float)` | IPlayer, IBlockPos, string, string, float, float | void | 播放声音 |
| `.playSound(IPlayer, double, double, double, string, string, float, float)` | IPlayer, double, double, double, string, string, float, float | void | 播放声音 |
| `.spawnParticle(string, double, double, double, double, double, double, int...)` | string, double, double, double, double, double, double, int... | void | 生成粒子 |
| `.rayTraceBlocks(IVector3d, IVector3d, @Optional bool, @Optional bool, @Optional(true) bool)` | IVector3d, IVector3d, bool, bool, bool | IRayTraceResult | 射线检测。第一个向量为起点，第二个为方向和长度。最后三个参数：是否在液体处停止、是否忽略无碰撞箱方块、是否返回最后不可碰撞方块 |
| `.getPickedBlock(IBlockPos, IRayTraceResult, IPlayer)` | IBlockPos, IRayTraceResult, IPlayer | IItemStack | 获取拾取的方块物品（可返回 null） |
| `.isSpawnChunk(int, int)` | int, int | bool | 检查是否为出生区块 |
| `.extinguishFire(IPlayer, IBlockPos, IFacing)` | IPlayer, IBlockPos, IFacing | bool | 扑灭火焰 |

---

## IBlockPos

> `import crafttweaker.world.IBlockPos;`

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `x` | int | X 坐标 |
| `y` | int | Y 坐标 |
| `z` | int | Z 坐标 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.add(int, int, int)` | int, int, int | IBlockPos | 坐标加法 |
| `.add(IBlockPos)` | IBlockPos | IBlockPos | 坐标加法 |
| `.subtract(IBlockPos)` | IBlockPos | IBlockPos | 坐标减法 |
| `.north()` | 无 | IBlockPos | 北方坐标 |
| `.south()` | 无 | IBlockPos | 南方坐标 |
| `.east()` | 无 | IBlockPos | 东方坐标 |
| `.west()` | 无 | IBlockPos | 西方坐标 |
| `.up()` | 无 | IBlockPos | 上方坐标 |
| `.down()` | 无 | IBlockPos | 下方坐标 |
| `.offset(EnumFacing)` | EnumFacing | IBlockPos | 指定方向坐标 |
| `.offset(EnumFacing, int)` | EnumFacing, int | IBlockPos | 指定方向指定距离坐标 |
| `.distanceSq(IBlockPos)` | IBlockPos | double | 距离平方 |
| `.distanceSq(double, double, double)` | double, double, double | double | 距离平方 |
| `.distanceSqToCenter(double, double, double)` | double, double, double | double | 到中心点距离平方 |
| `.withinDistance(IBlockPos, double)` | IBlockPos, double | bool | 是否在指定距离内 |
| `.getX()` | 无 | int | 获取 X |
| `.getY()` | 无 | int | 获取 Y |
| `.getZ()` | 无 | int | 获取 Z |
| `.toLong()` | 无 | long | 转为 long |
| `.fromLong(long)` | long | IBlockPos | 从 long 转换 |
| `.asPosition3f` | 无 | IPosition3f | 转为 Position3f 对象 |
| `.getOffset(IFacing, int)` | IFacing, int | IBlockPos | 获取指定方向偏移指定距离后的新位置 |

---

## IBiome

> `import crafttweaker.world.IBiome;`

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 生物群系名称 |
| `id` | int | ID |
| `temperature` | float | 温度 |
| `rainfall` | float | 降雨量 |
| `humidity` | float | 湿度 |
| `isSnowyBiome` | bool | 是否雪地 |
| `isHumid` | bool | 是否潮湿 |
| `ignorePlayerSpawnSuitability` | bool | 是否忽略玩家生成适应性 |
| `waterColorMultiplier` | int | 水颜色倍增器 |
| `minHeight` | float | 最小高度 |
| `maxHeight` | float | 最大高度 |
| `baseHeight` | float | 基础高度 |
| `heightVariation` | float | 高度变化 |
| `enableRain` | bool | 是否启用雨 |
| `enableSnow` | bool | 是否启用雪 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.canRain()` | 无 | bool | 是否可以下雨 |
| `.isSnowyBiome()` | 无 | bool | 是否雪地 |
| `.setTemperature(float)` | float | void | 设置温度 |
| `.setRainfall(float)` | float | void | 设置降雨量 |
| `.setWaterColorMultiplier(int)` | int | void | 设置水颜色倍增器 |
| `.setEnableRain(bool)` | bool | void | 设置是否启用雨 |
| `.setEnableSnow(bool)` | bool | void | 设置是否启用雪 |
| `.setMinHeight(float)` | float | void | 设置最小高度 |
| `.setMaxHeight(float)` | float | void | 设置最大高度 |
| `.setBaseHeight(float)` | float | void | 设置基础高度 |
| `.setHeightVariation(float)` | float | void | 设置高度变化 |

---

## IBlockAccess

> `import crafttweaker.world.IBlockAccess;`

IBlockAccess 是 IWorld 的父接口，所有 IWorld 对象都可以使用 IBlockAccess 的方法。

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getBlockState(IBlockPos)` | IBlockPos | IBlockState | 获取指定位置的方块状态 |
| `.isAirBlock(IBlockPos)` | IBlockPos | bool | 检查指定位置是否为空气方块 |
| `.getStrongPower(IBlockPos, IFacing)` | IBlockPos, IFacing | int | 获取指定方块面的强红石信号 |

---

## IExplosion

> `import crafttweaker.world.IExplosion;`

IExplosion 代表一个爆炸对象，可以通过 IWorld 的 `createExplosion` 或 `performExplosion` 获取。

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 爆炸所在的世界 |
| `placedBy` | IEntityLivingBase | 发起爆炸的实体（TNT 则为放置 TNT 的实体，可能为 null） |
| `position` | Position3f | 爆炸位置 |
| `affectedBlockPositions` | IBlockPos[] | 爆炸影响的方块位置列表（`doExplosionA()` 调用前可能为空） |
| `playerKnockbackMap` | Map\<IPlayer, IVector3d\> | 爆炸区域内玩家的击退映射 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.clearAffectedBlockPositions()` | 无 | void | 清除受影响方块位置列表 |
| `.onExplosionStart(IWorld)` | IWorld | bool | 触发 ExplosionStart 事件，可用于在手动引爆前取消爆炸 |
| `.doExplosionA()` | 无 | void | 执行爆炸第一部分：实体伤害、击退、赋值 affectedBlockPositions |
| `.doExplosionB(bool)` | bool | void | 执行爆炸第二部分：声音、粒子、方块破坏/掉落、火焰生成 |

---

## IFacing

> `import crafttweaker.world.IFacing;`

IFacing 代表一个方向（北、南、东、西、上、下）。

### 静态方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `IFacing.north()` | 无 | IFacing | 获取北方向 |
| `IFacing.east()` | 无 | IFacing | 获取东方向 |
| `IFacing.south()` | 无 | IFacing | 获取南方向 |
| `IFacing.west()` | 无 | IFacing | 获取西方向 |
| `IFacing.down()` | 无 | IFacing | 获取下方向 |
| `IFacing.up()` | 无 | IFacing | 获取上方向 |
| `IFacing.fromString(string)` | string | IFacing | 从字符串获取方向（如 "NORTH"） |
| `IFacing.getDirectionFromEntityLiving(IBlockPos, IEntityLivingBase)` | IBlockPos, IEntityLivingBase | IFacing | 根据实体位置获取方向（常用于确定方块放置朝向，可返回 UP/DOWN） |

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 方向名称 |
| `rotateY` | IFacing | 绕 Y 轴旋转后的方向 |
| `opposite` | IFacing | 反方向 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.compare(IFacing)` | IFacing | int | 比较两个方向，相等返回 0 |

---

## IRayTraceResult

> `import crafttweaker.world.IRayTraceResult;`

IRayTraceResult 代表玩家视线或点击的射线检测结果。

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `isMiss` | bool | 是否未命中 |
| `isBlock` | bool | 是否命中方块 |
| `blockPos` | IBlockPos | 命中的方块位置（非 bool 返回值可为 null） |
| `sideHit` | IFacing | 命中的方块面（非 bool 返回值可为 null） |

---

## IVector3d

> `import crafttweaker.world.IVector3d;`

IVector3d 是一个使用三个 double 表示方向的向量对象。

### 静态方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `IVector3d.create(double, double, double)` | double, double, double | IVector3d | 创建新的 IVector3d 对象 |

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `x` | double | X 分量 |
| `y` | double | Y 分量 |
| `z` | double | Z 分量 |
| `normalized` | IVector3d | 归一化后的向量 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.dotProduct(IVector3d)` | IVector3d | double | 点积 |
| `.crossProduct(IVector3d)` | IVector3d | IVector3d | 叉积 |
| `.subtract(IVector3d)` | IVector3d | IVector3d | 向量减法 |
| `.subtractReverse(IVector3d)` | IVector3d | IVector3d | 反向减法（other - this） |
| `.add(IVector3d)` | IVector3d | IVector3d | 向量加法 |
| `.distanceTo(IVector3d)` | IVector3d | double | 到另一个向量的距离 |
| `.scale(double)` | double | IVector3d | 缩放向量 |

---

## IWorldInfo

> `import crafttweaker.world.IWorldInfo;`

IWorldInfo 用于获取 IWorld 的更多详细信息，通过 `world.worldInfo` 获取。

### 属性

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

---

## IWorldProvider

> `import crafttweaker.world.IWorldProvider;`

IWorldProvider 用于获取 IWorld 的更多维度信息，通过 `world.provider` 获取。

### 静态方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `IWorldProvider.getFromID(int)` | int | IWorldProvider | 通过维度 ID 获取 WorldProvider（需在游戏运行时调用） |

### 属性

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

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getBiome(IBlockPos)` | IBlockPos | IBiome | 获取指定位置的生物群系 |
| `.getMoonPhase(long)` | long | int | 获取指定时间的月相 |
| `.getRespawnDimension(IPlayer)` | IPlayer | IWorldProvider | 获取玩家的重生维度 |
| `.getStarBrightness(float)` | float | float | 获取星星亮度 |
| `.getSunBrightness(float)` | float | float | 获取太阳亮度 |
| `.getSunBrightnessFactor(float)` | float | float | 获取太阳亮度因子 |
| `.isBlockHighHumidity(IBlockPos)` | IBlockPos | bool | 检查方块是否处于高湿度环境 |

---

## 草丛掉落

```zenscript
// 添加打草掉落（百分比权重）
vanilla.seeds.addSeed(<minecraft:carrot> % 1);  // 1% 几率

// 移除打草掉落
vanilla.seeds.removeSeed(<minecraft:wheat_seeds>);
```

---

## ZenUtils 扩展（需安装 ZenUtils）

> `import mods.zenutils.*;`

### IWorld 扩展

对 `crafttweaker.world.IWorld` 的扩展，所有世界对象自动可用。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `getCustomTileEntity(IBlockPos)` | IBlockPos | TileEntityInGame | 获取指定位置的 ZenUtils 自定义方块实体，不存在则返回 null |
| `getLiquidHandler(IBlockPos, @Optional IFacing)` | IBlockPos, IFacing（可选） | LiquidHandler | 获取方块实体的流体处理器 |
| `gameRuleHelper` | 无 | GameRuleHelper | 获取游戏规则管理器 |
| `getGameRuleHelper()` | 无 | GameRuleHelper | 获取游戏规则管理器（方法形式） |

### GameRuleHelper（游戏规则）

> `import mods.zenutils.GameRuleHelper;`

通过 `world.gameRuleHelper` 或 `world.getGameRuleHelper()` 获取。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `addGameRule(String, String, String)` | key, value, type | void | 添加自定义游戏规则。type 必须为 `"Any"`、`"Numeric"` 或 `"Boolean"` |
| `hasRule(String)` | String | bool | 检查规则是否存在 |
| `getRules()` | 无 | String[] | 获取所有规则名 |
| `getBoolean(String)` | String | bool | 获取布尔值规则 |
| `getInt(String)` | String | int | 获取整数规则 |
| `getString(String)` | String | String | 获取字符串规则 |
