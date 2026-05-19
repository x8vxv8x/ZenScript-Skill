# Aether Legacy CraftTweaker API 参考

> Mod ID: `aether_legacy`
> 前置条件: 无
> 导入: `import mods.aether_legacy.<ClassName>;`

## API 列表

### Accessory (饰品)

> `import mods.aether_legacy.Accessory;`

#### 注册饰品方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerAccessory(IItemStack input, String type)` | void | 注册物品为Aether饰品，type 为饰品类型 |

#### 饰品类型
- ring（戒指）
- pendant（吊坠）
- cape（披风）
- shield（盾牌）
- gloves（手套）
- miscellaneous（杂项）

### Enchanter (附魔台)

> `import mods.aether_legacy.Enchanter;`

#### 添加附魔配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerEnchantment(IItemStack input, IItemStack output, int timeRequired)` | void | 添加附魔台配方，timeRequired 为所需时间（tick） |
| `.registerEnchantment(IItemStack repair, int timeRequired)` | void | 注册可修复物品，timeRequired 为所需时间（tick） |
| `.registerEnchanterFuel(IItemStack input, int timeGiven)` | void | 注册附魔台燃料，timeGiven 为提供时间（tick） |

#### 移除附魔配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeEnchantment(IItemStack input)` | void | 移除指定输入的附魔配方（1.5.2+） |

### Freezer (冷冻机)

> `import mods.aether_legacy.Freezer;`

#### 添加冷冻配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerFreezable(IItemStack input, IItemStack output, int timeRequired)` | void | 添加冷冻配方，timeRequired 为所需时间（tick） |
| `.registerFreezerFuel(IItemStack input, int timeGiven)` | void | 注册冷冻机燃料，timeGiven 为提供时间（tick） |

#### 移除冷冻配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeFreezable(IItemStack input)` | void | 移除指定输入的冷冻配方（1.5.2+） |
