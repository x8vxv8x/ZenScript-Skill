# Magneticraft CraftTweaker API 参考

> Mod ID: `magneticraft`
> 前置条件: 无
> 导入: `import mods.magneticraft.<ClassName>;`

## API 列表

### CrushingTable（粉碎台）

> `import mods.magneticraft.CrushingTable;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output)` | void | 添加粉碎台配方 |
| `.removeRecipe(IItemStack input)` | void | 根据输入物品移除配方 |
| `.addHammer(IIngredient hammer, int miningLevel, int speed, int durabilityPerRecipe)` | void | 添加可用锤子 |
| `.removeHammer(IItemStack hammer)` | void | 移除可用锤子 |

### FluidFuel（流体燃料）

> `import mods.magneticraft.FluidFuel;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(ILiquidStack fuel, int burnTime, double powerPerCycle)` | void | 添加流体燃料 |
| `.removeFuel(ILiquidStack fuel)` | void | 移除流体燃料 |

### GasificationUnit（气化单元）

> `import mods.magneticraft.GasificationUnit;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output, ILiquidStack liquidOut, float ticks, float minTemperature)` | void | 添加气化单元配方 |
| `.removeRecipe(IItemStack input)` | void | 根据输入物品移除配方 |

### Grinder（研磨机）

> `import mods.magneticraft.Grinder;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output, IItemStack secondaryOutput, float probability, float ticks)` | void | 添加研磨机配方 |
| `.removeRecipe(IItemStack input)` | void | 根据输入物品移除配方 |

### HydraulicPress（液压机）

> `import mods.magneticraft.HydraulicPress;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output, float ticks, int mode)` | void | 添加液压机配方。mode: 0=轻型（标准板），1=中型（双层板），2=重型（重型板） |
| `.removeRecipe(IItemStack input, int mode)` | void | 根据输入物品和模式移除配方 |

### OilHeater（原油加热器）

> `import mods.magneticraft.OilHeater;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack input, ILiquidStack output, float ticks, int minTemperature)` | void | 添加原油加热器配方 |
| `.removeRecipe(ILiquidStack input)` | void | 根据输入流体移除配方 |

### Refinery（精炼厂）

> `import mods.magneticraft.Refinery;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack input, ILiquidStack output1, ILiquidStack output2, ILiquidStack output3, float ticks)` | void | 添加精炼厂配方（1 输入，3 输出） |
| `.removeRecipe(ILiquidStack input)` | void | 根据输入流体移除配方 |

### Sieve（电动滤筛台）

> `import mods.magneticraft.Sieve;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output1, float output1Probability, IItemStack output2, float output2Probability, IItemStack output3, float output3Probability, float ticks)` | void | 添加配方（3 个输出，各自有概率） |
| `.removeRecipe(IItemStack input)` | void | 根据输入物品移除配方 |

### SluiceBox（洗矿槽）

> `import mods.magneticraft.SluiceBox;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, float prob1, IItemStack output1)` | void | 添加洗矿槽配方（1 个输出） |
| `.addRecipe(IIngredient input, float prob1, IItemStack output1, float prob2, IItemStack output2)` | void | 添加洗矿槽配方（2 个输出） |
| `.addRecipe(IIngredient input, float prob1, IItemStack output1, float prob2, IItemStack output2, float prob3, IItemStack output3)` | void | 添加洗矿槽配方（3 个输出） |
| `.addRecipe(IIngredient input, float prob1, IItemStack output1, float prob2, IItemStack output2, float prob3, IItemStack output3, float prob4, IItemStack output4)` | void | 添加洗矿槽配方（4 个输出） |
| `.addRecipe(IIngredient input, float prob1, IItemStack output1, float prob2, IItemStack output2, float prob3, IItemStack output3, float prob4, IItemStack output4, float prob5, IItemStack output5)` | void | 添加洗矿槽配方（5 个输出） |
| `.addRecipe(IIngredient input, float prob1, IItemStack output1, float prob2, IItemStack output2, float prob3, IItemStack output3, float prob4, IItemStack output4, float prob5, IItemStack output5, float prob6, IItemStack output6)` | void | 添加洗矿槽配方（6 个输出） |
| `.removeRecipe(IItemStack input)` | void | 根据输入物品移除配方 |

### Thermopile（温差电堆）

> `import mods.magneticraft.Thermopile;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack input, float temperature, float conductivity)` | void | 添加配方（物品输入） |
| `.addRecipe(IBlockState block, float temperature, float conductivity)` | void | 添加配方（方块状态输入） |
| `.removeRecipe(IItemStack input)` | void | 根据输入物品移除配方 |

### Wrench（扳手）

> `import mods.magneticraft.Wrench;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient wrench)` | void | 添加可用扳手 |
| `.removeWrench(IItemStack wrench)` | void | 移除可用扳手 |
