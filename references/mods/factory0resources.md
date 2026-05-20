# Factory0 Resources CraftTweaker API 参考

> Mod ID: `factory0resources`
> 前置条件: Roids-Tweaker
> 导入: 见各章节

## API 列表

### ChunkData

> `import mods.roidtweaker.f0resources.ChunkData;`

包含给定区块的所有矿石和流体条目。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create()` | ChunkData | 创建空 ChunkData（用于无数据的区块） |

#### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.addData(OreData 或 FluidData data)` | data | void | 添加矿脉 |
| `.getDataOre(int index)` | index | OreData | 获取指定索引的矿石矿脉 |
| `.getDataFluid(int index)` | index | FluidData | 获取指定索引的流体矿脉 |
| `.removeData(OreData 或 FluidData data)` | data | void | 移除指定矿脉 |

### FluidData

> `import mods.roidtweaker.f0resources.FluidData;`

流体矿脉。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(ILiquidStack fluid, long amount)` | FluidData | 创建流体矿脉 |

#### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getStack(int amount)` | amount | ILiquidStack | 获取流体 |
| `.getAmount()` | 无 | long | 获取剩余量 |
| `.setAmount(long amount)` | amount | void | 设置剩余量 |
| `.mine(long quantity)` | quantity | ILiquidStack | 开采指定数量，返回开采的流体 |

### OreData

> `import mods.roidtweaker.f0resources.OreData;`

矿石矿脉。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(IItemStack ore, long amount)` | OreData | 创建矿石矿脉 |

#### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getStack(int amount)` | amount | IItemStack | 获取物品 |
| `.getAmount()` | 无 | long | 获取剩余量 |
| `.setAmount(long amount)` | amount | void | 设置剩余量 |
| `.mine(long quantity)` | quantity | IItemStack | 开采指定数量，返回开采的物品 |
| `.getRequiredTier()` | 无 | int | 获取所需采矿等级 |
| `.setRequiredTier(int tier)` | tier | void | 设置所需采矿等级 |
