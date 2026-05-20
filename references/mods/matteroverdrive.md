# Matter Overdrive CraftTweaker API 参考

> Mod ID: `matteroverdrive`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.matteroverdrive.*;`

## API 列表

### Inscriber（铭刻机）

> `import moretweaker.matteroverdrive.Inscriber;`

能量单位为 FE（Forge Energy），时间单位为 tick（1/20 秒）。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input1, IIngredient input2, IItemStack output, int energy, int time)` | void | 添加铭刻配方。`energy` 为能量消耗（FE），`time` 为加工时间（tick） |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### Matter（物质）

> `import moretweaker.matteroverdrive.Matter;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.set(IIngredient input, int matter)` | void | 设置物品的物质值 |
