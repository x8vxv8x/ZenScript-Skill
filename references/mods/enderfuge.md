# Enderfuge CraftTweaker API 参考

> Mod ID: `enderfuge`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.enderfuge.*;`

## API 列表

### EnderFuge（末地熔炉）

> `import moretweaker.enderfuge.EnderFuge;`

#### 配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input)` | void | 添加熔炼配方 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |

#### 燃料方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(IIngredient fuel, optional int burnTicks)` | void | 添加燃料。`burnTicks` 为燃烧时间 |
| `.removeFuel(IIngredient fuel)` | void | 移除燃料 |

#### 清除方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeAllRecipes()` | void | 移除所有配方 |
| `.removeAllFuels()` | void | 移除所有燃料 |
