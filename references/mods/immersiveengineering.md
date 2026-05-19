# Immersive Engineering CraftTweaker API 参考

> Mod ID: `immersiveengineering`
> 前置条件: 无
> 导入: `import mods.immersiveengineering.<ClassName>;`

Immersive Engineering 是一个以写实风格为特色的科技模组，包含多方块结构机器和电力系统。

---

## API 列表

### AlloySmelter（合金窑）

> `import mods.immersiveengineering.AlloySmelter;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient first, IIngredient second, int time)` | void | 添加合金配方 |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |

---

### ArcFurnace（电弧炉）

> `import mods.immersiveengineering.ArcFurnace;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input, IItemStack slag, int time, int energyPerTick, @Optional IIngredient[] additives, @Optional String specialRecipeType)` | void | 添加电弧炉配方。`specialRecipeType` 可选值：`"Alloying"`、`"Ores"` |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |

---

### BlastFurnace（高炉）

> `import mods.immersiveengineering.BlastFurnace;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input, int time, @Optional IItemStack slag)` | void | 添加高炉配方 |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |
| `.addFuel(IIngredient input, int time)` | void | 添加高炉燃料 |
| `.removeFuel(IItemStack output)` | void | 移除高炉燃料 |

---

### Blueprint（蓝图）

> `import mods.immersiveengineering.Blueprint;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String category, IItemStack output, IIngredient[] inputs)` | void | 添加蓝图配方。`category` 不存在时会创建新蓝图类别。已有类别：`components`、`molds`、`bullet`、`specialBullet`、`electrode` |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |

---

### BottlingMachine（灌装机）

> `import mods.immersiveengineering.BottlingMachine;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input, ILiquidStack fluid)` | void | 添加灌装配方 |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |

---

### CokeOven（焦炉）

> `import mods.immersiveengineering.CokeOven;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, int fuelOutput, IIngredient input, int time)` | void | 添加焦炉配方。`fuelOutput` 为燃料输出量 |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |

---

### Crusher（粉碎机）

> `import mods.immersiveengineering.Crusher;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input, int energy, @Optional IItemStack secondaryOutput, @Optional double secondaryChance)` | void | 添加粉碎配方。`secondaryChance` 为副产品概率（0-1） |
| `.removeRecipe(IItemStack output)` | void | 按输出移除配方 |
| `.removeRecipesForInput(IItemStack input)` | void | 按输入移除配方 |

---

### DieselHandler（柴油处理）

> `import mods.immersiveengineering.DieselHandler;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(ILiquidStack fuel, int time)` | void | 添加柴油发电机燃料 |
| `.removeFuel(ILiquidStack fuel)` | void | 移除柴油发电机燃料 |
| `.addDrillFuel(ILiquidStack fuel)` | void | 添加钻头燃料 |
| `.removeDrillFuel(ILiquidStack fuel)` | void | 移除钻头燃料 |

---

### Excavator（斗轮式挖掘机）

> `import mods.immersiveengineering.Excavator;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addMineral(String name, int mineralWeight, double failChance, String[] ores, double[] chances, @Optional int[] dimensionWhitelist, @Optional boolean blacklist)` | void | 添加矿物。`mineralWeight` 为权重，`failChance` 为失败概率，`ores` 为矿辞数组，`chances` 为概率数组，`dimensionWhitelist` 为维度白名单，`blacklist` 为是否黑名单模式 |
| `.removeMineral(String name)` | void | 移除矿物 |
| `.getMineral(String name)` | MineralMix | 获取矿物对象 |

---

### MineralMix（矿物混合）

> `import mods.immersiveengineering.MineralMix;`

通过 `Excavator.getMineral()` 获取。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `failChance` | double | 失败概率 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addOre(String ore, double chance)` | void | 添加矿石（使用矿辞名） |
| `.removeOre(String ore)` | void | 移除矿石 |

---

### Fermenter（工业发酵机）

> `import mods.immersiveengineering.Fermenter;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, ILiquidStack fluid, IIngredient input, int energy)` | void | 添加发酵配方 |
| `.removeFluidRecipe(ILiquidStack fluid)` | void | 按流体输出移除配方 |
| `.removeItemRecipe(IItemStack output)` | void | 按物品输出移除配方 |
| `.removeByInput(IItemStack input)` | void | 按输入移除配方 |

---

### MetalPress（金属冲压机）

> `import mods.immersiveengineering.MetalPress;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input, IItemStack mold, int energy, @Optional int inputSize)` | void | 添加冲压配方 |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |
| `.removeRecipeByMold(IItemStack mold)` | void | 按模具移除配方 |

---

### Mixer（搅拌机）

> `import mods.immersiveengineering.Mixer;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, ILiquidStack fluidInput, IIngredient[] itemInputs, int energy)` | void | 添加搅拌配方 |
| `.removeRecipe(ILiquidStack output)` | void | 移除配方 |

---

### Refinery（精炼厂）

> `import mods.immersiveengineering.Refinery;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, ILiquidStack input0, ILiquidStack input1, int energy)` | void | 添加精炼配方 |
| `.removeRecipe(ILiquidStack output)` | void | 移除配方 |

---

### Squeezer（工业挤压机）

> `import mods.immersiveengineering.Squeezer;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, ILiquidStack fluid, IIngredient input, int energy)` | void | 添加压榨配方 |
| `.removeFluidRecipe(ILiquidStack fluid)` | void | 按流体输出移除配方 |
| `.removeItemRecipe(IItemStack output)` | void | 按物品输出移除配方 |
| `.removeByInput(IItemStack input)` | void | 按输入移除配方 |

---

### Thermoelectric（热传导发电机）

> `import mods.immersiveengineering.Thermoelectric;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addTemperatureSource(IIngredient source, int temperature)` | void | 添加热源（温度单位：开尔文） |
| `.removeTemperatureSource(IIngredient source)` | void | 移除热源 |