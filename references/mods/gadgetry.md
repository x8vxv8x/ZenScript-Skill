# Gadgetry CraftTweaker API 参考

> Mod ID: `gadgetry`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.gadgetry.*;`

## API 列表

### AlloyFurnace（合金炉）

> `import moretweaker.gadgetry.AlloyFurnace;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IIngredient[] inputs)` | void | 添加合金配方 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### CombustionGenerator（燃烧发电机）

> `import moretweaker.gadgetry.CombustionGenerator;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(ILiquidStack liquid, int energyPerMb)` | void | 添加燃料。`energyPerMb` 为每毫桶能量产出 |
| `.remove(ILiquidStack liquid)` | void | 移除燃料 |
| `.removeAll()` | void | 移除所有燃料 |

### Distillery（蒸馏器）

> `import moretweaker.gadgetry.Distillery;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, ILiquidStack fluidOutput, IIngredient input, ILiquidStack fluidInput)` | void | 添加蒸馏配方。同时输出物品和流体 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### Grinder（研磨器）

> `import moretweaker.gadgetry.Grinder;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IIngredient input)` | void | 添加研磨配方 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |
