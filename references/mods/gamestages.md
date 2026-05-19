# GameStages CraftTweaker API 参考

> Mod ID: `gamestages`
> 前置条件: 无（部分功能需要安装对应子模组）
> 导入: 见各子模组章节

GameStages 是一个阶段模组，允许玩家解锁阶段，其他模组可以挂钩到这些阶段。此文档包含 GameStages 及其所有子模组的 CraftTweaker API。

---

## Player Stages（玩家阶段）

扩展 IPlayer 接口，可直接在任何 IPlayer 对象上调用。

### 检查阶段方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.hasGameStage(String stage)` | bool | 检查玩家是否拥有指定阶段 |
| `.hasAnyGameStages(String... stages)` | bool | 检查玩家是否拥有任意一个指定阶段 |
| `.hasAllGameStages(String... stages)` | bool | 检查玩家是否拥有所有指定阶段 |

### 添加/移除阶段方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGameStage(String stage)` | void | 为玩家解锁一个阶段 |
| `.removeGameStage(String stage)` | void | 移除玩家的一个已解锁阶段 |

---

## DimensionStages（维度阶段）

> `import mods.DimensionStages;`

限制玩家进入特定维度，除非拥有对应阶段。

### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addDimensionStage(String stage, int dimensionId)` | void | 将指定维度锁定在某个阶段后 |

---

## ItemStages（物品阶段）

> `import mods.ItemStages;`

将物品、方块、流体、附魔等放入自定义进度系统。如果玩家没有对应阶段，将无法正常使用该物品。

### 物品阶段方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addItemStage(String stage, IItemStack item)` | void | 将单个物品/方块锁定到阶段 |
| `.addItemStage(String stage, IOreDictEntry oreDict)` | void | 将矿辞下的所有物品锁定到阶段 |
| `.stageModItems(String stage, String modId)` | void | 将指定模组的所有物品锁定到阶段 |
| `.removeItemStage(IItemStack item)` | void | 移除物品的阶段锁定 |

### 流体阶段方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.stageLiquid(String stage, ILiquidStack liquid)` | void | 将流体锁定到阶段（主要用于 JEI 隐藏） |

### 附魔阶段方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.stageEnchant(String stage, IEnchantment enchant)` | void | 将附魔锁定到阶段 |
| `.stageEnchantByLevel(String stage, IEnchantment enchant)` | void | 将指定等级的附魔锁定到阶段 |

### 显示控制方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setUnfamiliarName(String name, IItemStack item)` | void | 设置物品在未解锁阶段时显示的名称 |
| `.stageTooltip(String stage, String prefix)` | void | 隐藏以指定前缀开头的提示行 |
| `.stageRecipeCategory(String stage, String category)` | void | 将 JEI 配方分类锁定到阶段 |

---

## MobStages（生物阶段）

> `import mods.MobStages;`

控制生物生成，将其配置到自定义进度系统中。

### 全局方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addStage(String stage, String entityId)` | void | 为生物创建全局阶段条目（每个生物只能有一个） |
| `.addReplacement(String entityId, String replacementId)` | void | 设置生物无法生成时的替代生物 |
| `.addRange(String entityId, int range)` | void | 设置搜索有效玩家的范围（默认 512 格） |
| `.toggleSpawner(String entityId, boolean allow)` | void | 设置刷怪笼是否可以绕过阶段检查（默认 false） |

### 维度特定方法

维度特定方法与全局方法相同，但额外添加一个 int dimensionId 参数。维度特定条目会覆盖该维度的全局条目。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addStage(String stage, String entityId, int dimension)` | void | 在指定维度为生物设置阶段 |
| `.addReplacement(String entityId, String replacementId, int dimension)` | void | 在指定维度设置替代生物 |
| `.toggleSpawner(String entityId, boolean allow, int dimension)` | void | 在指定维度设置刷怪笼是否绕过阶段检查 |

---

## RecipeStages（配方阶段）

> `import mods.recipestages.Recipes;`

允许合成台配方被自定义进度系统限制。

### 添加配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addShaped(String stage, IItemStack output, IIngredient[][] ingredients, @Optional IRecipeFunction function, @Optional IRecipeAction action)` | void | 添加有阶段锁定的有序配方 |
| `.addShaped(String name, String stage, IItemStack output, IIngredient[][] ingredients, @Optional IRecipeFunction function, @Optional IRecipeAction action)` | void | 添加有名称和阶段锁定的有序配方 |
| `.addShapedMirrored(String stage, IItemStack output, IIngredient[][] ingredients, @Optional IRecipeFunction function, @Optional IRecipeAction action)` | void | 添加有阶段锁定的镜像有序配方 |
| `.addShapedMirrored(String name, String stage, IItemStack output, IIngredient[][] ingredients, @Optional IRecipeFunction function, @Optional IRecipeAction action)` | void | 添加有名称和阶段锁定的镜像有序配方 |
| `.addShapeless(String stage, IItemStack output, IIngredient[] ingredients, @Optional IRecipeFunction function, @Optional IRecipeAction action)` | void | 添加有阶段锁定的无序配方 |
| `.addShapeless(String name, String stage, IItemStack output, IIngredient[] ingredients, @Optional IRecipeFunction function, @Optional IRecipeAction action)` | void | 添加有名称和阶段锁定的无序配方 |

### 设置配方阶段方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setRecipeStage(String name, IItemStack output)` | void | 将已有配方的输出物品设置到阶段 |
| `.setRecipeStage(String name, String recipeName)` | void | 将指定配方名设置到阶段 |
| `.setRecipeStageByMod(String name, String modId)` | void | 将指定模组的所有配方设置到阶段（不支持正则） |
| `.setRecipeStageByRegex(String name, String regex)` | void | 将匹配正则表达式的配方名设置到阶段 |

### 容器控制方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setPrintContainers(boolean printContainers)` | void | 设置是否在聊天中打印容器名称 |
| `.setContainerStage(String containerPath, String[] stages)` | void | 设置容器可以制作物品的阶段 |
| `.setPackageStage(String packageName, String[] stages)` | void | 设置包中所有容器可以制作物品的阶段 |

---

## Tiered_Tooltips（分层提示）

> `import mods.tieredtooltips;` (1.0.4+)
> `import mods.TieredTooltips;` (1.0.2 及更早版本)

根据物品锁定的阶段改变提示框颜色。

### 方法（1.0.4+）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.colorStage(String stageName, String background, String borderStart, String borderEnd)` | void | 设置阶段的提示框颜色（RGB/ARGB 十六进制值） |

### 方法（1.0.2 及更早）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.colourStage(String stageName, String background, String borderStart, String borderEnd)` | void | 设置阶段的提示框颜色（RGB/ARGB 十六进制值） |

---

## TinkerStages（匠魂阶段）

> `import mods.TinkerStages;`

将匠魂模组的各个方面放入自定义进度系统。

### 通用限制方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGeneralCraftingStage(String stage)` | void | 限制工具制作需要阶段（多个阶段只需拥有一个） |
| `.addGeneralPartReplacingStage(String stage)` | void | 限制部件替换需要阶段 |
| `.addGeneralPartBuildingStage(String stage)` | void | 限制部件制作需要阶段 |
| `.addGeneralModifierStage(String stage)` | void | 限制应用修改器需要阶段 |

### 特定限制方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addToolTypeStage(String stage, String toolId)` | void | 限制特定工具类型的制作（如 `tconstruct:pickaxe`） |
| `.addMaterialStage(String stage, String material)` | void | 限制材料的使用（包括制作、部件制作和使用） |
| `.addModifierStage(String stage, String modifier)` | void | 限制修改器的应用和使用 |

---

## WailaStages（Waila 阶段）

> `import mods.WailaStages;`
> `import mods.WailaProgression;`

限制 Waila/Hwyla HUD 的显示。

### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `mods.WailaStages.addWailaStage(String stage)` | void | 隐藏整个 HUD，除非玩家拥有阶段 |
| `mods.WailaProgression.addRequirement(String stage, String prefix)` | void | 隐藏特定行，除非玩家拥有阶段 |

---

## ZenStages（Zen 阶段管理器）

> `import mods.zenstages.ZenStager;`
> `import mods.zenstages.Stage;`

ZenStages 是 GameStages 子模组的统一管理工具，提供简单集成和调试功能。

### ZenStager 类

#### 创建/获取阶段

| 方法 | 返回 | 说明 |
|------|------|------|
| `.initStage(String stageName)` | Stage | 创建并返回新阶段 |
| `.getStage(String stageName)` | Stage | 获取已创建的阶段（不存在返回 null） |
| `.getStageMap()` | Stage[string] | 获取所有已创建阶段的映射 |

#### 获取阶段信息

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getStagedLiquids()` | ILiquidStack[][string] | 获取已阶段化的流体映射 |
| `.getIngredientStage(IIngredient ingredient)` | Stage | 获取物品的阶段（未阶段化返回 null） |
| `.getLiquidStage(ILiquidStack liquidStack)` | Stage | 获取流体的阶段 |
| `.getRecipeNameStage(String recipeName)` | Stage | 获取配方名的阶段（需要 RecipeStages） |
| `.getContainerStages(String containerName)` | Stage | 获取容器的阶段（需要 RecipeStages） |
| `.getPackageStages(String packageName)` | Stage | 获取包的阶段（需要 RecipeStages） |
| `.getDimensionStage(int dimId)` | Stage | 获取维度的阶段（需要 DimStages） |
| `.getMobStage(String mobName)` | Stage | 获取生物的阶段（需要 MobStages） |
| `.getTiCMaterialStage(String material)` | Stage | 获取匠魂材料的阶段（需要 TinkerStages） |

#### 包/容器阶段方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addPackage(String packageName, Stage[] stages)` | void | 设置包的阶段（需要 RecipeStages） |
| `.addContainer(String containerPath, Stage[] stages)` | void | 设置容器的阶段（需要 RecipeStages） |

#### 检查是否已阶段化

| 方法 | 返回 | 说明 |
|------|------|------|
| `.isStaged(String type, String value)` | bool | 检查指定类型和值是否已阶段化 |
| `.isStaged(String type, int value)` | bool | 检查指定类型和整数值是否已阶段化 |
| `.isStaged(String type, IIngredient value)` | bool | 检查指定类型和物品是否已阶段化 |

支持的类型：container、dimension、ingredient、mob、mod、multiblock、ore、package、recipename、tinker

#### 调试方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.checkConflicts()` | void | 检查是否有重复阶段化的条目，结果记录到 crafttweaker.log |

#### 构建方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.buildAll()` | void | **必须调用** - 完成阶段配置后调用，使所有阶段生效 |

---

### Stage 类

> `import mods.zenstages.Stage;`

Stage 类在使用 ZenStager.initStage() 创建阶段时获得，用于向阶段添加条目。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `stage` | string | 返回阶段名称 |

#### 添加物品方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addIngredient(IIngredient ingredient, @Optional boolean recipeStage)` | void | 添加物品到阶段（recipeStage 默认 true，同时阶段化配方） |
| `.addIngredients(IIngredient[] ingredients, @Optional boolean recipeStage)` | void | 添加多个物品到阶段 |
| `.addIngredientOverride(IIngredient ingredient, @Optional boolean recipeStage)` | void | 添加物品覆盖（用于从模组阶段化中重新阶段化特定物品） |

#### 添加模组方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addModId(String modId)` | void | 将模组的所有物品添加到阶段 |
| `.addModId(String[] modIds)` | void | 将多个模组的所有物品添加到阶段 |
| `.addModId(String modId, IIngredient[] ignoreStaging)` | void | 将模组物品添加到阶段，排除指定物品 |

#### 添加流体方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addLiquid(ILiquidStack liquidStack)` | void | 添加流体到阶段 |
| `.addLiquids(ILiquidStack[] liquidStacks)` | void | 添加多个流体到阶段 |

#### 添加维度方法（需要 DimStages）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addDimension(int dimId)` | void | 添加维度到阶段 |

#### 添加配方方法（需要 RecipeStages）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipeName(String recipeName)` | void | 添加配方名到阶段 |
| `.addRecipeRegex(String regex)` | void | 添加匹配正则的配方名到阶段 |

#### 添加生物方法（需要 MobStages）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addMob(String mobName)` | void | 添加生物到阶段 |
| `.addMobs(String[] mobNames)` | void | 添加多个生物到阶段 |
| `.addMob(String mobName, int dimId)` | void | 在指定维度添加生物到阶段 |
| `.addMobs(String[] mobNames, int dimId)` | void | 在指定维度添加多个生物到阶段 |

#### 添加匠魂方法（需要 TinkerStages）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addTiCMaterial(String materialName)` | void | 添加匠魂材料到阶段 |
| `.addTiCMaterials(String[] materialNames)` | void | 添加多个匠魂材料到阶段 |
| `.addTiCModifier(String modifierName)` | void | 添加匠魂修改器到阶段 |

#### 添加 IE 多方块方法（需要 MultiBlock Stages）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addIEMultiBlock(String multiblock)` | void | 添加 IE 多方块到阶段 |
| `.addIEMultiBlocks(String[] multiblocks)` | void | 添加多个 IE 多方块到阶段 |

#### 添加矿石替换方法（需要 OreStages）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addOreReplacement(IIngredient blockToHide, @Optional boolean isNonDefaulting)` | void | 添加矿石替换（隐藏方块） |
| `.addOreReplacement(IIngredient blockToHide, IItemStack blockToShow, @Optional boolean isNonDefaulting)` | void | 添加矿石替换（隐藏方块并显示替代方块） |

#### 检查自定义类型方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.isCustomStaged(String slug, String value)` | bool | 检查自定义类型是否已阶段化到此阶段 |
| `.isCustomStaged(String slug, String[] values)` | bool | 检查多个自定义类型值 |
| `.isCustomStaged(String slug, int value)` | bool | 检查整数类型的自定义类型 |
| `.isCustomStaged(String slug, int[] values)` | bool | 检查多个整数类型的自定义类型 |
| `.isCustomStaged(String slug, IIngredient value)` | bool | 检查物品类型的自定义类型 |
| `.isCustomStaged(String slug, IIngredient[] values)` | bool | 检查多个物品类型的自定义类型 |

---

### CustomStageType（自定义阶段类型）

> `import mods.zenstages.type.CustomStageType;`

允许创建自定义阶段类型，用于阶段化事件、方块交互等。

#### 创建方法（通过 ZenStager）

| 方法 | 返回 | 说明 |
|------|------|------|
| `ZenStager.initCustomType(String name, String value)` | CustomStageType | 创建字符串类型的自定义类型 |
| `ZenStager.initCustomType(String name, String[] values)` | CustomStageType | 创建字符串数组类型的自定义类型 |
| `ZenStager.initCustomType(String name, int value)` | CustomStageType | 创建整数类型的自定义类型 |
| `ZenStager.initCustomType(String name, int[] values)` | CustomStageType | 创建整数数组类型的自定义类型 |
| `ZenStager.initCustomType(String name, IIngredient value)` | CustomStageType | 创建物品类型的自定义类型 |
| `ZenStager.initCustomType(String name, IIngredient[] values)` | CustomStageType | 创建物品数组类型的自定义类型 |

#### CustomStageType 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setStage(Stage stage)` | void | 将自定义类型分配到阶段 |

#### 查询方法（通过 ZenStager）

| 方法 | 返回 | 说明 |
|------|------|------|
| `ZenStager.getCustomStage(String name, String value)` | Stage | 获取自定义类型的阶段（需要先 setStage） |
| `ZenStager.getCustomStage(String name, int value)` | Stage | 获取整数类型自定义类型的阶段 |
| `ZenStager.getCustomStage(String name, IIngredient value)` | Stage | 获取物品类型自定义类型的阶段 |
| `ZenStager.getCustomType(String name)` | CustomStageType | 获取自定义类型（无需 setStage） |