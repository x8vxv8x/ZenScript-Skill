# Cooking for Blockheads CraftTweaker API 参考

> Mod ID: `cookingforblockheads`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.cfb.*;`

## API 列表

### KitchenAppliances（厨房电器）

> `import moretweaker.cfb.KitchenAppliances;`

#### 烤面包机
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addToasterRecipe(IItemStack output, IIngredient input)` | void | 添加烤面包机配方 |
| `.removeToasterRecipe(IIngredient output)` | void | 按输出移除烤面包机配方 |
| `.removeAllToasterRecipes()` | void | 移除所有烤面包机配方 |

#### 水槽
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addSinkRecipe(IItemStack output, IIngredient input)` | void | 添加水槽配方 |
| `.removeSinkRecipe(IIngredient output)` | void | 按输出移除水槽配方 |
| `.removeAllSinkRecipes()` | void | 移除所有水槽配方 |

#### 烤箱
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addOvenRecipe(IItemStack output, IIngredient input)` | void | 添加烤箱配方 |
| `.removeOvenRecipe(IIngredient output)` | void | 按输出移除烤箱配方 |
| `.removeAllOvenRecipes()` | void | 移除所有烤箱配方 |

#### 食物配方
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFoodShapeless(IItemStack output, IIngredient[] inputs)` | void | 添加无序食物配方 |
| `.addFoodShaped(IItemStack output, IIngredient[][] inputs)` | void | 添加有序食物配方 |
| `.removeFoodRecipe(IIngredient output)` | void | 按输出移除食物配方 |
| `.removeAllFoodRecipes()` | void | 移除所有食物配方 |
