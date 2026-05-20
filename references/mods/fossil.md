# Fossils and Archeology CraftTweaker API 参考

> Mod ID: `fossil`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.fossil.*;`

注意：Fossils and Archeology 有原生 CraftTweaker 支持，但其分析仪和筛分器的配方移除功能存在缺陷，因此推荐使用 MoreTweaker 版本。

## API 列表

### Analyzer（分析仪）

> `import moretweaker.fossil.Analyzer;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addOutput(IIngredient input, IItemStack output, double weight)` | void | 添加分析输出。`weight` 为权重 |
| `.removeByInput(IIngredient input)` | void | 按输入移除 |
| `.removeByOutput(IIngredient output)` | void | 按输出移除 |
| `.removeAll()` | void | 移除所有输出 |

### Sifter（筛分器）

> `import moretweaker.fossil.Sifter;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addOutput(IIngredient input, IItemStack output, double weight)` | void | 添加筛分输出。`weight` 为权重 |
| `.removeByInput(IIngredient input)` | void | 按输入移除 |
| `.removeByOutput(IIngredient output)` | void | 按输出移除 |
| `.removeAll()` | void | 移除所有输出 |

### ArcheologyWorkbench（考古工作台）

> `import moretweaker.fossil.ArcheologyWorkbench;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output, optional IIngredient fuel)` | void | 添加考古配方。`fuel` 为燃料 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### CultureVat（培养缸）

> `import moretweaker.fossil.CultureVat;`

可添加自定义配方，但无法将新物品放入输入槽。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output)` | void | 添加培养配方 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |
