# Railcraft CraftTweaker API 参考

> Mod ID: `railcraft`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.railcraft.*;`

## API 列表

### BlastFurnace（高炉）

> `import moretweaker.railcraft.BlastFurnace;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IIngredient input, optional int ticks, optional int slag)` | void | 添加高炉配方。`ticks` 为加工时间，`slag` 为矿渣产出 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### CokeOven（焦炉）

> `import moretweaker.railcraft.CokeOven;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IIngredient input, ILiquidStack liquidOutput, optional int ticks)` | void | 添加焦炉配方。同时输出物品和流体，`ticks` 为加工时间 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### RockCrusher（碎石机）

> `import moretweaker.railcraft.RockCrusher;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IIngredient input, IItemStack[] outputs, float[] chances, optional int ticks)` | void | 添加碎石配方。`outputs` 为输出物品数组，`chances` 为每个输出的概率数组，`ticks` 为加工时间 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### RollingMachine（辊压机）

> `import moretweaker.railcraft.RollingMachine;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addShaped(IItemStack output, IIngredient[][] inputs, optional int ticks)` | void | 添加有序配方。`ticks` 为加工时间 |
| `.addShapeless(IItemStack output, IIngredient[] inputs, optional int ticks)` | void | 添加无序配方。`ticks` 为加工时间 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### FluidFuels（流体燃料）

> `import moretweaker.railcraft.FluidFuels;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(ILiquidStack fuel, optional int heatPerBucket)` | void | 添加流体燃料。`heatPerBucket` 为每桶热量 |
| `.remove(ILiquidStack fuel)` | void | 移除流体燃料 |
| `.removeAll()` | void | 移除所有流体燃料 |
