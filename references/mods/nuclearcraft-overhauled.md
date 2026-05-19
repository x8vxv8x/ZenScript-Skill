# NuclearCraft: Overhauled CraftTweaker API 参考

> Mod ID: `nuclearcraft`
> 前置条件: 无
> 导入: `import mods.nuclearcraft.<ClassName>;`

## 重要说明
- 这是核电工艺重制版，不是原版。使用前必须询问用户的模组类型。
- 所有配方包含五类信息：物品输入、流体输入、物品输出、流体输出、额外信息
- 物品在前，流体在后
- 部分方法需要 `#loader preinit` 预处理器

## 概率成分系统

### ChanceItemIngredient

> `mods.nuclearcraft.ChanceItemIngredient`

#### 创建方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(IIngredient ingredient, int chancePercent, @Optional int minStackSize)` | ChanceItemIngredient | 创建概率物品成分 |

#### 查询方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getInternalIngredient()` | IIngredient | 获取内部成分 |
| `.getChancePercent()` | int | 获取概率百分比 |
| `.getMinStackSize()` | int | 获取最小堆叠数 |

### ChanceFluidIngredient

> `mods.nuclearcraft.ChanceFluidIngredient`

#### 创建方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(IIngredient ingredient, int chancePercent, int stackDiff, @Optional int minStackSize)` | ChanceFluidIngredient | 创建概率流体成分 |

#### 查询方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getInternalIngredient()` | IIngredient | 获取内部成分 |
| `.getChancePercent()` | int | 获取概率百分比 |
| `.getStackDiff()` | int | 获取堆叠差异 |
| `.getMinStackSize()` | int | 获取最小堆叠数 |

---

## API 列表

### Manufactory（小制造机）

> `import mods.nuclearcraft.Manufactory;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, IIngredient itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加制造机配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient itemInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Alloy Furnace（合金炉）

> `import mods.nuclearcraft.AlloyFurnace;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput1, IIngredient itemInput2, IIngredient itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加合金炉配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient itemInput1, IIngredient itemInput2)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Assembler（组合机）

> `import mods.nuclearcraft.Assembler;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput1, IIngredient itemInput2, IIngredient itemInput3, IIngredient itemInput4, IIngredient itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加装配机配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient itemInput1, IIngredient itemInput2, IIngredient itemInput3, IIngredient itemInput4)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Separator（分离器）

> `import mods.nuclearcraft.Separator;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, IIngredient itemOutput1, IIngredient itemOutput2, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加分离器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient itemInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput1, IIngredient itemOutput2)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Decay Hastener（衰变加速器）

> `import mods.nuclearcraft.DecayHastener;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, IIngredient itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加衰变加速器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient itemInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Fuel Reprocessor（燃料再处理机）

> `import mods.nuclearcraft.FuelReprocessor;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, IIngredient itemOutput1~8, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加燃料再处理配方（8 个输出） |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient itemInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput1~8)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Electrolyzer（电解机）

> `import mods.nuclearcraft.Electrolyzer;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput, ILiquidStack fluidOutput1~4, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加电解配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput1~4)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Centrifuge（离心机）

> `import mods.nuclearcraft.Centrifuge;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput, ILiquidStack fluidOutput1~6, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加离心机配方（6 个输出） |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput1~6)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Chemical Reactor（化学反应器）

> `import mods.nuclearcraft.ChemicalReactor;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput1, ILiquidStack fluidInput2, ILiquidStack fluidOutput1, ILiquidStack fluidOutput2, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加化学反应器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(ILiquidStack fluidInput1, ILiquidStack fluidInput2)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput1, ILiquidStack fluidOutput2)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Melter（熔化机）

> `import mods.nuclearcraft.Melter;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, ILiquidStack fluidOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient itemInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Supercooler（超冷却机）

> `import mods.nuclearcraft.Supercooler;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput, ILiquidStack fluidOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加超冷却机配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Condenser

> `import mods.nuclearcraft.Condenser;`

**注意：部分功能损坏**

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput, ILiquidStack fluidOutput, @Optional double coolingRequired, @Optional int condensingTemperature)` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Crystallizer（结晶器）

> `import mods.nuclearcraft.Crystallizer;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput, IIngredient itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加结晶器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Infuser（流体注入器）

> `import mods.nuclearcraft.Infuser;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, ILiquidStack fluidInput, IIngredient itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient itemInput, ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Ingot Former（冷却器）

> `import mods.nuclearcraft.IngotFormer;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput, IIngredient itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Pressurizer（压缩机）

> `import mods.nuclearcraft.Pressurizer;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, IIngredient itemOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient itemInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Rock Crusher（岩石粉碎机）

> `import mods.nuclearcraft.RockCrusher;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, IIngredient itemOutput1, IIngredient itemOutput2, IIngredient itemOutput3, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加岩石粉碎机配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient itemInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput1, IIngredient itemOutput2, IIngredient itemOutput3)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Enricher（溶解器）

> `import mods.nuclearcraft.Enricher;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, ILiquidStack fluidInput, ILiquidStack fluidOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient itemInput, ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Extractor（流体提取机）

> `import mods.nuclearcraft.Extractor;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, IIngredient itemOutput, ILiquidStack fluidOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加流体提取机配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient itemInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput, ILiquidStack fluidOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Salt Mixer（盐混合器）

> `import mods.nuclearcraft.SaltMixer;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput1, ILiquidStack fluidInput2, ILiquidStack fluidOutput, @Optional double timeMultiplier, @Optional double powerMultiplier, @Optional double processRadiation)` | void | 添加盐混合器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(ILiquidStack fluidInput1, ILiquidStack fluidInput2)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Heat Exchanger（热交换器）

> `import mods.nuclearcraft.HeatExchanger;`

**注意：部分功能损坏**

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput, ILiquidStack fluidOutput, double heatRequired, int temperatureIn, int temperatureOut)` | void | 添加热交换器配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Turbine（涡轮机）

> `import mods.nuclearcraft.Turbine;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput, ILiquidStack fluidOutput, double powerPerMB, double expansionLevel, @Optional String particleEffect, @Optional double particleSpeedMultiplier)` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Decay Generator（衰变产能器）

> `import mods.nuclearcraft.DecayGenerator;`

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient blockInput, IIngredient blockOutput, double meanLifetime, double power, double radiation)` | void | 添加配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(IIngredient blockInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient blockOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Fission 系列

#### SolidFission（固体燃料裂变）

> `import mods.nuclearcraft.SolidFission;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, IIngredient itemOutput, int time, int heat, double efficiency, int criticality, boolean selfPriming, double radiation)` | void | 添加固体裂变配方 |
| `.removeRecipeWithInput(IIngredient itemInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

#### SaltFission（熔盐裂变）

> `import mods.nuclearcraft.SaltFission;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput, ILiquidStack fluidOutput, double baseTime, double basePower, @Optional double processRadiation)` | void | 添加熔盐裂变配方 |
| `.removeRecipeWithInput(ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

#### FissionModerator（裂变慢化剂）

> `import mods.nuclearcraft.FissionModerator;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IIngredient block, int fluxFactor, double efficiency)` | void | 添加裂变慢化剂 |
| `.remove(IIngredient block)` | void | 移除裂变慢化剂 |
| `.removeAll()` | void | 移除所有慢化剂 |

#### FissionReflector（裂变反射器）

> `import mods.nuclearcraft.FissionReflector;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IIngredient block, double efficiency, double reflectivity)` | void | 添加裂变反射器 |
| `.remove(IIngredient block)` | void | 移除裂变反射器 |
| `.removeAll()` | void | 移除所有反射器 |

#### FissionIrradiator（裂变辐照器）

> `import mods.nuclearcraft.FissionIrradiator;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IIngredient itemInput, IIngredient itemOutput, int fluxRequired, double heatPerFlux, double efficiency, double radiation)` | void | 添加裂变辐照器配方 |
| `.removeRecipeWithInput(IIngredient itemInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

#### FissionHeating（裂变加热）

> `import mods.nuclearcraft.FissionHeating;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput, ILiquidStack fluidOutput, int heatPerInputMB)` | void | 添加裂变加热配方 |
| `.removeRecipeWithInput(ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

#### FissionEmergencyCooling（裂变紧急冷却）

> `import mods.nuclearcraft.FissionEmergencyCooling;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput, ILiquidStack fluidOutput, double coolingPerInputMB)` | void | 添加裂变紧急冷却配方 |
| `.removeRecipeWithInput(ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput)` | void | 根据输出移除 |

### Fusion（聚变）

> `import mods.nuclearcraft.Fusion;`

**注意：尚未实现**

#### 添加配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput1, ILiquidStack fluidInput2, ILiquidStack fluidOutput1~4, double comboTime, double comboPower, double comboHeatVar, double processRadiation)` | void | 添加聚变配方 |

#### 移除配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipeWithInput(ILiquidStack fluidInput1, ILiquidStack fluidInput2)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(ILiquidStack fluidOutput1~4)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

---

## Radiation（辐射系统）

### RadiationScrubber（辐射清洗器）

> `import mods.nuclearcraft.RadiationScrubber;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, ILiquidStack fluidInput, IIngredient itemOutput, ILiquidStack fluidOutput, int processTime, int processPower, double processEfficiency)` | void | 添加辐射清洗器配方 |
| `.removeRecipeWithInput(IIngredient itemInput, ILiquidStack fluidInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient itemOutput, ILiquidStack fluidOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### RadiationBlockMutation（辐射方块突变）

> `import mods.nuclearcraft.RadiationBlockMutation;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient blockInput, IIngredient blockOutput, double radiationThreshold)` | void | 添加方块突变配方 |
| `.removeRecipeWithInput(IIngredient blockInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient blockOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### RadiationBlockPurification（辐射方块净化）

> `import mods.nuclearcraft.RadiationBlockPurification;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient blockInput, IIngredient blockOutput, double radiationThreshold)` | void | 添加方块净化配方 |
| `.removeRecipeWithInput(IIngredient blockInput)` | void | 根据输入移除 |
| `.removeRecipeWithOutput(IIngredient blockOutput)` | void | 根据输出移除 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Radiation（辐射工具）

> `import mods.nuclearcraft.Radiation;`

#### 成分辐射

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getRadiationLevel(IIngredient ingredient)` | double | 获取成分辐射值（rads/tick） |
| `.setRadiationLevel(IIngredient ingredient, double radiation)` | void | 设置成分辐射值 |

#### 食物辐射

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setFoodRadiationStats(IItemStack food, double radiation, double resistance)` | void | 设置食物辐射统计 |

#### 其他辐射

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addToRadiationBlacklist(IIngredient ingredient)` | void | 将成分加入辐射黑名单 |
| `.setMaterialRadiationLevel(String oreSuffix, double radiation)` | void | 设置材料辐射等级（支持 Unix 通配符） |

#### 辐射免疫

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setRadiationImmunityGameStages(boolean defaultImmunity, String[] stageNames)` | void | 设置玩家辐射免疫 |

### 实体辐射扩展

NuclearCraft: Overhauled 为 IEntityLivingBase 添加了以下扩展方法：

#### 辐射值操作

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRadiation(double amount, @Optional boolean useImmunity)` | void | 增加辐射值 |
| `.setRadiation(double amount, @Optional boolean useImmunity)` | void | 设置辐射值 |
| `.getRadiation()` | double | 获取辐射值 |

#### 抗辐射缓冲操作

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRadawayBuffer(double amount, @Optional boolean slowBuffer)` | void | 增加抗辐射缓冲 |
| `.setRadawayBuffer(double amount, @Optional boolean slowBuffer)` | void | 设置抗辐射缓冲 |
| `.getRadawayBuffer(boolean slowBuffer)` | double | 获取抗辐射缓冲。slowBuffer=true 返回慢速缓冲 |

#### 中毒缓冲操作

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addPoisonBuffer(double amount)` | void | 增加中毒缓冲 |
| `.setPoisonBuffer(double amount)` | void | 设置中毒缓冲 |
| `.getPoisonBuffer()` | double | 获取中毒缓冲 |

#### 辐射抗性操作

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRadiationResistance(double amount)` | void | 增加辐射抗性 |
| `.setRadiationResistance(double amount)` | void | 设置辐射抗性 |
| `.getRadiationResistance()` | double | 获取辐射抗性 |

#### 辐射等级获取

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getRawRadiationLevel()` | double | 获取原始辐射值（rads） |
| `.getRadiationLevel()` | double | 获取辐射变化值（rads/tick） |

---

## Registration（注册系统）

> `import mods.nuclearcraft.Registration;`

**注意：需要 `#loader preinit` 预处理器**

### 裂变散热器

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerFissionSink(String name, int coolingValue, String placementRule)` | void | 注册裂变散热器 |

### 熔盐裂变冷却加热器

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerFissionHeater(String name, String fluidInput, int inputAmount, String fluidOutput, int outputAmount, int coolingValue, String placementRule)` | void | 注册熔盐裂变冷却加热器 |

### 涡轮线圈

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerTurbineCoil(String name, double efficiency, String placementRule)` | void | 注册涡轮线圈 |

### 涡轮转子叶片

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerTurbineBlade(String name, double efficiency, double expansionCoefficient)` | void | 注册涡轮转子叶片 |

### 涡轮转子定子

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerTurbineStator(String name, double expansionCoefficient)` | void | 注册涡轮转子定子 |

---

## Recipe Info（配方信息）

> 通过 `.getRecipeHandler()` 获取配方处理器

### RecipeHandler 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getRecipeName()` | string | 获取配方名称 |
| `.getRecipeList()` | Recipe[] | 获取配方列表 |
| `.getItemInputSize()` | int | 获取物品输入槽位数 |
| `.getFluidInputSize()` | int | 获取流体输入槽位数 |
| `.getItemOutputSize()` | int | 获取物品输出槽位数 |
| `.getFluidOutputSize()` | int | 获取流体输出槽位数 |
| `.isShapeless()` | bool | 是否无序配方 |

### Recipe 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getItemIngredient(int index)` | IIngredient | 获取指定索引的物品输入 |
| `.getFluidIngredient(int index)` | ILiquidStack | 获取指定索引的流体输入 |
| `.getItemProduct(int index)` | IIngredient | 获取指定索引的物品输出 |
| `.getFluidProduct(int index)` | ILiquidStack | 获取指定索引的流体输出 |