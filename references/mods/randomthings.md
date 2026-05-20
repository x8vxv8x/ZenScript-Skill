# Random Things CraftTweaker API 参考

> Mod ID: `randomthings`
> 前置条件: Roids-Tweaker
> 导入: `import mods.roidtweaker.randomthings.Imbuing;`

## API 列表

### Imbuing（灌注台）

> `import mods.roidtweaker.randomthings.Imbuing;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input, IIngredient[] ingredients)` | void | 添加配方。支持条件，不支持转换器。ingredients 长度应为 3。支持 null IIngredient |
| `.removeRecipe(IIngredient output)` | void | 移除输出匹配的配方 |
| `.removeRecipe(int index)` | void | 按索引移除配方。注意：其他模组在 PostInit 添加配方时索引不可靠。默认配方顺序：苔石砖、火焰、毒药、经验、凋零。自定义配方按脚本顺序排列 |
| `.clearRecipes()` | void | 清除所有配方 |
