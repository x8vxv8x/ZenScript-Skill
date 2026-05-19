# Forestry CraftTweaker API 参考

> Mod ID: `forestry`
> 前置条件: Modtweaker
> 导入: `import mods.forestry.*;`

## API 列表

### Carpenter（木工机）

> `import mods.forestry.Carpenter;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient[][] ingredients, int packagingTime, @Optional ILiquidStack fluidInput, @Optional IItemStack box)` | void | 添加木工配方。`packagingTime` 为加工时间。`fluidInput` 可选流体输入。`box` 可选模具 |
| `.removeRecipe(IItemStack output, @Optional ILiquidStack fluidInput)` | void | 按输出移除配方 |

### Centrifuge（离心机）

> `import mods.forestry.Centrifuge;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(WeightedItemStack[] output, IItemStack ingredients, int packagingTime)` | void | 添加离心配方 |
| `.removeRecipe(IIngredient input)` | void | 按输入移除配方 |

### CharcoalWall（木炭墙）

> `import mods.forestry.CharcoalWall;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addWall(IBlock block, int amount)` | void | 添加木炭墙方块。`amount` 为产出木炭数 |
| `.addWallState(IBlockState state, int amount)` | void | 添加木炭墙方块状态 |
| `.addWallStack(IItemStack stack, int amount)` | void | 添加木炭墙物品堆（需可转方块） |
| `.removeWall(IBlock block)` | void | 按方块移除 |
| `.removeWallState(IBlockState state)` | void | 按方块状态移除 |
| `.removeWallStack(IItemStack stack)` | void | 按物品堆移除 |

### Fermenter（发酵机）

> `import mods.forestry.Fermenter;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidOutput, IItemStack resource, ILiquidStack fluidInput, int fermentationValue, float fluidOutputModifier)` | void | 添加发酵配方。流体输出量 = fermentationValue × fluidOutputModifier |
| `.removeRecipe(IIngredient input)` | void | 按输入移除配方 |
| `.addFuel(IItemStack item, int fermentPerCycle, int burnDuration)` | void | 添加发酵燃料。`fermentPerCycle` 每周期发酵量。`burnDuration` 单个燃料持续周期 |
| `.removeFuel(IIngredient fermenterItem)` | void | 移除发酵燃料 |

### Moistener（加湿器）

> `import mods.forestry.Moistener;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, int packagingTime)` | void | 添加加湿配方 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.addFuel(IItemStack item, IItemStack product, int moistenerValue, int stage)` | void | 添加加湿器燃料。`product` 离开工作槽的物品。`moistenerValue` 对最终产物的贡献。`stage` 阶段(低值先消耗) |
| `.removeFuel(IIngredient moistenerItem)` | void | 移除加湿器燃料 |

### Squeezer（榨汁机）

> `import mods.forestry.Squeezer;`

**注意**: 不能移除填充/排空流体容器的配方（如 Forestry 罐头）。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidOutput, IItemStack[] ingredients, int timePerItem, @Optional WeightedItemStack itemOutput)` | void | 添加榨汁配方 |
| `.removeRecipe(ILiquidStack liquid, @Optional IIngredient[] ingredients)` | void | 按流体输出移除配方 |

### Still（蒸馏器）

> `import mods.forestry.Still;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidOutput, ILiquidStack fluidInput, int timePerUnit)` | void | 添加蒸馏配方 |
| `.removeRecipe(ILiquidStack output, @Optional ILiquidStack fluidInput)` | void | 按输出移除配方 |

### ThermionicFabricator（热电子加工台）

> `import mods.forestry.ThermionicFabricator;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addCast(IItemStack output, IIngredient[][] ingredients, ILiquidStack liquidStack, @Optional IItemStack plan)` | void | 添加铸造配方 |
| `.removeCast(IIngredient product)` | void | 移除铸造配方 |
| `.addSmelting(ILiquidStack liquidStack, IItemStack itemInput, int meltingPoint)` | void | 添加熔炼配方。目前只有 `<liquid:glass>` 推荐使用 |
| `.removeSmelting(IIngredient itemInput)` | void | 移除熔炼配方 |

## 使用示例

### 添加木工配方

```zenscript
import mods.forestry.Carpenter;

Carpenter.addRecipe(<minecraft:redstone> * 9, [[<minecraft:redstone_block>]], 30);
Carpenter.addRecipe(<minecraft:gold_ingot>, [[<minecraft:gold_block>]], 30, <liquid:for.honey> * 100);
```

### 添加发酵配方

```zenscript
import mods.forestry.Fermenter;

Fermenter.addRecipe(<liquid:lava>, <minecraft:obsidian>, <liquid:water>, 1000, 0.5);
```

### 添加蒸馏配方

```zenscript
import mods.forestry.Still;

Still.addRecipe(<liquid:lava>, <liquid:water>, 200);
```
