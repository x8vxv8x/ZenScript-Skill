# Thermal Expansion CraftTweaker API 参考

> Mod ID: `thermalexpansion`
> 前置条件: Modtweaker
> 导入: `import mods.thermalexpansion.*;`

## API 列表

### Pulverizer（磨粉机）

> `import mods.thermalexpansion.Pulverizer;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, int energy, @Optional IItemStack secondaryOutput, @Optional int secondaryChance)` | void | 添加粉碎配方 |
| `.removeRecipe(IItemStack input)` | void | 按输入移除配方 |

### Sawmill（锯木机）

> `import mods.thermalexpansion.Sawmill;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, int energy, @Optional IItemStack secondaryOutput, @Optional int secondaryChance)` | void | 添加锯木配方 |
| `.removeRecipe(IItemStack input)` | void | 按输入移除配方 |

### InductionSmelter（感应炉）

> `import mods.thermalexpansion.InductionSmelter;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack primaryOutput, IItemStack primaryInput, IItemStack secondaryInput, int energy, @Optional IItemStack secondaryOutput, @Optional int secondaryChance)` | void | 添加感应炉配方 |
| `.removeRecipe(IItemStack primaryInput, IItemStack secondaryInput)` | void | 按输入移除配方 |

### RedstoneFurnace（红石炉）

> `import mods.thermalexpansion.RedstoneFurnace;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, int energy)` | void | 添加配方 |
| `.removeRecipe(IItemStack input)` | void | 按输入移除配方 |
| `.addPyrolysisRecipe(IItemStack output, IItemStack input, int energy, int creosote)` | void | 添加热解配方（焦化增强）。**注意**: 实际能量 = energy × 1.5 |
| `.removePyrolysisRecipe(IItemStack input)` | void | 移除热解配方 |

### Crucible（熔岩炉）

> `import mods.thermalexpansion.Crucible;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, IItemStack input, int energy)` | void | 添加配方（物品→流体） |
| `.removeRecipe(IItemStack input)` | void | 按输入移除配方 |

### Transposer（流体转置机）

> `import mods.thermalexpansion.Transposer;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addExtractRecipe(ILiquidStack output, IItemStack input, int energy)` | void | 添加抽取配方（物品→流体） |
| `.addExtractRecipe(ILiquidStack output, IItemStack input, int energy, WeightedItemStack itemOut)` | void | 添加抽取配方（带副产物） |
| `.addFillRecipe(IItemStack output, IItemStack input, ILiquidStack fluid, int energy)` | void | 添加灌装配方（流体+物品→物品） |
| `.removeExtractRecipe(IItemStack input)` | void | 移除抽取配方 |
| `.removeFillRecipe(IItemStack input, ILiquidStack fluid)` | void | 移除灌装配方 |

### Enchanter（附魔机）

> `import mods.thermalexpansion.Enchanter;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, IItemStack secondInput, int energy, int experience, boolean empowered)` | void | 添加附魔配方 |
| `.removeRecipe(IItemStack input, IItemStack secondInput)` | void | 按输入移除配方 |

### Infuser（能量灌注机）

> `import mods.thermalexpansion.Infuser;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, int energy)` | void | 添加配方 |
| `.removeRecipe(IItemStack input)` | void | 按输入移除配方 |

### Centrifuge（离心机）

> `import mods.thermalexpansion.Centrifuge;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(WeightedItemStack[] outputs, IItemStack input, ILiquidStack fluid, int energy)` | void | 添加离心配方 |
| `.addRecipeMob(IEntityDefinition entity, WeightedItemStack[] outputs, @Nullable ILiquidStack fluid, int energy, int xp)` | void | 添加实体离心配方。`fluid` 为 null 则使用默认经验液 |
| `.removeRecipe(IItemStack input)` | void | 按输入移除配方 |
| `.removeRecipeMob(IEntityDefinition entity)` | void | 按实体移除配方 |

### Compactor（压缩机）

> `import mods.thermalexpansion.Compactor;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addMintRecipe(IItemStack output, IItemStack input, int energy)` | void | 添加铸币配方（需铸币冲压增强） |
| `.removeMintRecipe(IItemStack input)` | void | 移除铸币配方 |
| `.addPressRecipe(IItemStack output, IItemStack input, int energy)` | void | 添加冲压配方 |
| `.removePressRecipe(IItemStack input)` | void | 移除冲压配方 |
| `.addStorageRecipe(IItemStack output, IItemStack input, int energy)` | void | 添加存储配方（板） |
| `.removeStorageRecipe(IItemStack input)` | void | 移除存储配方 |
| `.addGearRecipe(IItemStack output, IItemStack input, int energy)` | void | 添加齿轮配方（需齿轮加工增强） |
| `.removeGearRecipe(IItemStack input)` | void | 移除齿轮配方 |

### Insolator（有机灌注机）

> `import mods.thermalexpansion.Insolator;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack primaryOutput, IItemStack primaryInput, IItemStack secondaryInput, int energy, @Optional IItemStack secondaryOutput, @Optional int secondaryChance, @Optional int water)` | void | 添加配方 |
| `.addRecipeSaplingInfuser(IItemStack primaryOutput, IItemStack primaryInput, IItemStack secondaryInput, int energy, @Optional IItemStack secondaryOutput, @Optional int secondaryChance, @Optional int water)` | void | 添加树苗注入配方 |
| `.removeRecipe(IItemStack primaryInput, IItemStack secondaryInput)` | void | 按输入移除配方 |

### Refinery（药水精炼）

> `import mods.thermalexpansion.Refinery;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, WeightedItemStack outputItem, ILiquidStack input, int energy)` | void | 添加精炼配方 |
| `.addRecipePotion(ILiquidStack output, ILiquidStack input, int energy)` | void | 添加药水精炼配方（炼金蒸馏增强） |
| `.removeRecipe(ILiquidStack input)` | void | 移除精炼配方 |
| `.removeRecipePotion(ILiquidStack input)` | void | 移除药水精炼配方 |

### Imbuer（药水酿造机）

> `import mods.thermalexpansion.Imbuer;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, IItemStack input, ILiquidStack inputFluid, int energy)` | void | 添加配方 |
| `.removeRecipe(IItemStack input, ILiquidStack secondInput)` | void | 按输入移除配方 |

### Factorizer（公式处理器）

> `import mods.thermalexpansion.Factorizer;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipeSplit(IItemStack in, IItemStack out)` | void | 添加单向分解配方 |
| `.addRecipeCombine(IItemStack in, IItemStack out)` | void | 添加单向合成配方 |
| `.addRecipeBoth(IItemStack combined, IItemStack split)` | void | 添加双向配方 |
| `.removeRecipeSplit(IItemStack in)` | void | 移除分解配方 |
| `.removeRecipeCombine(IItemStack in)` | void | 移除合成配方 |

### Coolant（冷却剂管理器）

> `import mods.thermalexpansion.Coolant;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addCoolant(ILiquidStack fluid, int coolantRf, int coolantFactor)` | void | 添加冷却剂。`coolantRf` 非负。`coolantFactor` 1-100 |
| `.removeCoolant(ILiquidStack fluid)` | void | 移除冷却剂 |

### 发电机动态方法

#### CompressionDynamo（压缩能源炉）

> `import mods.thermalexpansion.CompressionDynamo;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(ILiquidStack stack, int energy)` | void | 添加燃料。`energy` 范围 10000-200000000 |
| `.removeFuel(ILiquidStack stack)` | void | 移除燃料 |

#### EnervationDynamo（弱化能源炉）

> `import mods.thermalexpansion.EnervationDynamo;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(IItemStack stack, int energy)` | void | 添加燃料。`energy` 范围 2000-200000000 |
| `.removeFuel(IItemStack stack)` | void | 移除燃料 |

#### MagmaticDynamo（热力能源炉）

> `import mods.thermalexpansion.MagmaticDynamo;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(ILiquidStack stack, int energy)` | void | 添加燃料。`energy` 范围 10000-200000000 |
| `.removeFuel(ILiquidStack stack)` | void | 移除燃料 |

#### NumismaticDynamo（通货能源炉）

> `import mods.thermalexpansion.NumisticDynamo;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(IItemStack stack, int energy)` | void | 添加燃料。`energy` 范围 2000-200000000 |
| `.addGemFuel(IItemStack stack, int energy)` | void | 添加宝石燃料 |
| `.removeFuel(IItemStack stack)` | void | 移除燃料 |
| `.removeGemFuel(IItemStack stack)` | void | 移除宝石燃料 |

#### ReactantDynamo（反应能源炉）

> `import mods.thermalexpansion.ReactantDynamo;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addReaction(IItemStack item, ILiquidStack liquid, int energy)` | void | 添加反应。`energy` 范围 10000-200000000 |
| `.addReactionElemental(IItemStack item, ILiquidStack liquid, int energy)` | void | 添加元素反应 |
| `.removeReaction(IItemStack item, ILiquidStack liquid)` | void | 移除反应 |
| `.removeReactionElemental(IItemStack item, ILiquidStack liquid)` | void | 移除元素反应 |

#### SteamDynamo（蒸汽能源炉）

> `import mods.thermalexpansion.SteamDynamo;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(IItemStack stack, int energy)` | void | 添加燃料。`energy` 范围 2000-200000000 |
| `.removeFuel(IItemStack stack)` | void | 移除燃料 |

## 使用示例

### 添加粉碎机配方

```zenscript
import mods.thermalexpansion.Pulverizer;

Pulverizer.addRecipe(<minecraft:diamond>, <minecraft:stick>, 1500, <minecraft:stone>, 20);
```

### 添加感应炉配方

```zenscript
import mods.thermalexpansion.InductionSmelter;

InductionSmelter.addRecipe(<minecraft:diamond>, <minecraft:stick>, <minecraft:iron_ore>, 1500, <minecraft:stone>, 20);
```

### 添加流体转置机配方

```zenscript
import mods.thermalexpansion.Transposer;

Transposer.addFillRecipe(<minecraft:leaves:1>, <minecraft:leaves:0>, <liquid:water> * 200, 20);
```
