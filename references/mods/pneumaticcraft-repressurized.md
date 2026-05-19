# PneumaticCraft: Repressurized CraftTweaker API 参考

> Mod ID: `pneumaticcraft`
> 前置条件: 无（模组自带 CraftTweaker 支持）
> 导入: `import mods.pneumaticcraft.<ClassName>;`

## API 列表

### assembly（装配台）

> `import mods.pneumaticcraft.assembly;`

#### 移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeLaserRecipe(IItemStack output)` | void | 移除第一个匹配输出的激光配方 |
| `.removeDrillRecipe(IItemStack output)` | void | 移除第一个匹配输出的钻头配方 |
| `.removeDrillLaserRecipe(IItemStack output)` | void | 移除第一个匹配输出的钻头+激光配方 |
| `.removeAllLaserRecipes()` | void | 移除所有激光配方 |
| `.removeAllDrillRecipes()` | void | 移除所有钻头配方 |
| `.removeAllDrillLaserRecipes()` | void | 移除所有钻头+激光配方 |

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addLaserRecipe(IItemStack input, IItemStack output)` | void | 添加激光配方 |
| `.addDrillRecipe(IItemStack input, IItemStack output)` | void | 添加钻头配方 |

- 钻头+激光组合配方会在钻头配方 A→B 和激光配方 B→C 同时存在时自动生成

### explosioncrafting（爆炸合成）

> `import mods.pneumaticcraft.explosioncrafting;`

#### 移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IIngredient output)` | void | 移除第一个匹配输出的配方 |
| `.removeAllRecipes()` | void | 移除所有爆炸合成配方 |

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack input, IItemStack output, int loss_rate)` | void | 添加爆炸合成配方，loss_rate 为损失率（百分比） |
| `.addRecipe(IOreDictEntry input, IItemStack output, int loss_rate)` | void | 添加爆炸合成配方（矿辞输入） |

### heatframecooling（热量框架）

> `import mods.pneumaticcraft.heatframecooling;`

#### 移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IIngredient output)` | void | 移除第一个匹配输出的配方 |
| `.removeAllRecipes()` | void | 移除所有配方 |

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack input, IItemStack output)` | void | 添加冷却配方 |
| `.addRecipe(IOreDictEntry input, IItemStack output)` | void | 添加冷却配方（矿辞输入） |

### liquidfuel（液体燃料）

> `import mods.pneumaticcraft.liquidfuel;`

#### 移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeFuel(ILiquidStack fluid)` | void | 移除指定流体的燃料注册 |
| `.removeAllFuels()` | void | 移除所有已注册的燃料 |

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(ILiquidStack fluid, double mlPerBucket)` | void | 注册流体为燃料，mlPerBucket 为每桶燃料产生的压缩空气毫升数（参考：煤炭在空气压缩机中产生 16000mL） |

### plasticmixer（塑料混合机）

> `import mods.pneumaticcraft.plasticmixer;`

#### 移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(ILiquidStack fluid)` | void | 移除第一个匹配输入流体的配方 |
| `.removeAllRecipes()` | void | 移除所有塑料混合机配方 |

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack liquid, IItemStack stack, int temperature)` | void | 添加双向配方（温度单位为开尔文） |
| `.addSolidifyOnlyRecipe(ILiquidStack liquidInput, IItemStack itemOutput)` | void | 添加仅固化配方 |
| `.addMeltOnlyRecipe(IItemStack itemInput, ILiquidStack fluidOutput, int temperature)` | void | 添加仅熔化配方（温度单位为开尔文） |

- 温度说明：273K = 0°C，373K = 100°C

### pressurechamber（压力室）

> `import mods.pneumaticcraft.pressurechamber;`

#### 移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack[] outputs)` | void | 移除第一个匹配输出数组的配方 |
| `.removeAllRecipes()` | void | 移除所有压力室配方 |

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient[] inputs, double pressure, IItemStack[] outputs)` | void | 添加压力室配方，pressure 为所需压力（bar） |

### refinery（精炼厂）

> `import mods.pneumaticcraft.refinery;`

#### 移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IIngredient[] outputs)` | void | 移除第一个匹配输出数组的配方 |
| `.removeRecipes(IIngredient input)` | void | 移除第一个匹配输入的配方 |
| `.removeAllRecipes()` | void | 移除所有精炼厂配方 |

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack input, ILiquidStack[] outputs)` | void | 添加精炼配方（默认最低温度 373K） |
| `.addRecipe(int minimumTemperature, ILiquidStack input, ILiquidStack[] outputs)` | void | 添加精炼配方（指定最低温度，v0.9.0+） |

- 精炼厂数量为 2-4 个方块，输出流体数量受方块数限制
- 温度越高处理速度越快

### thermopneumaticprocessingplant（热气动加工机）

> `import mods.pneumaticcraft.thermopneumaticprocessingplant;`

#### 移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IIngredient output)` | void | 移除第一个匹配输出的配方 |
| `.removeAllRecipes()` | void | 移除所有热气动加工机配方 |

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack itemInput, double pressure, double temperature, ILiquidStack output)` | void | 添加配方（物品输入→流体输出） |
| `.addRecipe(ILiquidStack liquidInput, IItemStack itemInput, double pressure, double temperature, ILiquidStack output)` | void | 添加配方（流体+物品输入→流体输出，item 可为 null） |

- 温度单位为开尔文：273K = 0°C，373K = 100°C
- 压力单位为 bar

### xpfluid（经验流体）

> `import mods.pneumaticcraft.xpfluid;`

#### 移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeXPFluid(ILiquidStack fluid)` | void | 移除指定流体的经验注册 |
| `.removeAllXPFluids()` | void | 移除所有已注册的经验流体 |

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addXPFluid(ILiquidStack fluid, double ratio)` | void | 注册流体为经验流体，ratio 为每毫桶流体对应的经验值 |

## 使用示例

### 爆炸合成

```zenscript
import mods.pneumaticcraft.explosioncrafting;

// 移除默认的铁锭→压缩铁锭配方
explosioncrafting.removeRecipe(<pneumaticcraft:ingot_iron_compressed>);

// 添加新配方：铁锭损失率 95%，钢锭损失率 10%
explosioncrafting.addRecipe(<ore:ingotIron>, <pneumaticcraft:ingot_iron_compressed>, 95);
explosioncrafting.addRecipe(<ore:ingotSteel>, <pneumaticcraft:ingot_iron_compressed>, 10);
```
---
## 注意事项

- PneumaticCraft: Repressurized 的 CraftTweaker 问题请提交到其 [GitHub Issue Tracker](https://github.com/TeamPneumatic/pnc-repressurized/issues)
- 此参考仅适用于 PneumaticCraft: Repressurized（1.12.2），不适用于原版 PneumaticCraft
- 温度单位统一使用开尔文（K），273K = 0°C
