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

---

## Roids-Tweaker 扩展（需安装 Roids-Tweaker）

> `import mods.immersiveengineering.ArcFurnace;`
> `import mods.immersiveengineering.Blueprint;`
> `import mods.immersiveengineering.Excavator;`
> `import mods.immersiveengineering.MetalPress;`
> `import mods.immersiveengineering.MineralMix;`
> `import mods.immersiveengineering.SlagReplacer;`
> `import mods.roidtweaker.immersiveengineering.GardenCloche;`

### ArcFurnace 扩展

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecycling(IIngredient ingredient)` | void | 将物品添加到电弧炉回收白名单，IE 会自动添加默认回收配方 |
| `.removeRecyclingOutput(IIngredient ingredient)` | void | 移除所有输出匹配的回收配方 |

### Blueprint 扩展

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getRegisteredBlueprints()` | string[] | 获取所有已注册的蓝图类型 |
| `.addBlueprint(String type)` | void | 添加蓝图类型。`addRecipe` 已自动创建，此方法用于 `getRegisteredBlueprints` |
| `.addVillagerTrade(String category, IItemStack price)` | void | 添加 IE 村民可出售的蓝图 |

蓝图的翻译键为 `desc.immersiveengineering.info.blueprint.[蓝图名]`，若无则回退到蓝图的原始类型名。

### Excavator 扩展

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getRegisteredMinerals()` | List\<MineralMix\> | 获取所有已注册矿物 |

### GardenCloche（温室）

> `import mods.roidtweaker.immersiveengineering.GardenCloche;`

额外支持命令 `/ct gardencloche [fluidFertilizers 或 crop]` 打印所有作物或液体肥料。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFertilizer(IIngredient fertilizer, float multiplier)` | void | 添加肥料，支持 IIngredient（包括 ILiquidStack 和物品条件） |
| `.addFertilizer(IIngredient fertilizer, GardenClocheMultiplierFunction multiplier)` | void | IE 需要乘数时调用此函数，第一个参数始终是 IItemStack 或 ILiquidStack |
| `.RemoveFertilizer(IIngredient fertilizer)` | void | 移除肥料。必须可转换为 List\<IItemStack\> 或 List\<IFluidStack\> |
| `.clearFertilizers(@Optional Boolean restrictionReadWiki)` | void | false=仅流体，true=仅物品，不指定=全部清除 |
| `.listAllFluidFertilizers()` | List\<String\> | 列出所有液体肥料（仅用于 ZenCloche 兼容，不要在脚本中调用） |
| `.listAllCrops()` | List\<String\> | 列出所有作物（仅用于 ZenCloche 兼容，不要在脚本中调用） |
| `.addPlantHandler(String type)` | void | 添加植物处理器 |
| `.addCrop(String type, IIngredient seed, IItemStack[] drops, @Optional IIngredient soil, @Optional IBlock display)` | void | 添加作物。默认类型："crop"、"stem"、"stacking"，默认土壤：泥土，默认显示：作物方块 |
| `.addCrop(String type, IIngredient seed, IItemStack[] drops, IIngredient soil, IBlockState display)` | void | 同上，但可指定方块状态 |
| `.removeCrop(IIngredient crop, @Optional String type)` | void | 移除作物。未指定类型则从所有包含该种子的类型中移除 |
| `.setSoilTexture(IIngredient soil, String texture)` | void | 设置土壤纹理。支持 IOreDictEntry 和 IItemStack，格式为 `namespace:path` |

### GardenClocheMultiplierFunction

> `import mods.roidtweaker.immersiveengineering.GardenClocheMultiplierFunction;`

函数签名为 `function(fertilizer as IIngredient, seed as IItemStack, soil as IItemStack) as float`。

### IWorld 扩展

> `import crafttweaker.world.IWorld;`

#### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getMineralMix(IBlockPos pos)` | pos | MineralMix | 获取指定位置的矿物混合 |
| `.setMineralMix(IBlockPos pos, MineralMix mix)` | pos, mix | void | 设置指定位置的矿物混合 |
| `.getMineralMap()` | 无 | MineralMix[][IBlockPos] | 获取矿物映射（为 MineralMixTweaker 兼容保留，推荐使用上述方法） |

### MetalPress 扩展

支持 NBT 敏感配方。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipeNBT(IItemStack output, IIngredient input, IItemStack mold, int energy)` | void | 添加 NBT 敏感的冲压配方 |

### MineralMix 扩展

通过 `Excavator.getMineral()` 获取 MineralMix 对象后可调用以下方法。

#### @ZenCaster

| 方法 | 返回 | 说明 |
|------|------|------|
| `.toString()` | string | 返回矿物名称 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.printRegisteredMinerals()` | void | 打印所有已注册矿物 |
| `.setWeight(int weight)` | void | 设置权重 |
| `.setDimensionWhitelist(int[] list)` | void | 设置维度白名单 |
| `.setDimensionBlacklist(int[] list)` | void | 设置维度黑名单 |
| `.getWeight()` | int | 获取权重 |
| `.getOres()` | WeightedOreDictEntry[] | 获取矿石列表 |
| `.getDimensionWhitelist()` | int[] | 获取维度白名单 |
| `.getDimensionBlacklist()` | int[] | 获取维度黑名单 |

### SlagReplacer（矿渣替换器）

> `import mods.immersiveengineering.SlagReplacer;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setSlag(IItemStack slag, @Optional IIngredient filter, @Optional String filterBy)` | void | 替换高炉和电弧炉配方中的矿渣。filter 默认 `<*>`，filterBy 接受 `OUTPUT` 或 `SLAG`（默认 `OUTPUT`）。遍历所有配方并按条件替换 |