# Inspirations CraftTweaker API 参考

> Mod ID: `inspirations`
> 前置条件: Modtweaker
> 导入: `import mods.inspirations.Cauldron;`

## API 列表

### Cauldron（炼药锅）

> `import mods.inspirations.Cauldron;`

Inspirations 扩展了原版炼药锅，支持流体、酿造和染色配方。如果配置中炼药锅设为 `simple` 模式，只有使用水的配方可以被合成，但所有配方仍会在 JEI 中显示。

#### 流体配方

##### 流体变换（物品 + 流体 → 物品）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFluidRecipe(IItemStack output, IIngredient input, ILiquidStack fluid, @Optional int levels, @Optional boolean boiling)` | void | 添加流体配方。`levels` 消耗液位数(0-3, 默认1)。`boiling` 是否需要火焰(默认忽略) |
| `.removeFluidRecipe(IIngredient output, @Optional IIngredient input, @Optional ILiquidStack fluid)` | void | 移除流体配方 |

##### 流体转换（物品 + 流体A → 流体B）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFluidTransform(ILiquidStack output, IIngredient input, ILiquidStack fluid, @Optional int maxLevels, @Optional boolean boiling)` | void | 添加流体转换配方。`maxLevels` 最大液位限制 |
| `.removeFluidTransform(IIngredient output, @Optional IIngredient input, @Optional ILiquidStack fluid)` | void | 移除流体转换配方 |

##### 填充配方（物品 + 流体 → 填充炼药锅）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFillRecipe(IIngredient input, ILiquidStack fluid, @Optional int levels, @Optional IItemStack container)` | void | 添加填充配方。`levels` 填充液位数(默认1)。`container` 返回容器物品 |
| `.removeFillRecipe(IIngredient input, @Optional ILiquidStack fluid)` | void | 移除填充配方 |

#### 酿造配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addBrewingRecipe(String output, String input, IIngredient reagent)` | void | 添加酿造配方（药水类型名）。可用 `/ct inspirations potions` 查看所有药水类型 |
| `.removeBrewingRecipe(String output, @Optional String input, @Optional IIngredient reagent)` | void | 移除酿造配方。input/output 设为 null 则为通配 |
| `.addPotionRecipe(IItemStack output, IIngredient input, String potion, @Optional int levels, @Optional boolean boiling)` | void | 添加药水物品配方 |
| `.removePotionRecipe(IIngredient output, @Optional IIngredient input, @Optional String potion)` | void | 移除药水物品配方 |

#### 染色配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addDyeRecipe(IItemStack output, IIngredient input, String dye)` | void | 添加染色配方。`dye` 为 EnumDyeColor 字符串，可用 `/ct inspirations dyes` 查看 |
| `.removeDyeRecipe(IIngredient output, @Optional IIngredient input, @Optional String dye)` | void | 移除染色配方 |

## 使用示例

### 添加流体配方

```zenscript
import mods.inspirations.Cauldron;

// 烈焰粉 + 岩浆 → 烈焰棒
Cauldron.addFluidRecipe(<minecraft:blaze_rod>, <minecraft:blaze_powder> * 2, <liquid:lava>);

// 需要火焰的配方
Cauldron.addFluidRecipe(<minecraft:water_bucket>, <minecraft:ice>, <liquid:lava>, 1, true);
```

### 添加酿造配方

```zenscript
import mods.inspirations.Cauldron;

Cauldron.addBrewingRecipe("minecraft:invisibility", "minecraft:thick", <minecraft:diamond>);
```

### 添加染色配方

```zenscript
import mods.inspirations.Cauldron;

Cauldron.addDyeRecipe(<minecraft:diamond>, <minecraft:emerald>, "blue");
```
