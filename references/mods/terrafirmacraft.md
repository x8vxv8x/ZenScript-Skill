# TerraFirmaCraft CraftTweaker API 参考

> Mod ID: `terrafirmacraft`
> 前置条件: 无
> 导入: `import mods.terrafirmacraft.<ClassName>;`

## API 列表

### Alloy (合金)

> `import mods.terrafirmacraft.Alloy;`
> `import mods.terrafirmacraft.AlloyRecipeBuilder;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addAlloy(String metal)` | AlloyRecipeBuilder | 添加合金配方，返回配方构建器 |
| `.removeAlloy(String metal)` | void | 移除指定金属的合金配方 |

#### AlloyRecipeBuilder 构建器方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addMetal(String input, double min, double max)` | AlloyRecipeBuilder | 添加金属成分，min/max 为最小/最大比例 |
| `.build()` | void | 构建合金配方 |

### Anvil (铁砧)

> `import mods.terrafirmacraft.Anvil;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String registryName, IIngredient input, IItemStack output, int minTier, String skillType, String... forgeRules)` | void | 添加铁砧配方。`minTier`：0=石、1=铜、2=青铜、3=锻铁、4=钢、5=黑钢、6=红/蓝钢。`skillType`：`general`/`tools`/`weapons`/`armor`/`null`。`forgeRules`：类型_顺序，类型可选 `HIT`/`DRAW`/`PUNCH`/`BEND`/`UPSET`/`SHRINK`，顺序可选 `ANY`/`NOT_LAST`/`LAST`/`SECOND_LAST`/`THIRD_LAST`（如 `HIT_ANY`），配方需 1-3 条规则 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeRecipe(String registryName)` | void | 移除指定注册名的配方 |

### Barrel (木桶)

> `import mods.terrafirmacraft.Barrel;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String registryName, @Optional IIngredient itemInput, ILiquidStack fluidInput, @Optional IItemStack itemOutput, @Optional ILiquidStack fluidOutput, int hours)` | void | 添加木桶配方，hours 为处理时间（小时） |
| `.removeRecipe(@Optional IItemStack outputItem, @Optional ILiquidStack outputLiquid)` | void | 移除指定输出的配方 |
| `.removeRecipe(String registryName)` | void | 移除指定注册名的配方 |

### Chisel (凿子)

> `import mods.terrafirmacraft.Chisel;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String registryName, IItemStack input, IItemStack output)` | void | 添加凿子配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeRecipe(String registryName)` | void | 移除指定注册名的配方 |

### Heating (加热)

> `import mods.terrafirmacraft.Heating;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String registryName, IItemStack input, IItemStack output, float transformTemp, float maxTemp)` | void | 添加加热配方，transformTemp 为完全转化温度，maxTemp 为销毁温度 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeRecipe(String registryName)` | void | 移除指定注册名的配方 |

### ItemRegistry (物品注册)

> `import mods.terrafirmacraft.ItemRegistry;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerItemSize(IIngredient input, String size, String weight)` | void | 注册物品尺寸和重量。size 可选：`TINY`、`VERY_SMALL`、`SMALL`、`NORMAL`、`LARGE`、`VERY_LARGE`、`HUGE`。weight 可选：`VERY_LIGHT`、`LIGHT`、`MEDIUM`、`HEAVY`、`VERY_HEAVY` |
| `.registerItemHeat(IIngredient input, float heatCapacity, float meltTemp, bool forgeable)` | void | 注册物品热量属性，heatCapacity 为热容，meltTemp 为熔化温度，forgeable 为是否可锻造 |
| `.registerItemMetal(IIngredient input, String metal, int units, bool canMelt)` | void | 注册物品为金属物品，metal 为金属类型，units 为单位，canMelt 为是否可熔炼 |
| `.registerFood(IIngredient input, int hunger, float water, float saturation, float decay, float grain, float veg, float fruit, float meat, float dairy)` | void | 注册食物属性 |
| `.registerArmor(IIngredient input, float crushingModifier, float piercingModifier, float slashingModifier)` | void | 注册护甲属性 |
| `.registerFuel(IItemStack itemStack, int burnTicks, float temperature, bool forgeFuel, bool bloomeryFuel)` | void | 注册燃料属性 |

### ClayKnapping, FireClayKnapping, LeatherKnapping (捏制)

> `import mods.terrafirmacraft.ClayKnapping;`
> `import mods.terrafirmacraft.FireClayKnapping;`
> `import mods.terrafirmacraft.leatherKnapping;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String registryName, IItemStack output, String... pattern)` | void | 添加捏制配方，pattern 为图案 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeRecipe(String registryName)` | void | 移除指定注册名的配方 |

### StoneKnapping (石头捏制)

> `import mods.terrafirmacraft.StoneKnapping;`

石头捏制支持按岩石类型指定不同输出。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String registryName, IItemStack[] output, String[] rocks, String... pattern)` | void | 添加石头捏制配方。`output` 为输出数组（对应每种岩石类型），`rocks` 为岩石类型数组（如 `["shale", "claystone", "rocksalt", "limestone"]` 或 `["all"]`），`pattern` 为图案 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeRecipe(String registryName)` | void | 移除指定注册名的配方 |

### Loom (织布机)

> `import mods.terrafirmacraft.Loom;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String registryName, IIngredient input, IItemStack output, int steps, String loomTexture)` | void | 添加织布机配方，steps 为步骤数，loomTexture 为纹理路径 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeRecipe(String registryName)` | void | 移除指定注册名的配方 |

### Quern (磨石座)

> `import mods.terrafirmacraft.Quern;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String registryName, IIngredient input, IItemStack output)` | void | 添加配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeRecipe(String registryName)` | void | 移除指定注册名的配方 |

### Welding (焊接)

> `import mods.terrafirmacraft.Welding;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String registryName, IIngredient input1, IIngredient input2, IItemStack output, int minTier)` | void | 添加焊接配方，minTier 为最低等级。输入必须是可锻造的（通过 ItemRegistry 注册），且不可堆叠 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeRecipe(String registryName)` | void | 移除指定注册名的配方 |

---

## 参考数据

### 加热温度等级

| 等级 | 起始温度 | 结束温度 |
|------|---------|---------|
| Warming (微温) | 1 | 80 |
| Hot (热) | 80 | 210 |
| Very Hot (极热) | 210 | 480 |
| Faint Red (暗红) | 480 | 580 |
| Dark Red (深红) | 580 | 730 |
| Bright Red (亮红) | 730 | 930 |
| Orange (橙) | 930 | 1100 |
| Yellow (黄) | 1100 | 1300 |
| Yellow White (黄白) | 1300 | 1400 |
| White (白) | 1400 | 1500 |
| Brilliant White (亮白) | 1500 | - |

### 金属类型常量

`registerItemMetal` 的 `metal` 参数可选值：

`BISMUTH`、`BISMUTH_BRONZE`、`BLACK_BRONZE`、`BRASS`、`BRONZE`、`COPPER`、`GOLD`、`LEAD`、`NICKEL`、`ROSE_GOLD`、`SILVER`、`TIN`、`ZINC`、`STERLING_SILVER`、`WROUGHT_IRON`、`PIG_IRON`、`STEEL`、`PLATINUM`、`BLACK_STEEL`、`BLUE_STEEL`、`RED_STEEL`、`WEAK_STEEL`、`WEAK_BLUE_STEEL`、`WEAK_RED_STEEL`、`HIGH_CARBON_STEEL`、`HIGH_CARBON_BLUE_STEEL`、`HIGH_CARBON_RED_STEEL`、`HIGH_CARBON_BLACK_STEEL`、`UNKNOWN`
