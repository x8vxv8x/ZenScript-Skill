# The Betweenlands CraftTweaker API 参考

> Mod ID: `thebetweenlands`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.betweenlands.*;`

## API 列表

### Animator（动画师）

> `import moretweaker.betweenlands.Animator;`

实体输出示例：`minecraft:wither`。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack input, int fuel, int life, IItemStack output)` | void | 添加物品输出配方。`fuel` 为燃料消耗，`life` 为生命值 |
| `.addRecipe(IItemStack input, int fuel, int life, String entity)` | void | 添加实体输出配方 |
| `.removeRecipe(IIngredient output)` | void | 按物品输出移除配方 |
| `.removeRecipe(String entityOutput)` | void | 按实体输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### Composter（堆肥箱）

> `import moretweaker.betweenlands.Composter;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input)` | void | 添加堆肥配方（使用默认值） |
| `.addRecipe(IIngredient input, int compostValue, int compostTime)` | void | 添加堆肥配方。`compostValue` 为堆肥值，`compostTime` 为堆肥时间 |

### DruidAltar（德鲁伊祭坛）

> `import moretweaker.betweenlands.DruidAltar;`

`inputs` 数组长度必须为 4。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient[] inputs)` | void | 添加德鲁伊祭坛配方 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### Mortar（研磨器）

> `import moretweaker.betweenlands.Mortar;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output)` | void | 添加研磨配方 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### Purifier（净化器）

> `import moretweaker.betweenlands.Purifier;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output)` | void | 添加净化配方 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |
