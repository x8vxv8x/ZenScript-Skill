# IC2 Tweaker CraftTweaker API 参考

> Mod ID: `ic2`
> 前置条件: 无
> 导入: `import mods.ic2.<ClassName>;`

IC2 Tweaker 为 IndustrialCraft 2 提供 CraftTweaker 集成。

---

## API 列表

### BlastFurnace（高炉）

> `import mods.ic2.BlastFurnace;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack[] outputs, IIngredient input, int totalFluidCost, int time)` | void | 添加高炉配方。`totalFluidCost` 为每 tick 液化空气消耗（mB/tick），`time` 为总时间（tick） |

---

### BlockCutter（方块切割机）

> `import mods.ic2.BlockCutter;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input, @Optional int hardness)` | void | 添加配方。`hardness` 为刀片最低硬度要求（默认 0） |

---

### Canner（装罐机）

> `import mods.ic2.Canner;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addBottleRecipe(IItemStack output, IIngredient container, IIngredient filler)` | void | 添加瓶装配方。`container` 为被填充物，`filler` 为填充物 |
| `.addEnrichRecipe(ILiquidStack output, ILiquidStack input, IIngredient additive)` | void | 添加浓缩配方。`additive` 为添加剂 |

---

### Compressor（压缩机）

> `import mods.ic2.Compressor;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input)` | void | 添加压缩配方 |

---

### Electrolyzer（电解机）

> `import mods.ic2.Electrolyzer;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack[] outputs, ILiquidStack input, int power, @Optional int time)` | void | 添加电解配方。`outputs` 为输出数组（对应下-上-北-南-西-东方向，可省略尾部 null），`power` 为 EU/t 消耗，`time` 为时间（默认 200 tick） |

---

### Extractor（提取机）

> `import mods.ic2.Extractor;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input)` | void | 添加提取配方 |

---

### Fermenter（发酵机）

> `import mods.ic2.Fermenter;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, ILiquidStack input, int heat)` | void | 添加发酵配方。`heat` 为发酵所需热量 |

---

### HeatExchanger（流体热交换器）

> `import mods.ic2.HeatExchanger;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFluidCoolDown(ILiquidStack output, ILiquidStack input, int heat)` | void | 添加流体冷却配方 |
| `.addFluidCoolDown(ILiquidDefinition output, ILiquidDefinition input, int heat)` | void | 添加流体冷却配方（使用 ILiquidDefinition） |
| `.addFluidHeatUp(ILiquidStack output, ILiquidStack input, int heat)` | void | 添加流体加热配方 |
| `.addFluidHeatUp(ILiquidDefinition output, ILiquidDefinition input, int heat)` | void | 添加流体加热配方（使用 ILiquidDefinition） |

---

### Macerator（打粉机）

> `import mods.ic2.Macerator;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input)` | void | 添加粉碎配方 |

---

### MetalFormer（金属成型机）

> `import mods.ic2.MetalFormer;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addCuttingRecipe(IItemStack output, IIngredient input)` | void | 添加切割配方 |
| `.addExtrudingRecipe(IItemStack output, IIngredient input)` | void | 添加挤压配方 |
| `.addRollingRecipe(IItemStack output, IIngredient input)` | void | 添加辊压配方 |

---

### OreWasher（洗矿机）

> `import mods.ic2.OreWasher;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack[] outputs, IIngredient input, @Optional int water)` | void | 添加洗矿配方。`water` 为所需水量（mB，默认 1000） |

---

### Recycler（回收机）

> `import mods.ic2.Recycler;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addBlacklist(IIngredient ingredient)` | void | 添加回收机黑名单（该物品不会被回收为废料） |

---

### ScrapBox（废料箱）

> `import mods.ic2.ScrapBox;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addDrop(WeightedItemStack weightedItem)` | void | 添加废料箱掉落（百分比权重除以 100） |
| `.addDrop(IItemStack item, float weight)` | void | 添加废料箱掉落 |

---

### SemiFluidGenerator（半流质发电机）

> `import mods.ic2.SemiFluidGenerator;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFluid(ILiquidStack liquid, double powerOutput)` | void | 添加半流质燃料。`powerOutput` 为 EU/t 输出 |

---

### ThermalCentrifuge（热能离心机）

> `import mods.ic2.ThermalCentrifuge;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack[] outputs, IIngredient input, @Optional int minHeat)` | void | 添加热能离心配方。`minHeat` 为最低热量要求 |