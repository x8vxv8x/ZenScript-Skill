# Immersive Intelligence CraftTweaker API 参考

> Mod ID: `immersiveintelligence`
> 前置条件: Immersive Engineering
> 导入: `import mods.immersiveintelligence.<ClassName>;`

Immersive Intelligence 是 Immersive Engineering 的扩展模组，专注于电子、战争、后勤和情报。

---

## API 列表

### BlockPenetration（方块穿透）

> `import mods.immersiveintelligence.BlockPenetration;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addMaterial(IMaterial material, float integrity, float density, String penetrationType, String sound)` | void | 添加材质硬度。`integrity` 为生命值，`density` 为速度衰减系数。`penetrationType`：`metal`/`ground`/`solid`/`flesh`/`light` |
| `.addMaterial(String name, float integrity, float density)` | void | 添加金属方块硬度（自动生成方块和台阶变体） |
| `.addMaterial(IBlockState state, float integrity, float density, String penetrationType, String sound)` | void | 添加方块硬度 |

---

### Bullets（弹药系统）

> `import mods.immersiveintelligence.bullet.Bullets;`
> `import mods.immersiveintelligence.bullet.CoreMaterialBuilder;`
> `import mods.immersiveintelligence.bullet.ComponentMaterialBuilder;`

#### Bullets 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addShrapnel(String name, int color, String texture, int damage, float mass, float brightness)` | void | 添加弹片。`color` 为 RGB 整数，`brightness` 为 0-1 发光效果 |
| `.removeShrapnel(String name)` | void | 移除弹片 |
| `.removeCore(String name)` | void | 移除弹头核心 |
| `.removeComponent(String name)` | void | 移除弹头组件 |

#### CoreMaterialBuilder（弹头核心构建器）

| 方法 | 返回 | 说明 |
|------|------|------|
| `CoreMaterialBuilder.create(String name)` | CoreMaterialBuilder | 创建构建器 |
| `.setColor(int color)` | CoreMaterialBuilder | 设置颜色（RGB 整数） |
| `.setDensity(float density)` | CoreMaterialBuilder | 设置密度（影响质量和重力） |
| `.setDmgModifier(float modifier)` | CoreMaterialBuilder | 设置伤害倍率（默认 1.0） |
| `.setEffectModifier(float modifier)` | CoreMaterialBuilder | 设置效果倍率（默认 1.0） |
| `.setPenHardness(float hardness)` | CoreMaterialBuilder | 设置穿透硬度 |
| `.setStack(IIngredient stack)` | CoreMaterialBuilder | 设置合成材料 |
| `.register()` | void | 注册 |

#### ComponentMaterialBuilder（弹头组件构建器）

| 方法 | 返回 | 说明 |
|------|------|------|
| `ComponentMaterialBuilder.create(String name)` | ComponentMaterialBuilder | 创建构建器 |
| `.setColor(int color)` | ComponentMaterialBuilder | 设置颜色 |
| `.setDensity(float density)` | ComponentMaterialBuilder | 设置密度 |
| `.setRole(String role)` | ComponentMaterialBuilder | 设置角色。可选：`general_purpose`/`shrapnel`/`piercing`/`explosive`/`incendiary`/`tracer`/`flare`/`chemical`/`special` |
| `.setStack(IIngredient stack)` | ComponentMaterialBuilder | 设置合成材料 |
| `.setComponentEffect(IComponentFunction effect)` | ComponentMaterialBuilder | 设置爆炸效果函数 |
| `.register()` | void | 注册 |

---

### ChemicalBath（化学浸洗器）

> `import mods.immersiveintelligence.ChemicalBath;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, IItemStack itemOutput, ILiquidStack fluidInput, int energy, int time)` | void | 添加配方 |
| `.addWashingRecipe(IIngredient itemInput, IItemStack itemOutput, ILiquidStack fluidInput, int energy, int time)` | void | 添加配方（JEI 分类不同） |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |

---

### ChemicalPainter（化学喷绘机）

> `import mods.immersiveintelligence.ChemicalPainter;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, IChemicalPainterFunction function, int paintAmount, int energy, int time)` | void | 添加配方。`function` 接收 (IItemStack input, int RGBColor, int vanillaColor) 返回 IItemStack |
| `.addWashingRecipe(IIngredient itemInput, IItemStack itemOutput, ILiquidStack fluidInput, int energy, int time)` | void | 添加清洗配方 |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |

---

### CO2Input（CO2 输入）

> `import mods.immersiveintelligence.CO2Input;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addMultiblock(String classPath, int time, int amount, int[] pos)` | void | 添加多方块 CO2 源。`pos` 为多方块内位置（用 `/ct nbt` 获取） |
| `.addTile(String classPath, int time, int amount)` | void | 添加 TileEntity CO2 源 |

---

### Coagulator（凝聚器）

> `import mods.immersiveintelligence.Coagulator;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack itemOutput, ILiquidStack fluidInput, ILiquidStack coagulantInput, int energy, int time)` | void | 添加凝聚配方 |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |

---

### Electrolyzer（电解器）

> `import mods.immersiveintelligence.Electrolyzer;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluidInput, ILiquidStack fluidOutput1, int energy, int time, @Optional ILiquidStack fluidOutput2)` | void | 添加电解配方 |
| `.removeRecipe(ILiquidStack output)` | void | 移除配方 |

---

### Filler（填充机）

> `import mods.immersiveintelligence.Filler;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack itemOutput, IIngredient itemInput, String dust, int amount, int time, int energy)` | void | 添加填充配方 |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |

---

### FuelStation（燃料站）

> `import mods.immersiveintelligence.FuelStation;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addVehicle(String classPath, ILiquidStack[] fluids)` | void | 注册载具燃料 |

---

### LighterFuels（打火机燃料）

> `import mods.immersiveintelligence.LighterFuels;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(ILiquidStack fuelEntry, int amountPerUse)` | void | 添加打火机燃料 |
| `.removeFuel(ILiquidStack fuelEntry)` | void | 移除打火机燃料 |

---

### Machinegun（机枪）

> `import mods.immersiveintelligence.Machinegun;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addCoolant(ILiquidStack coolant, int amountPerUse)` | void | 添加冷却液 |
| `.setCoolAmount(ILiquidStack coolant, int amountPerUse)` | void | 修改已有冷却液消耗量 |
| `.removeCoolant(ILiquidStack coolant)` | void | 移除冷却液 |

---

### PrecisionAssembler（精密装配台）

> `import mods.immersiveintelligence.PrecisionAssembler;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack itemOutput, IItemStack trash, IIngredient[] itemInputs, String[] tools, String[] animations, int energy, float timeMultiplier)` | void | 添加配方。`tools` 为工具名数组，`animations` 为动画命令数组 |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |

工具名：`buzzsaw`(140tick)、`drill`(140tick)、`inserter`(60tick)、`solderer`(80tick)、`welder`(160tick)、`hammer`(40tick)

动画命令格式：`工具 动作 槽位`，如 `inserter pick first`、`drill work main`、`inserter drop main`

槽位：`main`(中)、`first`(左)、`second`(中)、`third`(右)

---

### RotaryInput（旋转输入）

> `import mods.immersiveintelligence.RotaryInput;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addInput(String classPath, float torque)` | void | 注册传输箱支持的 TileEntity |

---

### Sawmill（锯木厂）

> `import mods.immersiveintelligence.Sawmill;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient itemInput, IItemStack itemOutput, IItemStack secondaryItemOutput, int torque, int time, int hardness, int dustColor)` | void | 添加配方。`hardness`：铁=2、钢=3、钨=4。`dustColor` 为 RGB 整数 |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |

---

### Vulcanizer（硫化机）

> `import mods.immersiveintelligence.Vulcanizer;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient mainInput, IIngredient compoundInput, IIngredient sulfurInput, IItemStack itemMold, IItemStack itemOutput, int energy, @Optional String latexTexture, @Optional String rubberTexture)` | void | 添加硫化配方。前 3 个输入槽不限材料 |
| `.removeRecipe(IItemStack output)` | void | 移除配方 |