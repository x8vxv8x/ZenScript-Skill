# Steam Age Revolution CraftTweaker API 参考

> Mod ID: `steamagerevolution`
> 前置条件: 无
> 导入: `import mods.steamagerevolution.<ClassName>;`

## API 列表

### AlloyForge (合金锻造炉)

> `import mods.steamagerevolution.AlloyForge;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack input, ILiquidStack input, ILiquidStack output, int craftTime)` | void | 添加合金锻造配方，craftTime 为合成时间 |
| `.removeRecipe(ILiquidStack output)` | void | 移除指定输出的合金锻造配方 |
| `.removeAll()` | void | 移除所有合金锻造配方 |

### CastingBlock (铸造台)

> `import mods.steamagerevolution.CastingBlock;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack input, IItemStack output, int craftTime)` | void | 添加铸造配方，craftTime 为合成时间 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的铸造配方 |
| `.removeAll()` | void | 移除所有铸造配方 |

### Crucible (坩埚)

> `import mods.steamagerevolution.Crucible;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, ILiquidStack output, int craftTime, int steamCost)` | void | 添加坩埚配方，craftTime 为合成时间，steamCost 为蒸汽消耗 |
| `.removeRecipe(ILiquidStack output)` | void | 移除指定输出的坩埚配方 |
| `.removeAll()` | void | 移除所有坩埚配方 |

### Distiller (蒸馏器)

> `import mods.steamagerevolution.Distiller;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack input, IItemStack outputStack, ILiquidStack output, int craftTime, int steamCost)` | void | 添加蒸馏配方，craftTime 为合成时间，steamCost 为蒸汽消耗 |
| `.removeRecipe(IItemStack outputStack, ILiquidStack output)` | void | 移除指定输出的蒸馏配方 |
| `.removeAll()` | void | 移除所有蒸馏配方 |

### Grinder (研磨机)

> `import mods.steamagerevolution.Grinder;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output, int craftTime, int steamCost)` | void | 添加研磨配方，craftTime 为合成时间，steamCost 为蒸汽消耗 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的研磨配方 |
| `.removeAll()` | void | 移除所有研磨配方 |

### SteamFurnace (蒸汽熔炉)

> `import mods.steamagerevolution.SteamFurnace;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output, int craftTime, int steamCost)` | void | 添加蒸汽熔炉配方，craftTime 为合成时间，steamCost 为蒸汽消耗 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的蒸汽熔炉配方 |
| `.removeAll()` | void | 移除所有蒸汽熔炉配方 |

### SteamHammer (蒸汽锤)

> `import mods.steamagerevolution.SteamHammer;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IIngredient input, IItemStack output, int craftTime, int steamCost)` | void | 添加蒸汽锤配方，craftTime 为合成时间，steamCost 为蒸汽消耗 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的蒸汽锤配方 |
| `.removeAll()` | void | 移除所有蒸汽锤配方 |

### Steelworks (炼钢厂)

> `import mods.steamagerevolution.Steelworks;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack input, IIngredient input2, IItemStack output, int craftTime, int steamCost)` | void | 添加炼钢配方，craftTime 为合成时间，steamCost 为蒸汽消耗 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的炼钢配方 |
| `.removeAll()` | void | 移除所有炼钢配方 |

### Vat (大桶)

> `import mods.steamagerevolution.Vat;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack[] input, IIngredient[] inputItems, ILiquidStack output, int craftTime)` | void | 添加大桶配方，craftTime 为合成时间 |
| `.removeRecipe(ILiquidStack output)` | void | 移除指定输出的大桶配方 |
| `.removeAll()` | void | 移除所有大桶配方 |
