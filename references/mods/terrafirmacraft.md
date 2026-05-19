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
| `.addRecipe(String registryName, IIngredient input, IItemStack output, int minTier, String skillType, String... forgeRules)` | void | 添加铁砧配方，minTier 为最低等级，skillType 为技能类型，forgeRules 为锻造规则 |
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
| `.registerItemSize(IIngredient input, String size, String weight)` | void | 注册物品尺寸和重量，size 为尺寸，weight 为重量 |
| `.registerItemHeat(IIngredient input, float heatCapacity, float meltTemp, bool forgeable)` | void | 注册物品热量属性，heatCapacity 为热容，meltTemp 为熔化温度，forgeable 为是否可锻造 |
| `.registerItemMetal(IIngredient input, String metal, int units, bool canMelt)` | void | 注册物品为金属物品，metal 为金属类型，units 为单位，canMelt 为是否可熔炼 |
| `.registerFood(IIngredient input, int hunger, float water, float saturation, float decay, float grain, float veg, float fruit, float meat, float dairy)` | void | 注册食物属性 |
| `.registerArmor(IIngredient input, float crushingModifier, float piercingModifier, float slashingModifier)` | void | 注册护甲属性 |
| `.registerFuel(IItemStack itemStack, int burnTicks, float temperature, bool forgeFuel, bool bloomeryFuel)` | void | 注册燃料属性 |

### ClayKnapping, FireClayKnapping, LeatherKnapping, StoneKnapping (捏制)

> `import mods.terrafirmacraft.ClayKnapping;`
> `import mods.terrafirmacraft.FireClayKnapping;`
> `import mods.terrafirmacraft.leatherKnapping;`
> `import mods.terrafirmacraft.StoneKnapping;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String registryName, IItemStack output, String... pattern)` | void | 添加捏制配方，pattern 为图案 |
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
| `.addRecipe(String registryName, IIngredient input1, IIngredient input2, IItemStack output, int minTier)` | void | 添加焊接配方，minTier 为最低等级 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeRecipe(String registryName)` | void | 移除指定注册名的配方 |
