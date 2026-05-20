# Erebus CraftTweaker API 参考

> Mod ID: `erebus`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.erebus.*;`

注意：由于 Erebus 处理配方的方式，仅允许使用 `IItemStack` 和 `IOreDictEntry` 作为物品材料。

## API 列表

### Composter（发酵器）

> `import moretweaker.erebus.Composter;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack compostable)` | void | 添加发酵物品 |
| `.addAll(IItemStack[] compostables)` | void | 批量添加可发酵物品 |
| `.remove(IItemStack nonCompostable)` | void | 移除可发酵物品 |
| `.removeAll(IItemStack[] nonCompostables)` | void | 批量移除可发酵物品 |

### OfferingAltar（奉献祭坛）

> `import moretweaker.erebus.OfferingAltar;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input1, IIngredient input2, IIngredient input3)` | void | 添加配方，需要 3 个输入 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### SmoothieMaker（冰沙机）

> `import moretweaker.erebus.SmoothieMaker;`

`container` 参数必须放在输出槽才能开始配方。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, optional IItemStack container, IIngredient[] inputs, ILiquidStack[] fluids)` | void | 添加冰沙配方。`container` 为容器物品（必须放在输出槽），`fluids` 为流体材料 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |
