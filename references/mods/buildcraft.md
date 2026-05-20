# BuildCraft CraftTweaker API 参考

> Mod ID: `buildcraft`
> 前置条件: BuildCraft Compat Module
> 导入: `import mods.buildcraft.*;`

BuildCraft 是一个工业模组。

---

## API 列表

### AssemblyTable（装配台）

> `import mods.buildcraft.AssemblyTable;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(recipeName as string, output as IItemStack, power as int, inputs as IIngredient[])` | void | 添加装配台配方 |
| `.removeByName(name as string)` | void | 按名称移除配方 |

**参数说明**:
- `recipeName`: 配方名称（必须唯一）
- `output`: 输出物品
- `power`: 总能量消耗（MJ）
- `inputs`: 输入材料数组

#### 现有配方名称

**芯片组**:
- `buildcraftsilicon:redstone_chipset`
- `buildcraftsilicon:iron_chipset`
- `buildcraftsilicon:gold_chipset`
- `buildcraftsilicon:quartz_chipset`
- `buildcraftsilicon:diamond_chipset`

**插件**:
- `buildcraftsilicon:plug_pulsar`
- `buildcraftsilicon:light-sensor`
- `buildcrafttransport:facaderecipes`

**透镜**:
- `buildcraftsilicon:lens-regular`
- `buildcraftsilicon:lens-filter`
- `buildcraftsilicon:lens-regular-<color>`
- `buildcraftsilicon:lens-filter-<color>`

**电线**:
- `buildcrafttransport:wire-<color>`

**门**:
- `buildcraftsilicon:gate-<operation>-<material>-no_modifier`
- `buildcraftsilicon:gate-modifier-<operation>-<material>-<modifier>`

颜色参数: `white`, `orange`, `magenta`, `lightblue`, `yellow`, `lime`, `pink`, `gray`, `silver`, `cyan`, `purple`, `blue`, `brown`, `green`, `red`, `black`

操作参数: `and`, `or`

材料参数: `iron`, `nether_brick`, `gold`

修饰符参数: `lapis`, `quartz`, `diamond`

### CombustionEngine（燃油引擎）

> `import mods.buildcraft.CombustionEngine;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addCleanFuel(liquid as ILiquidStack, powerPerTick as double, timePerBucket as int)` | void | 添加清洁燃料 |
| `.addDirtyFuel(lFuel as ILiquidStack, powerPerTick as double, timePerBucket as int, lResidue as ILiquidStack)` | void | 添加脏燃料 |

**参数说明**:
- `liquid`: 燃料流体
- `powerPerTick`: 每tick能量输出（MJ）
- `timePerBucket`: 每桶燃料运行时间（tick）
- `lResidue`: 残留流体

---

## 注意事项

- 组装台需要 BuildCraft Silicon 模块
- 内燃机需要 BuildCraft Energy 模块
- 配方名称必须唯一，否则会覆盖现有配方
- 能量单位为 MJ（Minecraft Joules）

---

## MoreTweaker 扩展（需安装 MoreTweaker）

> `import moretweaker.buildcraft.AssemblyTable;`
> `import moretweaker.buildcraft.IntegrationTable;`
> `import moretweaker.buildcraft.Refinery;`

### AssemblyTable（装配台）

> `import moretweaker.buildcraft.AssemblyTable;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, long energyCost, IIngredient[] inputs)` | void | 添加装配台配方。`energyCost` 为能量消耗（MJ） |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### IntegrationTable（集成台）

> `import moretweaker.buildcraft.IntegrationTable;`

催化剂（catalyst）为中间的物品。配方按催化剂移除，**不是**按输出。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, long energyCost, IIngredient catalyst, IIngredient[] inputs)` | void | 添加集成配方。`energyCost` 为能量消耗（MJ），`catalyst` 为催化剂 |
| `.remove(IIngredient catalyst)` | void | 按催化剂移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### Refinery（精炼厂）

> `import moretweaker.buildcraft.Refinery;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addDistilling(ILiquidStack input, ILiquidStack output, ILiquidStack gasOutput, int energy)` | void | 添加蒸馏配方。`output` 为液体输出，`gasOutput` 为气体输出，`energy` 为能量消耗 |
| `.removeDistilling(ILiquidStack input)` | void | 按输入移除蒸馏配方 |
| `.removeAll()` | void | 移除所有配方 |
