# Integrated Dynamics CraftTweaker API 参考

> Mod ID: `integrateddynamics`
> 前置条件: 无
> 导入: `import mods.integrateddynamics.<ClassName>;`

Integrated Dynamics 是一个基于逻辑和自动化的模组。

---

## API 列表

### DryingBasin（烘干池）

> `import mods.integrateddynamics.DryingBasin;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(@Optional IItemStack inputStack, @Optional ILiquidStack inputFluid, @Optional IItemStack outputStack, @Optional ILiquidStack outputFluid, @Optional(10) int duration)` | void | 添加配方。所有参数可选，`duration` 默认 10 |
| `.removeRecipe(@Optional IItemStack inputStack, @Optional ILiquidStack inputFluid, @Optional IItemStack outputStack, @Optional ILiquidStack outputFluid, @Optional(10) int duration)` | void | 移除配方 |
| `.removeRecipesWithOutput(@Optional IItemStack outputStack, @Optional ILiquidStack outputFluid)` | void | 按输出移除配方 |

---

### MechanicalDryingBasin（电动烘干池）

> `import mods.integrateddynamics.MechanicalDryingBasin;`

API 与 DryingBasin 完全一致。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(@Optional IItemStack inputStack, @Optional ILiquidStack inputFluid, @Optional IItemStack outputStack, @Optional ILiquidStack outputFluid, @Optional(10) int duration)` | void | 添加配方 |
| `.removeRecipe(@Optional IItemStack inputStack, @Optional ILiquidStack inputFluid, @Optional IItemStack outputStack, @Optional ILiquidStack outputFluid, @Optional(10) int duration)` | void | 移除配方 |
| `.removeRecipesWithOutput(@Optional IItemStack outputStack, @Optional ILiquidStack outputFluid)` | void | 按输出移除配方 |

---

### Squeezer（挤压机）

> `import mods.integrateddynamics.Squeezer;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack inputStack, @Optional IItemStack outputStack, @Optional ILiquidStack outputFluid)` | void | 添加单输出配方 |
| `.addRecipe(IItemStack inputStack, @Optional IItemStack outputStack1, @Optional float outputStackChance1, @Optional IItemStack outputStack2, @Optional float outputStackChance2, @Optional IItemStack outputStack3, @Optional float outputStackChance3, @Optional ILiquidStack outputFluid)` | void | 添加多输出配方（最多 3 个物品输出，带概率） |
| `.removeRecipe(IItemStack inputStack, @Optional IItemStack outputStack, @Optional ILiquidStack outputFluid)` | void | 移除单输出配方 |
| `.removeRecipe(IItemStack inputStack, @Optional IItemStack outputStack1, @Optional float outputStackChance1, @Optional IItemStack outputStack2, @Optional float outputStackChance2, @Optional IItemStack outputStack3, @Optional float outputStackChance3, @Optional ILiquidStack outputFluid)` | void | 移除多输出配方 |
| `.removeRecipesWithOutput(@Optional IItemStack outputStack, @Optional ILiquidStack outputFluid)` | void | 按输出移除配方 |
| `.removeRecipesWithOutput(@Optional IItemStack outputStack1, @Optional float outputStackChance1, @Optional IItemStack outputStack2, @Optional float outputStackChance2, @Optional IItemStack outputStack3, @Optional float outputStackChance3, @Optional ILiquidStack outputFluid)` | void | 按多输出移除配方 |

---

### MechanicalSqueezer（电动挤压机）

> `import mods.integrateddynamics.MechanicalSqueezer;`

API 与 Squeezer 类似，但多了 `duration` 参数。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack inputStack, @Optional IItemStack outputStack, @Optional ILiquidStack outputFluid, @Optional(10) int duration)` | void | 添加单输出配方 |
| `.addRecipe(IItemStack inputStack, @Optional IItemStack outputStack1, @Optional float outputStackChance1, @Optional IItemStack outputStack2, @Optional float outputStackChance2, @Optional IItemStack outputStack3, @Optional float outputStackChance3, @Optional ILiquidStack outputFluid, @Optional(10) int duration)` | void | 添加多输出配方 |
| `.removeRecipe(IItemStack inputStack, @Optional IItemStack outputStack, @Optional ILiquidStack outputFluid, @Optional(10) int duration)` | void | 移除单输出配方 |
| `.removeRecipe(IItemStack inputStack, @Optional IItemStack outputStack1, @Optional float outputStackChance1, @Optional IItemStack outputStack2, @Optional float outputStackChance2, @Optional IItemStack outputStack3, @Optional float outputStackChance3, @Optional ILiquidStack outputFluid, @Optional(10) int duration)` | void | 移除多输出配方 |
| `.removeRecipesWithOutput(@Optional IItemStack outputStack, @Optional ILiquidStack outputFluid)` | void | 按输出移除配方 |
| `.removeRecipesWithOutput(@Optional IItemStack outputStack1, @Optional float outputStackChance1, @Optional IItemStack outputStack2, @Optional float outputStackChance2, @Optional IItemStack outputStack3, @Optional float outputStackChance3, @Optional ILiquidStack outputFluid)` | void | 按多输出移除配方 |