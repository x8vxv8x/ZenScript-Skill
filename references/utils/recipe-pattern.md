# Recipe Pattern CraftTweaker API 参考

> Mod ID: `ctintegration`
> 前置条件: CraftTweaker Integration
> 导入: `import mods.ctintegration.util.RecipePattern;`

类似 JSON 的配方注册方式。

## API 列表

### RecipePattern

> `import mods.ctintegration.util.RecipePattern;`

#### 静态方法（初始化）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.init(String[] recipePattern)` | RecipePattern | 从模式字符串数组创建 |
| `.init(IItemStack output, String[] recipePattern)` | RecipePattern | 从模式和输出创建 |
| `.init(String name, IItemStack output, String[] recipePattern)` | RecipePattern | 从名称、模式和输出创建 |

#### 配置方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.with(String character, IIngredient ingredient)` | RecipePattern | 将字符映射到 IIngredient（字符串只能包含一个字符） |
| `.and(String character, IIngredient ingredient)` | RecipePattern | 同 `with`，别名 |
| `.withOutput(IItemStack output)` | RecipePattern | 设置输出 |
| `.setMirrored(boolean isMirrored)` | RecipePattern | 设置是否镜像 |
| `.setName(String name)` | RecipePattern | 设置配方名 |
| `.setShapeless(boolean isShapeless)` | RecipePattern | 设置无序。无序时所有行合并为一行，忽略空白 |
| `.setFunction(IRecipeFunction function)` | RecipePattern | 设置配方函数 |
| `.setFunction(IRecipeAction action)` | RecipePattern | 设置配方动作 |
| `.map(Map<String, IIngredient> mapping)` | RecipePattern | 批量映射字符到 IIngredient |
| `.build()` | void | **必须调用** - 注册工作台配方 |

空白字符始终映射为 `null`。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `ingredients` | IIngredient[][] | 从映射获取二维 IIngredient 数组 |
| `shapelessIngredients` | IIngredient[] | 无序配方的一维 IIngredient 数组（无需先调用 setShapeless） |
