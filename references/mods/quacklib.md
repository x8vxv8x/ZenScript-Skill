# QuackLib CraftTweaker API 参考

> Mod ID: `quacklib`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.quacklib.*;`

## API 列表

### AlloyFurnace（合金炉）

> `import moretweaker.quacklib.AlloyFurnace;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient[] inputs)` | void | 添加合金配方 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

## 注意事项

- 使用匹配多个物品的材料时，JEI 中只显示其中一个。这是 QuackLib JEI 支持的限制，非 MoreTweaker 的问题。
