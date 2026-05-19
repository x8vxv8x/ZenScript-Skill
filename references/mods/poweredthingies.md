# Powered Thingies CraftTweaker API 参考

> Mod ID: `poweredthingies`
> 前置条件: 无
> 导入: `import mods.poweredthingies.Tweaker;`

## API 列表

### Tweaker（入口类）

> `import mods.poweredthingies.Tweaker;`

Tweaker 是获取各机器 Tweaker 实例的入口类。由于 Kotlin 基类在 CraftTweaker 中导入的问题，需要通过此类获取各机器的 Tweaker。

#### 获取机器 Tweaker 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.compoundTweaker()` | CompoundMaker | 获取化合物制造机 Tweaker |
| `.fluidCompoundTweaker()` | FluidCompoundProducer | 获取流体化合物生产机 Tweaker |
| `.fluidBurnerFuelTweaker()` | FluidBurnerFuel | 获取流体燃烧器燃料 Tweaker |
| `.fluidBurnerCoolantTweaker()` | FluidBurnerCoolant | 获取流体燃烧器冷却剂 Tweaker |
| `.itemCompoundProducerTweaker()` | ItemCompoundProducer | 获取物品化合物生产机 Tweaker |
| `.incineratorTweaker()` | Incinerator | 获取焚化炉 Tweaker |
| `.itemLiquefierTweaker()` | ItemLiquefier | 获取物品液化器 Tweaker |
| `.poweredKilnTweaker()` | PoweredKiln | 获取电力窑 Tweaker |
| `.powderMakerTweaker()` | PowderMaker | 获取粉末制造机 Tweaker |

### 通用方法（所有机器 Tweaker 共享）

所有机器 Tweaker 都支持以下方法：

| 方法 | 返回 | 说明 |
|------|------|------|
| `.clear()` | void | 清除该机器的全部配方 |
| `.logKeys()` | void | 将该机器的所有配方键输出到 CT 日志 |
| `.removeRecipe(String key)` | void | 根据键移除配方（使用 `logKeys()` 查看有效键） |

### CompoundMaker（化合物制造机）

> `import mods.poweredthingies.Tweaker.compoundTweaker as ct;`

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, ILiquidStack? left, IItemStack[]? top, ILiquidStack? right, IItemStack[]? bottom)` | void | 添加化合物制造配方，四个方向可为 null |

```zenscript
var ct = Tweaker.compoundTweaker();
ct.addRecipe(<minecraft:obsidian>, <liquid:lava> * 250, [<minecraft:cobblestone>, <minecraft:cobblestone>], null, [<minecraft:cobblestone>, <minecraft:cobblestone>]);
```

### FluidCompoundProducer（流体化合物生产机）

> `import mods.poweredthingies.Tweaker.fluidCompoundTweaker as fct;`

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, ILiquidStack inputA, ILiquidStack inputB)` | void | 添加流体化合物配方 |

```zenscript
var fct = Tweaker.fluidCompoundTweaker();
fct.addRecipe(<liquid:tf-sewage> * 150, <liquid:water> * 300, <liquid:lava> * 100);
```

### FluidBurnerFuel（流体燃烧器 - 燃料）

> `import mods.poweredthingies.Tweaker.fluidBurnerFuelTweaker as fuel;`

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(ILiquidStack fluid, int ticks)` | void | 添加燃料，ticks 为该燃料燃烧的 tick 数 |

```zenscript
var fuel = Tweaker.fluidBurnerFuelTweaker();
fuel.addFuel(<liquid:tf-sewage> * 50, 100);
```

### FluidBurnerCoolant（流体燃烧器 - 冷却剂）

> `import mods.poweredthingies.Tweaker.fluidBurnerCoolantTweaker as coolant;`

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addCoolant(ILiquidStack fluid, float timeMultiplier)` | void | 添加冷却剂，timeMultiplier 为燃料燃烧时间的倍率 |

```zenscript
var coolant = Tweaker.fluidBurnerCoolantTweaker();
coolant.addCoolant(<liquid:tf-sewage> * 50, 1.1);
```

### ItemCompoundProducer（物品化合物生产机）

> `import mods.poweredthingies.Tweaker.itemCompoundProducerTweaker as icp;`

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack inputStack, ILiquidStack inputFluid, IItemStack result)` | void | 添加物品化合物配方 |

```zenscript
var icp = Tweaker.itemCompoundProducerTweaker();
icp.addRecipe(<minecraft:cobblestone>, <liquid:water> * 125, <minecraft:mossy_cobblestone>);
```

### Incinerator（焚化炉）

> `import mods.poweredthingies.Tweaker.incineratorTweaker as it;`

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack input, long power, WeightedItemStack[] outputs)` | void | 添加焚化配方，power 为总能量产出（RF/T/FE），outputs 为加权物品数组（使用 `%` 设置权重） |

```zenscript
var it = Tweaker.incineratorTweaker();
it.addRecipe(<minecraft:bucket>, 3600, [<minecraft:iron_ingot> % 15]);
```

### ItemLiquefier（物品液化器）

> `import mods.poweredthingies.Tweaker.itemLiquefierTweaker as ilt;`

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack input, ILiquidStack output)` | void | 添加物品液化配方 |

```zenscript
var ilt = Tweaker.itemLiquefierTweaker();
ilt.addRecipe(<minecraft:bucket>, <liquid:lava> * 125);
```

### PoweredKiln（电力窑）

> `import mods.poweredthingies.Tweaker.poweredKilnTweaker as pkt;`

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack input, IItemStack output)` | void | 添加电力窑配方 |

```zenscript
var pkt = Tweaker.poweredKilnTweaker();
pkt.addRecipe(<minecraft:bucket>, <minecraft:iron_ingot>);
```

### PowderMaker（粉末制造机）

> `import mods.poweredthingies.Tweaker.powderMakerTweaker as pmt;`

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack input, WeightedItemStack[] outputs)` | void | 添加粉末制造配方，outputs 为加权物品数组（使用 `%` 设置权重） |

```zenscript
var pmt = Tweaker.powderMakerTweaker();
pmt.addRecipe(<minecraft:bucket>, [<minecraft:iron_ingot> % 100, <minecraft:iron_ingot> % 12, <minecraft:iron_ingot> % 12]);
```