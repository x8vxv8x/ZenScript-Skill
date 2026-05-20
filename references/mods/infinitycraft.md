# InfinityCraft CraftTweaker API 参考

> Mod ID: `infinitycraft`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.infinitycraft.*;`

## API 列表

### Compressor（压缩机）

> `import moretweaker.infinitycraft.Compressor;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output, optional int experience)` | void | 添加压缩配方。`experience` 为产出经验 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |
