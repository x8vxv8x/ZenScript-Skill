# NuclearCraft CraftTweaker API 参考

> Mod ID: `nuclearcraft`
> 前置条件: 无
> 导入: `import mods.nuclearcraft.<ClassName>;`

## 重要说明
- 这是核电工艺原版，不是重制版。使用前必须询问用户的模组类型。
- **所有方法参数必须使用双层括号 `([...])`**，因为 NuclearCraft 的方法需要数组参数
- 所有配方包含五类信息：物品输入、流体输入、物品输出、流体输出、额外信息
- 物品在前，流体在后

### 输入类型

| 类型 | 说明 |
|------|------|
| IItemStack | 物品，如 `<minecraft:gunpowder> * 4` |
| IOreDictEntry | 矿辞，如 `<ore:ingotIron> * 2` |
| ILiquidStack | 流体，如 `<liquid:lava> * 1500` |
| null | 空 |

### 概率输出类型

| 类型 | 格式 | 说明 |
|------|------|------|
| ChanceItemStack | `IItemStack, int percentage, @Optional int minStackSize` | 概率物品输出 |
| ChanceOreDictEntry | `IOreDictEntry, int percentage, @Optional int minStackSize` | 概率矿辞输出 |
| ChanceLiquidStack | `ILiquidStack, int percentage, int stackDifference, @Optional int minStackSize` | 概率流体输出 |

---

## API 列表

### Manufactory（小制造机）

> `import mods.nuclearcraft.manufactory;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([itemInput, itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加制造机配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([itemInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([itemOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Alloy Furnace（合金炉）

> `import mods.nuclearcraft.alloy_furnace;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([itemInput1, itemInput2, itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加合金炉配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([itemInput1, itemInput2])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([itemOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Isotope Separator（同位素分离器）

> `import mods.nuclearcraft.isotope_separator;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([itemInput, itemOutput1, itemOutput2, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加同位素分离器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([itemInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([itemOutput1, itemOutput2])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Decay Hastener（衰变加速器）

> `import mods.nuclearcraft.decay_hastener;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([itemInput, itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加衰变加速器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([itemInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([itemOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Fuel Reprocessor（燃料处理机）

> `import mods.nuclearcraft.fuel_reprocessor;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([itemInput, itemOutput1, itemOutput2, itemOutput3, itemOutput4, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([itemInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([itemOutput1, itemOutput2, itemOutput3, itemOutput4])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Electrolyzer（电解机）

> `import mods.nuclearcraft.electrolyzer;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput, fluidOutput1, fluidOutput2, fluidOutput3, fluidOutput4, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加电解配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput1, fluidOutput2, fluidOutput3, fluidOutput4])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Centrifuge（离心机）

> `import mods.nuclearcraft.centrifuge;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput, fluidOutput1, fluidOutput2, fluidOutput3, fluidOutput4, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加离心机配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput1, fluidOutput2, fluidOutput3, fluidOutput4])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Chemical Reactor（化学反应器）

> `import mods.nuclearcraft.chemical_reactor;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput1, fluidInput2, fluidOutput1, fluidOutput2, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加化学反应器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput1, fluidInput2])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput1, fluidOutput2])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Melter（金属熔化机）

> `import mods.nuclearcraft.melter;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([itemInput, fluidOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([itemInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Supercooler（超冷却机）

> `import mods.nuclearcraft.supercooler;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput, fluidOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Condenser

> `import mods.nuclearcraft.condenser;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput, fluidOutput, @Optional double coolingRequired, @Optional int condensingTemperature])` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Crystallizer（结晶器）

> `import mods.nuclearcraft.crystallizer;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput, itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加结晶器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([itemOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Infuser（流体注入器）

> `import mods.nuclearcraft.infuser;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([itemInput, fluidInput, itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([itemInput, fluidInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([itemOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Ingot Former（金属成型机）

> `import mods.nuclearcraft.ingot_former;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput, itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([itemOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Pressurizer（压缩机）

> `import mods.nuclearcraft.pressurizer;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([itemInput, itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([itemInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([itemOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Rock Crusher（碎石机）

> `import mods.nuclearcraft.rock_crusher;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([itemInput, itemOutput1, itemOutput2, itemOutput3, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([itemInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([itemOutput1, itemOutput2, itemOutput3])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Irradiator（中子辐照器）

> `import mods.nuclearcraft.irradiator;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput1, fluidInput2, fluidOutput1, fluidOutput2, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加辐照器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput1, fluidInput2])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput1, fluidOutput2])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Fluid Enricher（溶解器）

> `import mods.nuclearcraft.dissolver;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([itemInput, fluidInput, fluidOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([itemInput, fluidInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Fluid Extractor（流体提取机）

> `import mods.nuclearcraft.extractor;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([itemInput, itemOutput, fluidOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加流体提取配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([itemInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([itemOutput, fluidOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Salt Mixer（盐混合器）

> `import mods.nuclearcraft.salt_mixer;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput1, fluidInput2, fluidOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation])` | void | 添加盐混合器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput1, fluidInput2])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Heat Exchanger（热交换器）

> `import mods.nuclearcraft.heat_exchanger;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput, fluidOutput, double heatRequired, int temperatureIn, int temperatureOut])` | void | 添加热交换器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Steam Turbine（涡轮机）

> `import mods.nuclearcraft.turbine;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput, fluidOutput, double powerPerMB, double expansionLevel])` | void | 添加涡轮配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Decay Generator（衰变产能器）

> `import mods.nuclearcraft.decay_generator;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([blockInput, blockOutput, double lifetimeTicks, double energyPerSecond, @Optional double processRadiation])` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([blockInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([blockOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Fission（裂变）

> `import mods.nuclearcraft.fission;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([itemInput, itemOutput, double baseTime, double basePower, double baseHeat, String guiName, @Optional double processRadiation])` | void | 添加裂变配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([itemInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([itemOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Salt Fission（熔盐裂变）

> `import mods.nuclearcraft.salt_fission;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput, fluidOutput, double baseTime, double basePower, @Optional double processRadiation])` | void | 添加熔盐裂变配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Fusion（聚变）

> `import mods.nuclearcraft.fusion;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe([fluidInput1, fluidInput2, fluidOutput1, fluidOutput2, fluidOutput3, fluidOutput4, double comboTime, double comboPower, double comboHeatVar, @Optional double processRadiation])` | void | 添加聚变配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput([fluidInput1, fluidInput2])` | void | 根据输入移除 |
| `.removeRecipeWithOutput([fluidOutput1, fluidOutput2, fluidOutput3, fluidOutput4])` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

---

## Radiation（辐射系统）

### 物品辐射

> `import mods.nuclearcraft.radiation;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getRadiationLevel(IIngredient itemInput)` | double | 获取物品的辐射值（rads/tick） |

### 方块突变

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addBlockMutation(blockInput, blockOutput, double radiationThreshold)` | void | 添加方块突变。辐射低于阈值时不会突变 |

### 辐射免疫

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setRadiationImmunityGameStages(boolean defaultImmunity, string[] stageNames)` | void | 设置玩家辐射免疫。defaultImmunity 为无阶段时的默认免疫状态 |

### 实体辐射扩展

NuclearCraft 为 IEntityLivingBase 添加了以下扩展方法：

#### 辐射值操作

| 方法 | 返回 | 说明 |
|------|------|------|
| `IEntityLivingBase.addRadiation(double amount, @Optional boolean useImmunity)` | void | 增加辐射值 |
| `IEntityLivingBase.setRadiation(double amount, @Optional boolean useImmunity)` | void | 设置辐射值 |
| `IEntityLivingBase.getRadiation()` | double | 获取辐射值 |

#### 抗辐射缓冲操作

| 方法 | 返回 | 说明 |
|------|------|------|
| `IEntityLivingBase.addRadiationResistance(double amount, @Optional boolean slowBuffer)` | void | 增加抗辐射缓冲 |
| `IEntityLivingBase.setRadiationResistance(double amount, @Optional boolean slowBuffer)` | void | 设置抗辐射缓冲 |
| `IEntityLivingBase.getRadiationResistance(@Optional boolean slowBuffer)` | double | 获取抗辐射缓冲 |

#### 中毒缓冲操作

| 方法 | 返回 | 说明 |
|------|------|------|
| `IEntityLivingBase.addPoisonBuffer(double amount)` | void | 增加中毒缓冲 |
| `IEntityLivingBase.setPoisonBuffer(double amount)` | void | 设置中毒缓冲 |
| `IEntityLivingBase.getPoisonBuffer()` | double | 获取中毒缓冲 |

#### 辐射抗性操作

| 方法 | 返回 | 说明 |
|------|------|------|
| `IEntityLivingBase.addRadawayBuffer(double amount)` | void | 增加辐射抗性 |
| `IEntityLivingBase.setRadawayBuffer(double amount)` | void | 设置辐射抗性 |
| `IEntityLivingBase.getRadawayBuffer()` | double | 获取辐射抗性 |

#### 辐射等级获取

| 方法 | 返回 | 说明 |
|------|------|------|
| `IEntityLivingBase.getRawRadiationLevel()` | double | 获取原始辐射值（rads） |
| `IEntityLivingBase.getRadiationLevel()` | double | 获取辐射变化值（rads/tick） |