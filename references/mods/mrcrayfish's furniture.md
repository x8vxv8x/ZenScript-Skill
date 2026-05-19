# MrCrayfish's Furniture Mod CraftTweaker API 参考

> Mod ID: `cfm`
> 前置条件: 无
> 导入: `import mods.cfm.<ClassName>;`

## 注意事项

- 输入仅通过物品 ID 和元数据匹配，忽略 NBT

## API 列表

### Blender（搅拌机）

> `import mods.cfm.Blender;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addDrink(String name, IItemStack[] ingredients, int food, int[] colour)` | void | 添加搅拌饮品 |
| `.remove()` | void | 移除所有饮品 |
| `.remove(@Optional String name)` | void | 根据名称移除饮品 |
| `.remove(@Optional String name, @Optional IItemStack[] ingredients, @Optional Integer food, @Optional int[] colour)` | void | 根据参数匹配移除饮品 |

参数说明：
- `name`：饮品名称
- `ingredients`：所需物品数组
- `food`：恢复的食物值（饱和度与食物值无法独立设置）
- `colour`：RGB 颜色数组，如 `[255,182,193]`

### ChoppingBoard（砧板）

> `import mods.cfm.ChoppingBoard;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input)` | void | 添加砧板配方。输入必须为 1 个物品 |
| `.remove(@Optional IIngredient output, @Optional IIngredient input)` | void | 根据输入/输出匹配移除配方 |

### Dishwasher（洗碗机）

> `import mods.cfm.Dishwasher;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack item)` | void | 添加可清洗物品 |
| `.remove(@Optional IIngredient item)` | void | 移除可清洗物品。无参数则移除全部 |

### Freezer（冰箱冷冻室）

> `import mods.cfm.Freezer;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input)` | void | 添加冷冻配方。输入必须为 1 个物品 |
| `.remove(@Optional IIngredient output, @Optional IIngredient input)` | void | 根据输入/输出匹配移除配方。无参数则移除全部 |

### Grill（烧烤架）

> `import mods.cfm.Grill;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input)` | void | 添加烧烤配方。输入必须为 1 个物品 |
| `.remove(@Optional IIngredient output, @Optional IIngredient input)` | void | 根据输入/输出匹配移除配方。无参数则移除全部 |

### Microwave（微波炉）

> `import mods.cfm.Microwave;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input)` | void | 添加微波炉配方 |
| `.remove(@Optional IIngredient output, @Optional IIngredient input)` | void | 根据输入/输出匹配移除配方。无参数则移除全部 |

### MineBay（交易市场）

> `import mods.cfm.MineBay;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addTrade(IItemStack item, IItemStack currency)` | void | 添加交易。item 为商品，currency 为货币 |
| `.remove(@Optional IIngredient item)` | void | 根据交易结果移除交易。无参数则移除全部 |

### Oven（烤箱）

> `import mods.cfm.Oven;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input)` | void | 添加烤箱配方 |
| `.remove(@Optional IIngredient output, @Optional IIngredient input)` | void | 根据输入/输出匹配移除配方。无参数则移除全部 |

### Printer（打印机）

> `import mods.cfm.Printer;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack item)` | void | 添加可复制物品 |
| `.remove(@Optional IIngredient item)` | void | 移除可复制物品。无参数则移除全部 |

### Toaster（烤面包机）

> `import mods.cfm.Toaster;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input)` | void | 添加烤面包机配方。输入必须为 1 个物品 |
| `.remove(@Optional IIngredient output, @Optional IIngredient input)` | void | 根据输入/输出匹配移除配方。无参数则移除全部 |

### WashingMachine（洗衣机）

> `import mods.cfm.WashingMachine;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack item)` | void | 添加可清洗物品 |
| `.remove(@Optional IIngredient item)` | void | 移除可清洗物品。无参数则移除全部 |
