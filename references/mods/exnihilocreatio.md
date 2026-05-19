# Ex Nihilo Creatio CraftTweaker API 参考

> Mod ID: `exnihilocreatio`
> 前置条件: 无
> 导入: `import mods.exnihilocreatio.*;`

Ex Nihilo Creatio 是一个提供筛矿、锤击、堆肥等功能的模组。

---

## API 列表

### Sieve（筛子）

> `import mods.exnihilocreatio.Sieve;`

#### 添加筛矿配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addStringMeshRecipe(input as IIngredient, output as IItemStack, chance as float)` | void | 添加线筛配方 |
| `.addFlintMeshRecipe(input as IIngredient, output as IItemStack, chance as float)` | void | 添加燧石筛配方 |
| `.addIronMeshRecipe(input as IIngredient, output as IItemStack, chance as float)` | void | 添加铁筛配方 |
| `.addDiamondMeshRecipe(input as IIngredient, output as IItemStack, chance as float)` | void | 添加钻石筛配方 |

**参数说明**:
- `input`: 输入方块
- `output`: 输出物品
- `chance`: 掉落概率（0-1）

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeAll()` | void | 移除所有筛矿配方 |

### Hammer（锤子）

> `import mods.exnihilocreatio.Hammer;`

#### 添加锤击配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, output as IItemStack, toolLevel as int, chance as float, fortuneChance as float)` | void | 添加锤击配方 |

**参数说明**:
- `input`: 输入方块
- `output`: 输出物品
- `toolLevel`: 工具等级
- `chance`: 掉落概率（0-1）
- `fortuneChance`: 时运掉落概率（0-1）

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeAll()` | void | 移除所有锤击配方 |

### Crook（钩子）

> `import mods.exnihilocreatio.Crook;`

#### 添加钩子配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, reward as IItemStack, chance as float, fortuneChance as float)` | void | 添加钩子配方 |

**参数说明**:
- `input`: 输入方块
- `reward`: 奖励物品
- `chance`: 掉落概率（0-1）
- `fortuneChance`: 时运掉落概率（0-1）

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeAll()` | void | 移除所有钩子配方 |

### Compost（堆肥）

> `import mods.exnihilocreatio.Compost;`

#### 添加堆肥配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, chance as float, color as string, output as IItemStack)` | void | 添加堆肥配方 |

**参数说明**:
- `input`: 输入物品
- `chance`: 堆肥概率（0-1）
- `color`: 颜色（十六进制）
- `output`: 输出物品

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeAll()` | void | 移除所有堆肥配方 |

### Heat（热源）

> `import mods.exnihilocreatio.Heat;`

#### 添加热源

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IItemStack, heat as int)` | void | 添加热源方块 |

**参数说明**:
- `input`: 热源方块
- `heat`: 热量值

#### 移除热源

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeAll()` | void | 移除所有热源 |

### Ore（矿石）

> `import mods.exnihilocreatio.Ore;`

**注意**: 需要在 `#loader preinit` 或 `#loader contenttweaker` 中使用。

#### 添加矿石

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(name as string, color as string, @Optional output as IItemStack, @Optional translations as string[string], @Optional oreDict as string)` | void | 添加矿石 |

**参数说明**:
- `name`: 矿石名称
- `color`: 颜色（十六进制）
- `output`: 输出物品（需要使用 oredict.firstItem）
- `translations`: 翻译映射
- `oreDict`: 矿辞名称

#### 移除矿石

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeAll()` | void | 移除所有矿石 |