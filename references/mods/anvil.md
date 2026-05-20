# Anvil CraftTweaker API 参考

> Mod ID: `roidtweaker`
> 前置条件: Roids-Tweaker
> 导入: `import mods.roidtweaker.minecraft.Anvil;`
> 配置要求: `event category.allowAnvilRecipes=true`

## API 列表

### Anvil

> `import mods.roidtweaker.minecraft.Anvil;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient left, IIngredient right, IItemStack output, int xpCost)` | void | 添加铁砧配方 |
| `.addRecipeShapeless(IIngredient left, IIngredient right, IItemStack output, int xpCost)` | void | 添加无序铁砧配方 |
| `.addRecipes(IIngredient left, IIngredient[] right, IItemStack[] output, int[] xpCost)` | void | 批量添加配方（循环调用 addRecipe） |
| `.remove(IIngredient[] inputs)` | void | 按输入移除配方。仅指定一个输入时使用左侧。支持 `<*>` |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.addRepair(IIngredient repaired, IIngredient material, int amount, @Optional int xpCost)` | void | 添加修复配方。`amount` 为每材料修复量。默认 xpCost 为消耗的右侧物品数量 |
| `.addRepair(IIngredient repaired, IIngredient material, float amount, @Optional int xpCost)` | void | 同上，但 amount 为耐久百分比 |

所有方法支持 Ingredient Conditions 和 Ingredient Transformers。
