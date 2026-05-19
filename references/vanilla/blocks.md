# Blocks CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.block.IBlock;`、`import crafttweaker.block.IBlockState;`、`import crafttweaker.block.IBlockDefinition;`、`import crafttweaker.block.IBlockPattern;`、`import crafttweaker.block.IBlockProperties;`、`import crafttweaker.block.IBlockStateMatcher;`、`import crafttweaker.block.IMaterial;`、`import crafttweaker.block.IMobilityFlag;`

方块系统 API，用于操作方块、方块状态和方块定义。

---

## API 列表

### IBlock（方块）

> `import crafttweaker.block.IBlock;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `definition` | IBlockDefinition | 方块定义 |
| `meta` | int | Meta 值 |
| `state` | IBlockState | 方块状态 |
| `id` | int | 方块 ID |
| `name` | string | 方块名称 |
| `displayName` | string | 显示名称 |
| `commandString` | string | 命令字符串 |
| `harvestLevel` | int | 挖掘等级 |
| `harvestTool` | string | 挖掘工具 |
| `hardness` | float | 硬度 |
| `resistance` | float | 爆炸抗性 |
| `opacity` | float | 不透明度 |
| `lightValue` | int | 亮度 |
| `lightOpacity` | int | 光照不透明度 |
| `isFullBlock` | bool | 是否完整方块 |
| `isFullCube` | bool | 是否完整立方体 |
| `isNormalCube` | bool | 是否普通方块 |
| `isOpaque` | bool | 是否不透明 |
| `isReplaceable` | bool | 是否可替换 |
| `isAir` | bool | 是否空气 |
| `isFlammable` | bool | 是否可燃 |
| `isFireSource` | bool | 是否火源 |
| `isCollidable` | bool | 是否可碰撞 |
| `hasTileEntity` | bool | 是否有 Tile Entity |
| `tickRandomly` | bool | 是否随机 tick |
| `creativeTab` | string | 创造模式标签页 |
| `material` | string | 材料 |
| `slipperiness` | float | 滑度 |
| `data` | IData | 方块的 TileData（仅通过 `IWorld.getBlock()` 获取时非空） |
| `fluid` | ILiquidDefinition | 方块的流体 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getStateFromMeta(int)` | IBlockState | 从 Meta 获取状态 |
| `.getMetaFromState(IBlockState)` | int | 从状态获取 Meta |
| `.canProvidePower(IBlockState)` | bool | 是否可提供红石信号 |
| `.getWeakPower(IBlockState, IBlockAccess, IBlockPos, EnumFacing)` | int | 获取弱红石信号 |
| `.getStrongPower(IBlockState, IBlockAccess, IBlockPos, EnumFacing)` | int | 获取强红石信号 |
| `.getComparatorInputOverride(IBlockState, IWorld, IBlockPos)` | int | 获取比较器输入 |
| `.getCollisionBoundingBox(IBlockState, IBlockAccess, IBlockPos)` | IAxisAlignedBB | 获取碰撞箱 |
| `.getSelectedBoundingBox(IBlockState, IWorld, IBlockPos)` | IAxisAlignedBB | 获取选择箱 |
| `.getActualState(IBlockState, IBlockAccess, IBlockPos)` | IBlockState | 获取实际状态 |
| `.getExtendedState(IBlockState, IBlockAccess, IBlockPos)` | IBlockState | 获取扩展状态 |
| `.getDrops(IWorld, IBlockPos, IBlockState, int)` | List | 获取掉落物 |
| `.getItem(IWorld, IBlockPos, IBlockState)` | IItemStack | 获取物品 |
| `.quantityDropped(IRandom)` | int | 掉落数量 |
| `.getPickBlock(IBlockState, IRayTraceResult, IWorld, IBlockPos, IEntityPlayer)` | IItemStack | 获取拾取物品 |
| `.getExplosionResistance(IEntity)` | float | 获取爆炸抗性 |
| `.getEnchantPowerBonus(IWorld, IBlockPos)` | float | 获取附魔台加成 |
| `.getFireSpreadSpeed(IWorld, IBlockPos, EnumFacing)` | int | 获取火焰传播速度 |
| `.getFlammability(IWorld, IBlockPos, EnumFacing)` | int | 获取可燃性 |
| `.getLightValue(IBlockState)` | int | 获取亮度 |
| `.getAmbientOcclusionLightValue(IBlockState)` | float | 获取环境光遮蔽值 |
| `.shouldSideBeRendered(IBlockState, IBlockAccess, IBlockPos, EnumFacing)` | bool | 是否应渲染面 |
| `.isPassable(IWorld, IBlockPos)` | bool | 是否可通过 |
| `.isToolEffective(string, IBlockState)` | bool | 工具是否有效 |

### IBlockState（方块状态）

> `import crafttweaker.block.IBlockState;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `block` | IBlock | 方块 |
| `meta` | int | Meta 值 |
| `id` | int | 方块 ID |
| `name` | string | 方块名称 |
| `displayName` | string | 显示名称 |
| `commandString` | string | 命令字符串 |
| `isNormalCube` | bool | 是否普通方块 |
| `isOpaque` | bool | 是否不透明 |
| `isFullCube` | bool | 是否完整立方体 |
| `isFullBlock` | bool | 是否完整方块 |
| `hasCustomBreakingProgress` | bool | 是否有自定义破坏进度 |
| `isReplaceable` | bool | 是否可替换 |
| `isAir` | bool | 是否空气 |
| `isCollidable` | bool | 是否可碰撞 |
| `isBlockNormalCube` | bool | 是否普通方块 |
| `doesSideBlockRendering` | bool | 是否渲染面 |
| `renderType` | int | 渲染类型 |
| `weakPower` | int | 弱红石信号 |
| `strongPower` | int | 强红石信号 |
| `canProvidePower` | bool | 是否可提供红石信号 |
| `getLightValue` | int | 亮度 |
| `getComparatorInputOverride` | int | 比较器输入 |

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `IBlockState.getBlockState(string, string...)` | IBlockState | 运行时解析 IBlockState。第一个参数为 "modid:blockname"，后续为 "property=value" 对。未指定的属性使用默认值 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getPropertyNames()` | List\<string\> | 获取所有属性名 |
| `.getPropertyValue(string)` | string | 获取指定属性的值 |
| `.getAllowedValuesForProperty(string)` | List\<string\> | 获取指定属性的所有允许值 |
| `.withProperty(string, string)` | IBlockState | 创建新 IBlockState 并设置指定属性值 |
| `.getProperties()` | Map | 获取所有属性 |
| `.getValue(IProperty)` | IPropertyValue | 获取属性值 |
| `.withProperty(IProperty, IPropertyValue)` | IBlockState | 设置属性值 |
| `.cycleProperty(IProperty)` | IBlockState | 循环属性值 |
| `.isReplaceable(IWorld, IBlockPos)` | bool | 检查方块是否可替换 |
| `.getActualState(IBlockAccess, IBlockPos)` | IBlockState | 获取实际状态 |
| `.getBoundingBox(IBlockAccess, IBlockPos)` | IAxisAlignedBB | 获取碰撞箱 |
| `.addCollisionBoxToList(IWorld, IBlockPos, IAxisAlignedBB, List, IEntity, bool)` | void | 添加碰撞箱 |
| `.getDrops(IWorld, IBlockPos, int)` | List | 获取掉落物 |
| `.getPlayerRelativeBlockHardness(IPlayer, IWorld, IBlockPos)` | float | 获取相对破坏速度 |
| `.getEnchantPowerBonus(IWorld, IBlockPos)` | float | 获取附魔台加成 |
| `.getExplosionResistance(IEntity)` | float | 获取爆炸抗性 |
| `.getAmbientOcclusionLightValue()` | float | 获取环境光遮蔽值 |
| `.getLightValue(IWorld, IBlockPos)` | int | 获取亮度 |
| `.getWeakPower(IBlockAccess, IBlockPos, EnumFacing)` | int | 获取弱红石信号 |
| `.getStrongPower(IBlockAccess, IBlockPos, EnumFacing)` | int | 获取强红石信号 |
| `.canProvidePower()` | bool | 是否可提供红石信号 |
| `.isNormalCube()` | bool | 是否普通方块 |
| `.isOpaque()` | bool | 是否不透明 |
| `.isFullCube()` | bool | 是否完整立方体 |
| `.isFullBlock()` | bool | 是否完整方块 |
| `.hasCustomBreakingProgress()` | bool | 是否有自定义破坏进度 |
| `.isReplaceable()` | bool | 是否可替换 |
| `.isAir()` | bool | 是否空气 |
| `.isCollidable()` | bool | 是否可碰撞 |
| `.doesSideBlockRendering()` | bool | 是否渲染面 |
| `.shouldSideBeRendered(IBlockAccess, IBlockPos, EnumFacing)` | bool | 是否应渲染面 |
| `.getCollisionBoundingBox(IWorld, IBlockPos)` | IAxisAlignedBB | 获取碰撞箱 |
| `.getSelectedBoundingBox(IWorld, IBlockPos)` | IAxisAlignedBB | 获取选择箱 |
| `.compare(IBlockState)` | int | 比较两个状态，相等返回 0（也可使用 `==` `!=`） |
| `.matchBlock()` | IBlockStateMatcher | 获取匹配此方块所有状态的 IBlockStateMatcher |

### IBlockDefinition（方块定义）

> `import crafttweaker.block.IBlockDefinition;`

IBlockDefinition 提供方块的额外信息，可通过 `block.definition` 获取，或通过 `game.blocks` 获取所有方块定义列表。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `id` | string | 方块 ID（只读） |
| `name` | string | 方块名称（只读） |
| `displayName` | string | 显示名称（只读） |
| `commandString` | string | 命令字符串（只读） |
| `unlocalizedName` | string | 未本地化名称（只读） |
| `creativeTab` | ICreativeTab | 创造模式标签页（只读） |
| `defaultState` | IBlockState | 默认方块状态（只读） |
| `harvestLevel` | int | 挖掘等级（可读写） |
| `harvestTool` | string | 挖掘工具（可读写） |
| `hardness` | int | 硬度（可读写） |
| `resistance` | int | 爆炸抗性（可读写） |
| `lightLevel` | int | 亮度（可读写） |
| `lightOpacity` | int | 光照不透明度（可读写） |
| `tickRandomly` | bool | 是否随机 tick（可读写） |
| `canSpawnInBlock` | bool | 实体是否可在此方块内生成（只读） |
| `defaultSlipperiness` | float | 默认滑度（可读写） |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.makeStack(int)` | IItemStack | 创建物品堆叠 |
| `.setHarvestLevel(string, int, @Optional IBlockState)` | void | 设置挖掘等级。省略 IBlockState 则设置所有状态 |
| `.getHarvestLevel(IBlockState)` | int | 获取指定状态的挖掘等级 |
| `.getHarvestTool(IBlockState)` | string | 获取指定状态的挖掘工具 |
| `.getTickRate(IWorld)` | int | 获取指定世界的 tick 速率 |
| `.canPlaceBlockOnSide(IWorld, IBlockPos, IFacing)` | bool | 检查方块是否可以在指定面放置 |
| `.canPlaceBlockAt(IWorld, IBlockPos)` | bool | 检查方块是否可以在指定位置放置 |
| `.getSlipperiness(IBlockState, IBlockAccess, IBlockPos, @Optional IEntity)` | float | 获取方块滑度 |
| `.getLightOpacity(IBlockState)` | float | 获取指定状态的光照不透明度 |
| `.getLightOpacity(IBlockState, IWorld, IBlockPos)` | float | 获取指定位置的光照不透明度 |
| `.getLightLevel(IBlockState)` | float | 获取指定状态的亮度 |
| `.getLightLevel(IBlockState, IWorld, IBlockPos)` | float | 获取指定位置的亮度 |
| `.getResistance(IWorld, IBlockPos, IEntity, IExplosion)` | float | 获取指定位置和爆炸的爆炸抗性 |
| `.getStateFromMeta(int)` | IBlockState | 从 Meta 获取方块状态 |
| `.isToolEffective(string, IBlockState)` | bool | 检查工具是否对指定状态有效 |
| `.setUnbreakable()` | void | 设置不可破坏（等同于 `hardness = -1`） |
| `.setCreativeTab(string)` | void | 设置创造模式标签页 |
| `.setTickRandomly(bool)` | void | 设置随机 tick |
| `.setHardness(int)` | void | 设置硬度 |
| `.setResistance(int)` | void | 设置爆炸抗性 |
| `.setLightLevel(int)` | void | 设置亮度 |
| `.setLightOpacity(int)` | void | 设置光照不透明度 |
| `.setHarvestLevel(string, int)` | void | 设置挖掘等级 |
| `.setToolHarvest(string, int)` | void | 设置工具挖掘等级 |
| `.setSoundType(string)` | void | 设置声音类型 |
| `.setFlammability(int)` | void | 设置可燃性 |
| `.setFireSpreadSpeed(int)` | void | 设置火焰传播速度 |
| `.setFireSource(bool)` | void | 设置火源 |
| `.setFullBlock(bool)` | void | 设置完整方块 |
| `.setFullCube(bool)` | void | 设置完整立方体 |
| `.setNormalCube(bool)` | void | 设置普通方块 |
| `.setOpaque(bool)` | void | 设置不透明 |
| `.setReplaceable(bool)` | void | 设置可替换 |
| `.setAir(bool)` | void | 设置空气 |
| `.setCollidable(bool)` | void | 设置可碰撞 |
| `.addDrop(IItemStack)` | void | 添加掉落物 |
| `.addDrop(IItemStack, int, int)` | void | 添加掉落物（数量范围） |
| `.removeDrop(IItemStack)` | void | 移除掉落物 |
| `.clearDrops()` | void | 清除所有掉落 |

### IBlockPattern（方块模式）

> `import crafttweaker.block.IBlockPattern;`

IBlockPattern 是一个将多个方块组合为一个对象的接口，类似于 IIngredient 之于 IItemStack。IBlock 继承 IBlockPattern。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `blocks` | List\<IBlock\> | 列出此对象的所有可能方块 |
| `displayName` | string | 返回匹配方块的显示名称 |

#### 操作

- 可以使用 `|` 运算符合并两个 IBlockPattern
- 可以使用 `in` 关键字检查一个方块是否在 IBlockPattern 中

### IBlockProperties（方块属性接口）

> `import crafttweaker.block.IBlockProperties;`

IBlockProperties 是 IBlockState 的父接口，所有 IBlockState 的方法也适用于 IBlockProperties。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `canProvidePower` | bool | 是否可提供红石信号 |
| `mobilityFlag` | string | 移动标志 |
| `material` | IMaterial | 方块材质 |
| `causesSuffocation` | bool | 是否会导致窒息 |
| `hasCustomBreakingProgress` | bool | 是否有自定义破坏进度 |
| `blockNormalCube` | bool | 是否普通方块 |
| `fullBlock` | bool | 是否完整方块 |
| `fullCube` | bool | 是否完整立方体 |
| `normalCube` | bool | 是否普通方块 |
| `opaqueCube` | bool | 是否不透明立方体 |
| `translucent` | bool | 是否半透明 |
| `useNeighborBrightness` | bool | 是否使用邻居亮度 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.isReplaceable(IWorld, IBlockPos)` | bool | 检查方块是否可替换 |
| `.getLightValue(IWorld, IBlockPos)` | int | 获取指定位置的光照值 |
| `.getWeakPower(IBlockAccess, IBlockPos, IFacing)` | int | 获取弱红石信号 |
| `.getStrongPower(IBlockAccess, IBlockPos, IFacing)` | int | 获取强红石信号 |
| `.getComparatorInputOverride(IWorld, IBlockPos)` | int | 获取比较器输入覆盖 |
| `.canEntitySpawn(IEntity)` | bool | 检查实体是否可以在此方块上生成 |
| `.getActualState(IBlockAccess, IBlockPos)` | IBlockProperties | 获取实际方块属性 |
| `.getBlockHardness(IWorld, IBlockPos)` | float | 获取方块硬度 |
| `.getLightOpacy(IWorld, IBlockPos)` | int | 获取光照不透明度 |
| `.getPlayerRelativeBlockHardness(IPlayer, IWorld, IBlockPos)` | float | 获取玩家相对破坏速度 |
| `.isSideSolid(IBlockAccess, IBlockPos, IFacing)` | bool | 检查方块面是否为实体面 |

### IBlockStateMatcher（方块状态匹配器）

> `import crafttweaker.block.IBlockStateMatcher;`

IBlockStateMatcher 用于匹配 IBlockState 对象的一组要求。每个 IBlockState 也是 IBlockStateMatcher（只匹配自身）。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `IBlockStateMatcher.create(IBlockState...)` | IBlockStateMatcher | 创建匹配器。零个参数则永不匹配；一个参数则匹配该方块的任意属性值；多个参数等同于 OR 合并 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.matches(IBlockState)` | bool | 检查方块状态是否匹配（也可用 `has` 运算符） |
| `.withMatchedValuesForProperty(string, string...)` | IBlockStateMatcher | 添加属性匹配要求（仅非复合匹配器可用） |
| `.getMatchedValuesForProperty(string)` | List\<string\> | 获取指定属性的匹配值（仅非复合匹配器可用） |
| `.getMatchedProperties()` | Map\<string, List\<string\>\> | 获取所有匹配属性（仅非复合匹配器可用） |
| `.getMatchingBlockStates()` | Collection\<IBlockState\> | 获取所有匹配的方块状态集合 |
| `.isCompound()` | bool | 检查是否为复合匹配器 |
| `commandString` | string | 获取命令字符串表示 |

#### 操作

- 可以使用 `|` 运算符合并两个 IBlockStateMatcher 得到复合匹配器
- 复合匹配器不绑定特定方块，不能使用 `withMatchedValuesForProperty`

### IMaterial（方块材质）

> `import crafttweaker.block.IMaterial;`

IMaterial 代表方块的材质。

#### 静态方法（获取原版材质）

| 方法 | 返回 | 说明 |
|------|------|------|
| `IMaterial.air()` | IMaterial | 空气 |
| `IMaterial.anvil()` | IMaterial | 铁砧 |
| `IMaterial.barrier()` | IMaterial | 屏障 |
| `IMaterial.cactus()` | IMaterial | 仙人掌 |
| `IMaterial.cake()` | IMaterial | 蛋糕 |
| `IMaterial.carpet()` | IMaterial | 地毯 |
| `IMaterial.circuits()` | IMaterial | 红石线路 |
| `IMaterial.clay()` | IMaterial | 粘土 |
| `IMaterial.cloth()` | IMaterial | 布 |
| `IMaterial.coral()` | IMaterial | 珊瑚 |
| `IMaterial.craftedSnow()` | IMaterial | 雪块 |
| `IMaterial.dragonEgg()` | IMaterial | 龙蛋 |
| `IMaterial.fire()` | IMaterial | 火 |
| `IMaterial.glass()` | IMaterial | 玻璃 |
| `IMaterial.gourd()` | IMaterial | 葫芦 |
| `IMaterial.grass()` | IMaterial | 草 |
| `IMaterial.ground()` | IMaterial | 泥土 |
| `IMaterial.ice()` | IMaterial | 冰 |
| `IMaterial.iron()` | IMaterial | 铁 |
| `IMaterial.lava()` | IMaterial | 岩浆 |
| `IMaterial.leaves()` | IMaterial | 树叶 |
| `IMaterial.packedIce()` | IMaterial | 浮冰 |
| `IMaterial.piston()` | IMaterial | 活塞 |
| `IMaterial.plants()` | IMaterial | 植物 |
| `IMaterial.portal()` | IMaterial | 传送门 |
| `IMaterial.redstoneLight()` | IMaterial | 红石灯 |
| `IMaterial.rock()` | IMaterial | 石头 |
| `IMaterial.sand()` | IMaterial | 沙子 |
| `IMaterial.snow()` | IMaterial | 雪 |
| `IMaterial.sponge()` | IMaterial | 海绵 |
| `IMaterial.structureVoid()` | IMaterial | 结构空位 |
| `IMaterial.tnt()` | IMaterial | TNT |
| `IMaterial.vine()` | IMaterial | 藤蔓 |
| `IMaterial.water()` | IMaterial | 水 |
| `IMaterial.web()` | IMaterial | 蛛网 |
| `IMaterial.wood()` | IMaterial | 木头 |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `blocksLight` | bool | 是否阻挡光线 |
| `blocksMovement` | bool | 是否阻挡移动 |
| `canBurn` | bool | 是否可燃 |
| `mobilityFlag` | string | 移动标志 |
| `liquid` | bool | 是否液体 |
| `opaque` | bool | 是否不透明 |
| `replaceable` | bool | 是否可替换 |
| `solid` | bool | 是否固体 |
| `toolNotRequired` | bool | 是否不需要工具 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setReplaceable()` | IMaterial | 设置为可替换材质 |
| `.matches(IMaterial)` | bool | 检查两个材质是否相同 |

### IMobilityFlag（移动标志）

> `import crafttweaker.block.IMobilityFlag;`

IMobilityFlag 代表方块的移动标志（如活塞推动行为）。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.normal()` | IMobilityFlag | 正常 |
| `.destroy()` | IMobilityFlag | 被破坏 |
| `.block()` | IMobilityFlag | 阻挡 |
| `.ignore()` | IMobilityFlag | 忽略 |
| `.pushOnly()` | IMobilityFlag | 仅推 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.matches(IMobilityFlag)` | bool | 检查两个移动标志是否相同 |

---

## ContentTweaker 扩展（需安装 ContentTweaker）

> `import mods.contenttweaker.VanillaFactory;`
> `import mods.contenttweaker.Block;`

CoT 脚本第一行必须为 `#loader contenttweaker`。

### VanillaFactory 方块方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createBlock(string id, BlockMaterial)` | Block | 创建自定义方块 |

### Block（自定义方块）

> `import mods.contenttweaker.Block;`

| ZenProperty | 类型 | 默认值 | 说明 |
|-------------|------|--------|------|
| `blockHardness` | float | 5.0 | 方块硬度 |
| `blockResistance` | float | 5.0 | 防爆等级 |
| `blockSoundType` | SoundType | `<soundtype:metal>` | 方块声音 |
| `creativeTab` | ICreativeTab | 杂项 | 所在创造标签 |
| `lightValue` | int | 0 | 光照等级（最大 15） |
| `lightOpacity` | int | 255/0 | 不透明度 |
| `fullBlock` | bool | true | 是否完整方块 |
| `translucent` | bool | false | 是否半透明 |
| `blockLayer` | string | "SOLID" | 渲染层: "SOLID"/"CUTOUT_MIPPED"/"CUTOUT"/"TRANSLUCENT" |
| `gravity` | bool | false | 是否受重力影响 |
| `slipperiness` | float | 0.6 | 滑度（冰为 0.98） |
| `toolClass` | string | "pickaxe" | 需要的挖掘工具 |
| `toolLevel` | int | 2 | 需要的挖掘等级 |
| `entitySpawnable` | bool | true | 生物是否可在此方块上生成 |
| `witherProof` | bool | false | 是否抵御凋灵爆炸 |
| `beaconBase` | bool | false | 是否可作为信标基座 |
| `replaceable` | bool | 取决于材质 | 是否可直接替换 |
| `passable` | bool | 取决于材质 | 玩家是否可通过 |
| `dropHandler` | IBlockDropHandler | null | 自定义掉落物函数 |

| 方法 | 返回 | 说明 |
|------|------|------|
| `.register()` | void | 注册方块进游戏 |

### ContentTweaker 方块示例

```zenscript
#loader contenttweaker
import mods.contenttweaker.VanillaFactory;
import mods.contenttweaker.Block;

var antiIceBlock as Block = VanillaFactory.createBlock("anti_ice", <blockmaterial:ice>);
antiIceBlock.lightOpacity = 3;
antiIceBlock.blockHardness = 1.0;
antiIceBlock.blockResistance = 5.0;
antiIceBlock.toolClass = "pickaxe";
antiIceBlock.toolLevel = 0;
antiIceBlock.blockSoundType = <soundtype:snow>;
antiIceBlock.slipperiness = 0.75;
antiIceBlock.register();
```

---

## ZenUtils 扩展（需安装 ZenUtils + ContentTweaker）

> `import mods.zenutils.cotx.*;`

该部分是对 ContentTweaker 方块系统的扩展。(见上方ContentTweaker 扩展)

### VanillaFactory 方块扩展方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `VanillaFactory.createExpandBlock(String, IBlockMaterialDefinition)` | ExpandBlock | 创建扩展方块 |

### ExpandBlock（扩展方块）

> `import mods.zenutils.cotx.Block;`

继承 ContentTweaker 的 `BlockRepresentation`。

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `onBlockActivated` | IBlockActivated | null | 方块右键交互回调 |
| `onEntityWalk` | IEntityWalk | null | 实体踩踏回调 |
| `onEntityCollidedWithBlock` | IEntityCollided | null | 实体碰撞回调 |
| `tileEntity` | TileEntity | null | 关联的方块实体 |

#### IBlockActivated（函数式接口）

> `import mods.zenutils.cotx.IBlockActivated;`

| 参数 | 类型 |
|------|------|
| world | IWorld |
| pos | IBlockPos |
| state | ICTBlockState |
| player | ICTPlayer |
| hand | Hand |
| facing | Facing |
| blockHit | Position3f |

返回 `bool`。

#### IEntityWalk（函数式接口）

> `import mods.zenutils.cotx.IEntityWalk;`

参数：`IWorld`, `IBlockPos`, `IEntity`。返回 void。

#### IEntityCollided（函数式接口）

> `import mods.zenutils.cotx.IEntityCollided;`

参数：`IWorld`, `IBlockPos`, `ICTBlockState`, `IEntity`。返回 void。

### LateSetCoTFunction 方块部分

| Bracket | 返回 | 说明 |
|------|------|------|
| `<cotBlock:name>` | IBlockRepresentation | 获取 ContentTweaker 方块 |

| 方法 | 返回 | 说明 |
|------|------|------|
| `VanillaFactory.putTileEntityTickFunction(int, ITileEntityTick)` | void | 注册方块实体 tick 函数（可重载） |
