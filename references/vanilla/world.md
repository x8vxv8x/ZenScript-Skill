# World CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.world.IWorld;`、`import crafttweaker.world.IBlockPos;`、`import crafttweaker.world.IBiome;`、`import crafttweaker.world.IBlockAccess;`、`import crafttweaker.world.IExplosion;`、`import crafttweaker.world.IFacing;`、`import crafttweaker.world.IRayTraceResult;`、`import crafttweaker.world.IVector3d;`、`import crafttweaker.world.IWorldInfo;`、`import crafttweaker.world.IWorldProvider;`

世界、位置、方向、爆炸等相关 API。

---

## API 列表

### IWorld（世界）

> `import crafttweaker.world.IWorld;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `IWorld.getFromID(int)` | IWorld | 通过维度 ID 获取世界对象（需在游戏运行时调用，不可在加载阶段使用） |

#### @ZenGetter

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
| `moonPhase` | int | 当前月相 |
| `dimensionType` | string | 维度类型名称 |
| `worldInfo` | IWorldInfo | 世界信息对象，可获取更详细的属性 |
| `provider` | IWorldProvider | 世界维度提供者对象，可获取更详细的维度信息 |
| `random` | IRandom | 世界随机生成器 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getBlock(IBlockPos)` | IBlock | 获取方块 |
| `.getBlock(int, int, int)` | IBlock | 获取方块 |
| `.setBlockState(IBlockState, IBlockPos)` | bool | 设置方块状态 |
| `.setBlockState(IBlockState, IData, IBlockPos)` | bool | 设置方块状态并指定 TileEntity NBT 数据 |
| `.getBlockState(IBlockPos)` | IBlockState | 获取方块状态 |
| `.getBlockState(int, int, int)` | IBlockState | 获取方块状态 |
| `.getTileEntity(IBlockPos)` | ITileEntity | 获取 Tile Entity |
| `.getLightFor(EnumSkyBlock, IBlockPos)` | int | 获取光照 |
| `.getLightValue(IBlockPos)` | int | 获取光照值 |
| `.getBrightness(int, int, int)` | int | 获取指定坐标的亮度 |
| `.getBrightness(IBlockPos)` | int | 获取指定位置的亮度 |
| `.isAirBlock(IBlockPos)` | bool | 是否空气方块 |
| `.isBlockLoaded(IBlockPos)` | bool | 方块是否已加载 |
| `.isBlockModifiable(IPlayer, IBlockPos)` | bool | 玩家是否可修改方块 |
| `.canSeeSky(IBlockPos)` | bool | 是否能看到天空 |
| `.canBlockSeeSky(IBlockPos)` | bool | 方块是否能看到天空 |
| `.isBlockNormalCube(IBlockPos)` | bool | 是否普通方块 |
| `.isBlockFullCube(IBlockPos)` | bool | 是否完整方块 |
| `.isBlockFullBlock(IBlockPos)` | bool | 是否完整方块 |
| `.getStrongPower(IBlockPos, EnumFacing)` | int | 获取强红石信号 |
| `.getRedstonePower(IBlockPos, EnumFacing)` | int | 获取红石信号 |
| `.isBlockIndirectlyGettingPowered(IBlockPos)` | bool | 是否间接被红石充能 |
| `.createExplosion(IEntity, double, double, double, float, bool, bool)` | IExplosion | 创建爆炸对象（不执行）。参数：放置者、坐标、大小、是否引火、是否破坏地形 |
| `.performExplosion(IEntity, double, double, double, float, bool, bool)` | IExplosion | 创建并执行爆炸。参数：放置者、坐标、大小、是否引火、是否破坏地形 |
| `.performExplosion(IExplosion)` | IExplosion | 执行已有的爆炸对象 |
| `.createLightningBolt(double, double, double, @Optional bool)` | IEntity | 在指定坐标创建闪电 |
| `.addWeatherEffect(IEntity)` | bool | 添加天气效果 |
| `.spawnEntity(IEntity)` | bool | 生成实体 |
| `.removeEntity(IEntity)` | bool | 移除实体 |
| `.removeEntity(int)` | void | 移除实体 |
| `.getEntity(int)` | IEntity | 获取实体 |
| `.getEntitiesWithinAABB(Class, IAxisAlignedBB)` | List | 获取 AABB 内实体 |
| `.addBlockEvent(IBlockPos, Block, int, int)` | void | 添加方块事件 |
| `.getBiome(IBlockPos)` | IBiome | 获取生物群系 |
| `.getBiome(IPosition3f)` | IBiome | 获取生物群系 |
| `.getTopSolidBlock(IBlockPos)` | IBlockPos | 获取最高实心方块 |
| `.getActualHeight()` | int | 获取实际高度 |
| `.getChunks()` | List | 获取所有区块 |
| `.getPlayers(Class, Predicate)` | List | 获取玩家列表 |
| `.getGameRules()` | IGameRules | 获取游戏规则 |
| `.setRainStrength(float)` | void | 设置雨强度 |
| `.setThunderStrength(float)` | void | 设置雷强度 |
| `.setTime(long)` | void | 设置时间 |
| `.setTotalTime(long)` | void | 设置总时间 |
| `.setSpawnPoint(IBlockPos)` | void | 设置出生点 |
| `.setBlock(int, int, int, Block)` | void | 设置方块 |
| `.setBlock(int, int, int, Block, int, int)` | void | 设置方块 |
| `.destroyBlock(IBlockPos, bool)` | bool | 破坏方块 |
| `.destroyBlock(int, int, int, bool)` | bool | 破坏方块 |
| `.playSound(IPlayer, IBlockPos, string, string, float, float)` | void | 播放声音 |
| `.playSound(IPlayer, double, double, double, string, string, float, float)` | void | 播放声音 |
| `.spawnParticle(string, double, double, double, double, double, double, int...)` | void | 生成粒子 |
| `.rayTraceBlocks(IVector3d, IVector3d, @Optional bool, @Optional bool, @Optional(true) bool)` | IRayTraceResult | 射线检测。第一个向量为起点，第二个为方向和长度。最后三个参数：是否在液体处停止、是否忽略无碰撞箱方块、是否返回最后不可碰撞方块 |
| `.getPickedBlock(IBlockPos, IRayTraceResult, IPlayer)` | IItemStack | 获取拾取的方块物品（可返回 null） |
| `.isSpawnChunk(int, int)` | bool | 检查是否为出生区块 |
| `.extinguishFire(IPlayer, IBlockPos, IFacing)` | bool | 扑灭火焰 |

---

## Roids-Tweaker 扩展

### IWorld 扩展

可在任何 IWorld 上调用。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.setOrCreateGameRule(String key, String value)` | key, value | void | 设置游戏规则，不存在则创建 |
| `.getGameRules()` | 无 | IGameRules | 获取游戏规则对象 |
| `.playSound(String soundResourceLocation, String soundCategory, Position3f location, float volume, float pitch, @Optional bool distanceDelay)` | sound, category, location, volume, pitch, distanceDelay | void | 在指定位置播放声音 |
| `.canSeeSky(IBlockPos pos)` | pos | bool | 指定位置是否能看到天空 |
| `.canSnowAt(IBlockPos pos, bool lightCheck)` | pos, lightCheck | bool | 指定位置是否可降雪 |
| `.canBlockFreeze(IBlockPos pos, bool noWaterAdj)` | pos, noWaterAdj | bool | 指定位置方块是否可冻结 |
| `.getBlockLight(IBlockPos pos)` | pos | int | 获取方块光照 |
| `.getEntityItemsWithinAABB(IAxisAlignedBB aabb)` | aabb | IEntityItem[] | 获取 AABB 内的物品实体 |
| `.getEntitiesWithinAABB(IAxisAlignedBB aabb, @Optional IEntityDefinition entityType)` | aabb, entityType | IEntity[] | 获取 AABB 内的实体 |
| `.getSkyLight(IBlockPos pos)` | pos | int | 获取天空光照 |
| `.getTopBlock(IBlockPos pos)` | pos | IBlockPos | 获取最高方块 |
| `.getTopSolidBlock(IBlockPos pos)` | pos | IBlockPos | 获取最高实心方块 |
| `.setSpawnerEntity(IBlockPos pos, IEntityLivingBase entity)` | pos, entity | bool | 设置刷怪笼实体 |
| `.createEntityXp(int value)` | value | IEntityXp | 创建经验球实体 |
| `.spawnEntityXp(int value, IBlockPos pos)` | value, pos | void | 在指定位置生成经验球 |

### IBlockPos（方块位置）

> `import crafttweaker.world.IBlockPos;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `x` | int | X 坐标 |
| `y` | int | Y 坐标 |
| `z` | int | Z 坐标 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(int, int, int)` | IBlockPos | 坐标加法 |
| `.add(IBlockPos)` | IBlockPos | 坐标加法 |
| `.subtract(IBlockPos)` | IBlockPos | 坐标减法 |
| `.north()` | IBlockPos | 北方坐标 |
| `.south()` | IBlockPos | 南方坐标 |
| `.east()` | IBlockPos | 东方坐标 |
| `.west()` | IBlockPos | 西方坐标 |
| `.up()` | IBlockPos | 上方坐标 |
| `.down()` | IBlockPos | 下方坐标 |
| `.offset(EnumFacing)` | IBlockPos | 指定方向坐标 |
| `.offset(EnumFacing, int)` | IBlockPos | 指定方向指定距离坐标 |
| `.distanceSq(IBlockPos)` | double | 距离平方 |
| `.distanceSq(double, double, double)` | double | 距离平方 |
| `.distanceSqToCenter(double, double, double)` | double | 到中心点距离平方 |
| `.withinDistance(IBlockPos, double)` | bool | 是否在指定距离内 |
| `.getX()` | int | 获取 X |
| `.getY()` | int | 获取 Y |
| `.getZ()` | int | 获取 Z |
| `.toLong()` | long | 转为 long |
| `.fromLong(long)` | IBlockPos | 从 long 转换 |
| `.asPosition3f` | IPosition3f | 转为 Position3f 对象 |
| `.getOffset(IFacing, int)` | IBlockPos | 获取指定方向偏移指定距离后的新位置 |

### IBlockAccess（方块访问接口）

> `import crafttweaker.world.IBlockAccess;`

IBlockAccess 是 IWorld 的父接口，所有 IWorld 对象都可以使用 IBlockAccess 的方法。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getBlockState(IBlockPos)` | IBlockState | 获取指定位置的方块状态 |
| `.isAirBlock(IBlockPos)` | bool | 检查指定位置是否为空气方块 |
| `.getStrongPower(IBlockPos, IFacing)` | int | 获取指定方块面的强红石信号 |

### IExplosion（爆炸）

> `import crafttweaker.world.IExplosion;`

IExplosion 代表一个爆炸对象，可以通过 IWorld 的 `createExplosion` 或 `performExplosion` 获取。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 爆炸所在的世界 |
| `placedBy` | IEntityLivingBase | 发起爆炸的实体（TNT 则为放置 TNT 的实体，可能为 null） |
| `position` | Position3f | 爆炸位置 |
| `affectedBlockPositions` | IBlockPos[] | 爆炸影响的方块位置列表（`doExplosionA()` 调用前可能为空） |
| `playerKnockbackMap` | Map\<IPlayer, IVector3d\> | 爆炸区域内玩家的击退映射 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.clearAffectedBlockPositions()` | void | 清除受影响方块位置列表 |
| `.onExplosionStart(IWorld)` | bool | 触发 ExplosionStart 事件，可用于在手动引爆前取消爆炸 |
| `.doExplosionA()` | void | 执行爆炸第一部分：实体伤害、击退、赋值 affectedBlockPositions |
| `.doExplosionB(bool)` | void | 执行爆炸第二部分：声音、粒子、方块破坏/掉落、火焰生成 |

### IFacing（方向）

> `import crafttweaker.world.IFacing;`

IFacing 代表一个方向（北、南、东、西、上、下）。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `IFacing.north()` | IFacing | 获取北方向 |
| `IFacing.east()` | IFacing | 获取东方向 |
| `IFacing.south()` | IFacing | 获取南方向 |
| `IFacing.west()` | IFacing | 获取西方向 |
| `IFacing.down()` | IFacing | 获取下方向 |
| `IFacing.up()` | IFacing | 获取上方向 |
| `IFacing.fromString(string)` | IFacing | 从字符串获取方向（如 "NORTH"） |
| `IFacing.getDirectionFromEntityLiving(IBlockPos, IEntityLivingBase)` | IFacing | 根据实体位置获取方向（常用于确定方块放置朝向，可返回 UP/DOWN） |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 方向名称 |
| `rotateY` | IFacing | 绕 Y 轴旋转后的方向 |
| `opposite` | IFacing | 反方向 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.compare(IFacing)` | int | 比较两个方向，相等返回 0 |

### IRayTraceResult（射线检测结果）

> `import crafttweaker.world.IRayTraceResult;`

IRayTraceResult 代表玩家视线或点击的射线检测结果。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `isMiss` | bool | 是否未命中 |
| `isBlock` | bool | 是否命中方块 |
| `blockPos` | IBlockPos | 命中的方块位置（非 bool 返回值可为 null） |
| `sideHit` | IFacing | 命中的方块面（非 bool 返回值可为 null） |

#### 已弃用 @ZenGetter

以下 getter 已弃用，因为当前没有可靠的方式同时射线检测方块和实体。

| 属性 | 类型 | 说明 |
|------|------|------|
| `isEntity` | bool | 是否命中实体（始终返回 `false`） |
| `entity` | IEntity | 命中的实体（始终返回 `null`） |

### IVector3d（三维向量）

> `import crafttweaker.world.IVector3d;`

IVector3d 是一个使用三个 double 表示方向的向量对象。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `IVector3d.create(double, double, double)` | IVector3d | 创建新的 IVector3d 对象 |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `x` | double | X 分量 |
| `y` | double | Y 分量 |
| `z` | double | Z 分量 |
| `normalized` | IVector3d | 归一化后的向量 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.dotProduct(IVector3d)` | double | 点积 |
| `.crossProduct(IVector3d)` | IVector3d | 叉积 |
| `.subtract(IVector3d)` | IVector3d | 向量减法 |
| `.subtractReverse(IVector3d)` | IVector3d | 反向减法（other - this） |
| `.add(IVector3d)` | IVector3d | 向量加法 |
| `.distanceTo(IVector3d)` | double | 到另一个向量的距离 |
| `.scale(double)` | IVector3d | 缩放向量 |

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

---

## ZenUtils 扩展（需安装 ZenUtils）

> `import mods.zenutils.*;`

### IWorld 扩展

对 `crafttweaker.world.IWorld` 的扩展，所有世界对象自动可用。

**注意**：以下玩家查询方法在找不到玩家时返回 **null**。

#### 玩家查询方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getPlayerByName(String name)` | IPlayer | 通过名称获取玩家 |
| `.getPlayerByUUID(CrTUUID uuid)` | IPlayer | 通过 UUID 获取玩家 |
| `.getAllPlayers()` | List\<IPlayer\> | 获取所有玩家 |
| `.getClosestPlayerToEntity(IEntity, double distance, boolean spectator)` | IPlayer | 获取离指定实体最近的玩家 |
| `.getClosestPlayer(double x, double y, double z, double distance, boolean spectator)` | IPlayer | 获取离指定坐标最近的玩家 |

#### 实体查询方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getEntities()` | List\<IEntity\> | 获取世界中所有实体 |
| `.getEntityItems()` | List\<IEntityItem\> | 获取世界中所有物品实体 |

#### 自定义世界数据

@since 1.4.4

不同维度有不同的数据。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getCustomWorldData()` | IData | 获取自定义世界数据（非空） |
| `.setCustomWorldData(IData)` | void | 设置自定义世界数据 |
| `.updateCustomWorldData(IData)` | void | 更新自定义世界数据 |

#### 自定义区块数据

IBlockPos 参数用于定位所在区块，获取的是该区块的数据而非方块位置的数据。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getCustomChunkData(IBlockPos)` | IData | 获取自定义区块数据（非空） |
| `.setCustomChunkData(IData, IBlockPos)` | void | 设置自定义区块数据 |
| `.updateCustomChunkData(IData, IBlockPos)` | void | 更新自定义区块数据 |

#### 其他方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getCustomTileEntity(IBlockPos)` | TileEntityInGame | 获取 ZenUtils 自定义方块实体，不存在返回 null |
| `.getLiquidHandler(IBlockPos, @Optional IFacing)` | LiquidHandler | 获取方块实体的流体处理器 |
| `.destroyBlock(IBlockPos, bool dropBlock)` | bool | 破坏方块（@since 1.5.2） |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `gameRuleHelper` | GameRuleHelper | 获取游戏规则管理器 |

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getGameRuleHelper()` | GameRuleHelper | 获取游戏规则管理器（方法形式） |

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

### CrTItemHandler（物品容器）

> `import mods.zenutils.ItemHandler;`

@since 1.6.3

物品容器操作，类似箱子或玩家背包。

#### 获取实例

| 方法 | 返回 | 说明 |
|------|------|------|
| `world.getItemHandler(IBlockPos, @Optional IFacing)` | ItemHandler | 从方块实体获取物品容器 |
| `player.getPlayerInventoryItemHandler()` | ItemHandler | 获取玩家背包容器 |
| `player.getPlayerBaubleItemHandler()` | ItemHandler | 获取玩家饰品栏容器（需安装 Baubles） |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `size` | int | 可用槽位数 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getStackInSlot(int)` | IItemStack | 获取指定槽位物品（可为 null） |
| `.setStackInSlot(int, IItemStack)` | bool | 设置指定槽位物品 |
| `.insertItem(int, IItemStack, bool simulate)` | IItemStack | 插入物品，返回剩余部分（全部接受返回 null） |
| `.extractItem(int, int amount, bool simulate)` | IItemStack | 提取物品 |
| `.getSlotLimit(int)` | int | 获取指定槽位最大堆叠数 |
| `.isItemValid(int, IItemStack)` | bool | 检查物品是否可插入该槽位 |

支持 for 循环遍历。

### CrTLiquidHandler（流体容器）

> `import mods.zenutils.LiquidHandler;`

@since 1.9.8

流体容器操作。

#### 获取实例

| 方法 | 返回 | 说明 |
|------|------|------|
| `world.getLiquidHandler(IBlockPos, @Optional IFacing)` | LiquidHandler | 从方块实体获取流体容器 |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `tankProperties` | List\<ILiquidTankProperties\> | 流体槽属性列表（只读） |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.drain(int maxDrain, bool doDrain)` | ILiquidStack | 排出流体（不区分流体类型） |
| `.drain(ILiquidStack resource, bool doDrain)` | ILiquidStack | 排出指定流体 |
| `.fill(ILiquidStack resource, bool doFill)` | int | 填充流体，返回实际填充量 |

### ILiquidTankProperties（流体槽属性）

> `import mods.zenutils.ILiquidTankProperties;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `contents` | ILiquidStack | 流体内容副本（可为 null） |
| `capacity` | int | 最大容量（mB） |
| `canFill` | bool | 是否可填充 |
| `canDrain` | bool | 是否可排出 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.canFillFluidType(ILiquidStack)` | bool | 是否可填充指定类型流体 |
| `.canDrainFluidType(ILiquidStack)` | bool | 是否可排出指定类型流体 |
