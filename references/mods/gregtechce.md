# GregTech Community Edition CraftTweaker API 参考

> Mod ID: `gregtech`
> 前置条件: 无
> 导入: `import mods.gregtech.recipe.RecipeMap;`
> 加载器: 需要使用 `#loader gregtech`

GregTech CE 是 GregTech 的完全重写版本，注重性能和平衡。

---

## API 列表

### RecipeMap（配方映射）

> `import mods.gregtech.recipe.RecipeMap;`

GTCE 将所有配方存储在 RecipeMap 中。使用 `RecipeMap.getByName(machineName)` 获取特定机器的配方构建器。

#### 可用机器列表

| 机器名称 | 内部名 |
|---------|--------|
| 压缩机 | `compressor` |
| 提取机 | `extractor` |
| 粉碎机 | `macerator` |
| 洗矿厂 | `orewasher` |
| 热力离心机 | `thermal_centrifuge` |
| 熔炉 | `furnace` |
| 微波炉 | `microwave` |
| 组装机 | `assembler` |
| 冲压机 | `forming_press` |
| 流体装罐机 | `fluid_canner` |
| 等离子弧光炉 | `plasma_arc_furnace` |
| 弧光炉 | `arc_furnace` |
| 筛分机 | `sifter` |
| 精密激光雕刻机 | `laser_engraver` |
| 混合机 | `mixer` |
| 高压釜 | `autoclave` |
| 电磁分选机 | `electromagnetic_separator` |
| 极化器 | `polarizer` |
| 化学浸洗机 | `chemical_bath` |
| 酿造机 | `brewer` |
| 流体加热器 | `fluid_heater` |
| 蒸馏器 | `distillery` |
| 发酵机 | `fermenter` |
| 流体固化机 | `fluid_solidifier` |
| 流体提取机 | `fluid_extractor` |
| 离心机 | `centrifuge` |
| 电解机 | `electrolyzer` |
| 高炉 | `blast_furnace` |
| 爆破压缩机 | `implosion_compressor` |
| 真空冷冻机 | `vacuum_freezer` |
| 化学反应器 | `chemical_reactor` |
| 蒸馏塔 | `distillation_tower` |
| 裂解机 | `cracker` |
| 焦炉 | `pyro` |
| 拉丝机 | `wiremill` |
| 金属弯曲机 | `metal_bender` |
| 合金治炼炉 | `alloy_smelter` |
| 装罐机 | `canner` |
| 车床 | `lathe` |
| 切割锯 | `cutting_saw` |
| 挤出机 | `extruder` |
| 锻造锤 | `forge_hammer` |
| 打包机 | `packer` |
| 拆包机 | `unpacker` |
| 柴油发电机 | `diesel_generator` |
| 燃气轮机 | `gas_turbine` |
| 蒸汽轮机 | `steam_turbine` |
| 等离子发电机 | `plasma_generator` |

#### 构建器方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.recipeBuilder()` | RecipeBuilder | 创建配方构建器 |
| `.findRecipe(long voltage, IItemHandlerModifiable inputs, IMultipleTankHandler fluidInputs)` | Recipe | 查找配方 |

### RecipeBuilder（配方构建器）

配方构建器使用链式调用，类似 Java Stream。

#### 输入方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.inputs(IIngredient... inputs)` | RecipeBuilder | 添加物品输入 |
| `.fluidInputs(ILiquidStack... fluids)` | RecipeBuilder | 添加流体输入 |
| `.notConsumable(IIngredient input)` | RecipeBuilder | 添加不消耗的物品输入 |

#### 输出方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.outputs(IItemStack... outputs)` | RecipeBuilder | 添加物品输出 |
| `.fluidOutputs(ILiquidStack... fluids)` | RecipeBuilder | 添加流体输出 |
| `.chancedOutput(IItemStack stack, int chance, int tierChanceBoost)` | RecipeBuilder | 添加概率输出（10000 = 100%） |

#### 配置方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.duration(int duration)` | RecipeBuilder | 设置配方时间（tick） |
| `.EUt(int eu)` | RecipeBuilder | 设置每 tick EU 消耗 |
| `.property(String name, Object value)` | RecipeBuilder | 设置配方属性 |
| `.hidden()` | RecipeBuilder | 隐藏配方（不在 JEI 显示） |

#### 可用属性

| 属性名 | 说明 |
|--------|------|
| `temperature` | 高炉最低温度要求 |
| `circuit` | 集成电路配置 |
| `explosives` | 爆破压缩机所需炸药数量 |

#### 注册方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.buildAndRegister()` | void | 构建并注册配方 |

### Recipe（配方实例）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove()` | void | 移除配方 |

---

### PBFRecipeBuilder（原始高炉配方构建器）

> `import mods.gregtech.recipe.PBFRecipeBuilder;`

原始高炉使用不同于普通配方的语法。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.start()` | PBFRecipeBuilder | 开始创建配方 |
| `.input(IIngredient input)` | PBFRecipeBuilder | 添加输入 |
| `.output(IItemStack output)` | PBFRecipeBuilder | 添加输出 |
| `.duration(int duration)` | PBFRecipeBuilder | 设置时间 |
| `.fuelAmount(int amount)` | PBFRecipeBuilder | 设置燃料数量 |
| `.buildAndRegister()` | void | 构建并注册配方 |

---

### MaterialRegistry（材料注册表）

> `import mods.gregtech.material.MaterialRegistry;`

材料注册表用于获取、列出和创建统一系统中的材料。

#### 获取方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.get(String materialName)` | Material | 获取材料（可能返回 null） |
| `.getAllMaterials()` | List<Material> | 列出所有已注册材料 |

#### 创建方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createFluidMaterial(int metaItemSubId, String name, int color, String iconSet, @Optional MaterialStack[] components)` | FluidMaterial | 创建流体材料 |
| `.createDustMaterial(int metaItemSubId, String name, int color, String iconSet, int harvestLevel, @Optional MaterialStack[] components)` | DustMaterial | 创建粉末材料 |
| `.createGemMaterial(int metaItemSubId, String name, int color, String iconSet, int harvestLevel, @Optional MaterialStack[] components, @Optional float toolSpeed, @Optional int toolDurability)` | GemMaterial | 创建宝石材料 |
| `.createIngotMaterial(int metaItemSubId, String name, int color, String iconSet, int harvestLevel, @Optional MaterialStack[] components, @Optional float toolSpeed, @Optional int toolDurability, @Optional int blastFurnaceTemperature)` | IngotMaterial | 创建锭材料 |

---

### Material（材料对象）

#### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `color` | int | RGB 颜色格式 |
| `chemicalFormula` | string | 化学式 |
| `iconSet` | MaterialIconSet | 材料图标集 |
| `components` | ImmutableList<MaterialStack> | 材料组件列表 |
| `generationFlagsRaw` | long | 生成标志（见 MatFlags） |
| `element` | Element | 材料元素 |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `radioactive` | bool | 是否放射性 |
| `protons` | long | 质子数 |
| `neutrons` | long | 中子数 |
| `mass` | long | 质量 |
| `density` | long | 密度 |
| `camelCaseString` | string | 驼峰命名 |
| `unlocalizedName` | string | 未本地化名称 |
| `localizedName` | string | 本地化名称（仅客户端） |
| `name` | string | 材料注册表中的名称 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFlags(String... flagNames)` | void | 添加生成标志 |
| `.hasFlag(String flagName)` | bool | 检查是否有生成标志 |

---

### FluidMaterial（流体材料）

继承 Material 的所有成员。

#### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `fluidTemperature` | int | 流体温度 |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `hasFluid` | bool | 是否有流体 |
| `hasPlasma` | bool | 是否有等离子体 |
| `isGaseous` | bool | 是否为气体 |
| `fluid` | ILiquidDefinition | 材料流体 |
| `plasma` | ILiquidDefinition | 材料等离子流体 |

---

### DustMaterial（粉末材料）

继承 FluidMaterial 的所有成员。

#### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `oreMultiplier` | int | 粉碎时矿石输出倍率 |
| `byProductMultiplier` | int | 研磨时副产品输出倍率 |
| `smeltingMultiplier` | int | 原版熔炼物品数量倍率 |
| `directSmelting` | SolidMaterial | 矿石直接熔炼结果材料 |
| `washedIn` | FluidMaterial | 矿石清洗材料 |
| `separatedInto` | DustMaterial | 电磁分选结果材料 |
| `burnTime` | int | 燃料燃烧时间（0 或负值表示不可用作燃料） |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `oreByProducts` | List<FluidMaterial> | 矿石副产品列表 |
| `harvestLevel` | int | 开采等级 |

---

### SolidMaterial（固体材料）

继承 DustMaterial 的所有成员。

#### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `handleMaterial` | SolidMaterial | 工具手柄材料 |
| `macerateInto` | DustMaterial | 粉碎结果材料（默认自身） |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `toolSpeed` | float | 工具速度（默认 1.0） |
| `toolDurability` | int | 工具耐久（0 表示不可用于工具） |
| `toolEnchantments` | List<EnchantmentData> | 工具附魔列表 |

---

### IngotMaterial（锭材料）

继承 SolidMaterial 的所有成员。可用于线缆、电缆和流体管道。

#### 设置方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setCableProperties(long voltage, int baseAmperage, int lossPerBlock)` | void | 设置电缆属性 |
| `.setFluidPipeProperties(int throughput, int maxTemperature, boolean gasProof)` | void | 设置流体管道属性 |
| `.addToolEnchantment(IEnchantment enchantment)` | void | 添加工具附魔 |

---

### MaterialIconSet（材料图标集）

可用值：NONE、METALLIC、DULL、MAGNETIC、QUARTZ、DIAMOND、EMERALD、SHINY、SHARDS、ROUGH、FINE、SAND、FLINT、RUBY、LAPIS、POWDER、FLUID、GAS、LIGNITE、OPAL、GLASS、WOOD、LEAF、GEM_HORIZONTAL、GEM_VERTICAL、PAPER、NETHERSTAR

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 名称 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.toString()` | string | 转为字符串 |
| `MaterialIconSet.getByName(String name)` | MaterialIconSet | 静态方法，按名称获取 |

---

### 材料生成标志

| 标志名（不区分大小写） | 说明 |
|----------------------|------|
| `DECOMPOSITION_BY_ELECTROLYZING` | 启用电解分解配方生成 |
| `DECOMPOSITION_BY_CENTRIFUGING` | 启用离心分解配方生成 |
| `BURNING` | 持续燃烧光环 |
| `FLAMMABLE` | 可燃 |
| `EXPLOSIVE` | 爆炸性 |
| `NO_UNIFICATION` | 完全禁用统一 |
| `NO_RECYCLING` | 物品不可回收 |
| `DISABLE_DECOMPOSITION` | 禁用分解配方生成 |
| `DECOMPOSITION_REQUIRES_HYDROGEN` | 分解需要氢气输入 |
| `GENERATE_PLATE` | 生成板材 |
| `GENERATE_DENSE` | 生成致密板 |
| `NO_WORKING` | 不可加工（用于涂层材料） |
| `NO_SMASHING` | 不可锻造 |
| `NO_SMELTING` | 不可熔炼 |
| `INDUCTION_SMELTING_LOW_OUTPUT` | 感应炉输出减少 |
| `SMELT_INTO_FLUID` | 熔炼成流体 |
| `EXCLUDE_BLOCK_CRAFTING_RECIPES` | 排除方块合成配方 |
| `EXCLUDE_PLATE_COMPRESSOR_RECIPE` | 排除板材压缩配方 |
| `CRYSTALLISABLE` | 可结晶 |
| `GENERATE_LENSE` | 生成透镜 |
| `HIGH_SIFTER_OUTPUT` | 高筛分输出 |
| `GENERATE_FLUID_BLOCK` | 生成流体方块 |
| `GENERATE_PLASMA` | 生成等离子体 |
| `STATE_GAS` | 标记为气体状态 |
| `GENERATE_ROD` | 生成棒材 |
| `GENERATE_GEAR` | 生成齿轮 |
| `GENERATE_LONG_ROD` | 生成长棒材 |
| `MORTAR_GRINDABLE` | 可用研钵研磨 |

---

## 使用示例

### 示例一：添加高炉配方

```zenscript
#loader gregtech
import mods.gregtech.recipe.RecipeMap;

// 电弧高炉
val blast_furnace = RecipeMap.getByName("blast_furnace");
blast_furnace.recipeBuilder()
    .inputs(<ore:ingotCompressedWroughtIron> * 1)
    .fluidInputs([<liquid:oxygen> * 500])
    .outputs(<ore:ingotSteel>.firstItem * 1)
    .property("temperature", 1000)
    .duration(40)
    .EUt(120)
    .buildAndRegister();
```

### 示例二：添加原始高炉配方

```zenscript
import mods.gregtech.recipe.PBFRecipeBuilder;

PBFRecipeBuilder.start()
    .input(<ore:ingotCompressedWroughtIron> * 1)
    .output(<ore:ingotSteel>.firstItem * 1)
    .duration(250)
    .fuelAmount(2)
    .buildAndRegister();
```

### 示例三：移除配方

```zenscript
import mods.gregtech.recipe.RecipeMap;

val compressor = RecipeMap.getByName("compressor");
compressor.findRecipe(2, [<minecraft:redstone>], null).remove();
```

### 示例四：创建自定义材料

```zenscript
#loader gregtech
import mods.gregtech.material.MaterialRegistry;

// 创建粉末材料
val dustMaterial = MaterialRegistry.createDustMaterial(700, "test", 0xFFAA33, "dull", 2);
dustMaterial.addFlags(["GENERATE_ORE", "GENERATE_PLATE"]);

// 创建宝石材料（自动创建电解配方）
val gemFancy = MaterialRegistry.createGemMaterial(701, "some_fancy_gemstone", 0x0F3E4E2, "gem_horizontal", 1, 
    [<material:beryllium>*4, <material:silicon>*2, <material:oxygen>*9, <material:hydrogen>*2], 1.0, 0);

// 创建锭材料（使用自定义材料作为组件）
val ingotComplex = MaterialRegistry.createIngotMaterial(702, "complex_alloy", 0xF6872E, "shiny", 1, 
    [<material:copper>*3, <material:electrum>*1, <material:redstone>*9, <material:some_fancy_gemstone>*2], 3.5, 0);
```

### 示例五：设置电缆和管道属性

```zenscript
#loader gregtech
import mods.gregtech.material.MaterialRegistry;

var ingotMaterial = MaterialRegistry.createIngotMaterial(2052, "test", 0x1a2f3e, "ingot", 1);
ingotMaterial.setCableProperties(128, 4, 1); // 128EU/t 4A 1 loss/block
ingotMaterial.setFluidPipeProperties(1000, 100, false); // 1000L/t 100K 不防气体
```

### 示例六：添加工具附魔

```zenscript
#loader gregtech
import mods.gregtech.material.MaterialRegistry;

var material = MaterialRegistry.get("iron"); // 修改铁材料
material.addToolEnchantment(<enchantment:minecraft:fortune> * 1); // 添加时运 I
```
