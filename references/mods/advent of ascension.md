# Advent of Ascension CraftTweaker API 参考

> Mod ID: `aoa`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.aoa.*;`

## API 列表

### InfusionTable（注魔台）

> `import moretweaker.aoa.InfusionTable;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack mainInput, IIngredient[] inputs, optional int infusionLevel, optional int xpMin, optional int xpMax)` | void | 添加物品注魔配方。`mainInput` 为中心物品，`inputs` 为周围材料，`infusionLevel` 为注魔等级，`xpMin`/`xpMax` 为经验范围 |
| `.addRecipe(String enchantmentId, int enchantmentLevel, IIngredient[] inputs, optional int infusionLevel, optional int xpMin, optional int xpMax)` | void | 添加附魔注魔配方 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IIngredient output)` | void | 按输出移除物品注魔配方 |
| `.removeRecipe(String enchantmentId)` | void | 按附魔 ID 移除附魔注魔配方 |
| `.removeAll()` | void | 移除所有注魔配方 |

### DivineStation（神圣祭坛 / 升级套件）

> `import moretweaker.aoa.DivineStation;`

#### 配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack input, IItemStack upgradeKit, IItemStack output)` | void | 添加升级套件配方 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |
