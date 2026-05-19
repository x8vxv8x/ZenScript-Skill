# Survivalist CraftTweaker API 参考

> Mod ID: `survivalist`
> 前置条件: 无
> 导入: `import gigaherz.survivalist.<ClassName>;`

## API 列表

### Choppable (砧板)

> `import gigaherz.survivalist.Choppable;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output, outputMultiplier, hitCountMultiplier)` | void | 添加砧板配方，outputMultiplier 为输出倍率，hitCountMultiplier 为击打次数倍率 |
| `.removeRecipe(IIngredient output, IIngredient input)` | void | 移除指定输出的砧板配方 |

### Dryable (晾干架)

> `import gigaherz.survivalist.Dryable;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output, int time)` | void | 添加晾干架配方，time 为处理时间（tick） |
| `.removeRecipe(IIngredient output, IIngredient input)` | void | 移除指定输出的晾干架配方 |
