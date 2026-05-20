# Bewitchment CraftTweaker API 参考

> Mod ID: `bewitchment`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.bewitchment.*;`

## API 列表

### Distillery（蒸馏器）

> `import moretweaker.bewitchment.Distillery;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack[] outputs, IIngredient[] inputs)` | void | 添加蒸馏配方，支持多输出 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### FrostFire（霜火）

> `import moretweaker.bewitchment.FrostFire;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input)` | void | 添加霜火配方 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### WitchesCauldron（女巫大锅）

> `import moretweaker.bewitchment.WitchesCauldron;`

#### 配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack[] outputs, IIngredient[] inputs)` | void | 添加大锅配方，支持多输出 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAllRecipes()` | void | 移除所有配方 |

#### 酿造方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addBrew(IIngredient[] trigger, String potion, optional int duration, optional int amplifier)` | void | 添加酿造配方。`trigger` 为触发材料，`potion` 为药水 ID，`duration` 为持续时间，`amplifier` 为效果等级 |
| `.removeBrew(IIngredient trigger)` | void | 按触发材料移除酿造配方 |
| `.removeAllBrews()` | void | 移除所有酿造配方 |

### WitchesOven（女巫烤炉）

> `import moretweaker.bewitchment.WitchesOven;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, IItemStack output, IItemStack byproduct, optional float chance, optional boolean requiresJar)` | void | 添加烤炉配方。`byproduct` 为副产品，`chance` 为副产品概率，`requiresJar` 为是否需要罐子 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### WitchesRitual（女巫仪式）

> `import moretweaker.bewitchment.WitchesRitual;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String name, IItemStack[] outputs, IIngredient[] inputs, String entityOutput, String entityInput, int power, int ringSmall, int ringMedium, int ringLarge)` | void | 添加仪式配方 |
| `.removeByOutput(IIngredient output)` | void | 按输出移除配方 |
| `.removeByInput(IIngredient input)` | void | 按输入移除配方 |
| `.removeAll()` | void | 移除所有配方 |

#### 粉笔环字段

`ringSmall`、`ringMedium`、`ringLarge` 参数使用以下字段值：

| 字段 | 说明 |
|------|------|
| `WitchesRitual.NONE` | 无粉笔 |
| `WitchesRitual.GOLDEN` | 金色粉笔（注意：使用此值会抛出异常，因为金色环不可用） |
| `WitchesRitual.RITUAL` | 仪式粉笔（标准白色粉笔） |
| `WitchesRitual.FIERY` | 烈焰/地狱粉笔 |
| `WitchesRitual.PHASING` | 相位/异界粉笔 |
| `WitchesRitual.ANY` | 任意粉笔 |
