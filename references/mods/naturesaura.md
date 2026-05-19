# Nature's Aura CraftTweaker API 参考

> Mod ID: `naturesaura`
> 前置条件: 无
> 导入: `import mods.naturesaura.Altar;` / `import mods.naturesaura.TreeRitual;` / `import mods.naturesaura.Offering;` / `import mods.naturesaura.AnimalSpawner;`

## API 列表

### Altar（自然祭坛）

> `import mods.naturesaura.Altar;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String name, IIngredient input, IItemStack output, IIngredient catalyst, int aura, int time)` | void | 添加自然祭坛配方 |
| `.removeRecipe(IItemStack output)` | void | 根据输出物品移除配方 |

参数说明：
- `name`：配方注册名
- `input`：输入物品
- `output`：输出物品
- `catalyst`：催化剂方块（放置在四个角落），可为 null
- `aura`：完成配方所需的灵气量
- `time`：处理时间（tick）

### TreeRitual（森林仪式）

> `import mods.naturesaura.TreeRitual;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String name, IIngredient saplingType, IItemStack output, int time, IIngredient[] items)` | void | 添加森林仪式配方 |
| `.removeRecipe(IItemStack output)` | void | 根据输出物品移除配方 |

参数说明：
- `name`：配方注册名
- `saplingType`：需要放置并生长成树的树苗
- `output`：仪式产出物品
- `time`：处理时间（tick）
- `items`：仪式所需物品列表

### Offering（献祭）

> `import mods.naturesaura.Offering;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String name, IIngredient input, int inputAmount, IIngredient startItem, IItemStack output)` | void | 添加献祭配方 |
| `.removeRecipe(IItemStack output)` | void | 根据输出物品移除配方 |

参数说明：
- `name`：配方注册名
- `input`：献祭物品
- `inputAmount`：所需献祭物品数量（input 变量的数量会被忽略）
- `startItem`：启动献祭所需的物品
- `output`：献祭产出物品

### AnimalSpawner（生物生成祭坛）

> `import mods.naturesaura.AnimalSpawner;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String name, String entity, int aura, int time, IIngredient[] ingredients)` | void | 添加生物生成配方 |
| `.removeRecipe(String name)` | void | 根据配方注册名移除配方 |

参数说明：
- `name`：配方注册名
- `entity`：要生成的实体名称
- `aura`：完成配方所需的灵气量
- `time`：处理时间（tick）
- `ingredients`：所需物品列表
