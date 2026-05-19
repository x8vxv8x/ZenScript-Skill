# Embers Rekindled CraftTweaker API 参考

> Mod ID: `embers`
> 前置条件: 无
> 导入: `import mods.embers.*;`

Embers Rekindled 是一个以蒸汽朋克为主题的模组，提供多种机器和配方管理。

---

## API 列表

### DawnstoneAnvil（黎明石砧）

> `import mods.embers.DawnstoneAnvil;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(outputs as IItemStack[], inputTop as IIngredient, inputBottom as IIngredient)` | void | 添加黎明石砧配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(inputTop as IIngredient, inputBottom as IIngredient)` | void | 按输入移除配方 |

#### 黑名单方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.blacklistRepair(input as IIngredient)` | void | 禁止修复 |
| `.blacklistMateriaRepair(input as IIngredient)` | void | 禁止材料修复 |
| `.blacklistBreakdown(input as IIngredient)` | void | 禁止分解 |

#### IItemStack 扩展

```zenscript
itemstack.hasHeat(); // 是否有热量
itemstack.getHeat(); // 获取热量
itemstack.setHeat(float level); // 设置热量
itemstack.getMaxHeat(); // 获取最大热量
itemstack.getHeatLevel(); // 获取热量等级
itemstack.setHeatLevel(int level); // 设置热量等级
itemstack.addModifier(IItemStack modifier); // 添加修饰符
Boolean itemstack.isModifierValid(string modifiername); // 修饰符是否有效
Boolean itemstack.hasModifier(string modifiername); // 是否有修饰符
Integer itemstack.getModifierLevel(string modifiername); // 获取修饰符等级
itemstack.setModifierLevel(string modifiername, int level); // 设置修饰符等级
```

#### IIngredient 扩展

```zenscript
ingredient.anyHeat(); // 任何热量
ingredient.onlyHeatAtLeast(float amount); // 热量至少为
ingredient.onlyHeatAtMost(float amount); // 热量至多为
ingredient.onlyHeatLevelAtLeast(int level); // 热量等级至少为
ingredient.onlyHeatLevelAtMost(int level); // 热量等级至多为
ingredient.onlyWithModifier(string modifier); // 只有修饰符
ingredient.onlyWithModifierLevelAtLeast(string modifier, int level); // 修饰符等级至少为
ingredient.onlyWithModifierLevelAtMost(string modifier, int level); // 修饰符等级至多为
ingredient.onlyIfModifierValid(string modifier); // 只有修饰符有效
```

### EmberBore（灰烬晶体开采机）

> `import mods.embers.EmberBore;`
> `import mods.embers.EmberBoreSet;`

#### 创建/获取开采机

```zenscript
var boreset = EmberBore.create(dimensionIDs as int[], biomes as string[]);
var defaultBoreset = EmberBore.getDefault();
```

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addOutput(output as WeightedItemStack)` | void | 添加输出 |
| `.removeOutput(output as IItemStack)` | void | 移除输出 |
| `.clear()` | void | 清空输出 |

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `dimensions` | int[] | 适用维度ID数组 |
| `biomes` | string[] | 适用生物群系数组 |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `stacks` | WeightedItemStack[] | 输出物品数组 |

### EmberGeneration（灰烬能量）

> `import mods.embers.EmberGeneration;`

#### 余烬燃料

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addEmberFuel(item as IIngredient, ember as double)` | void | 添加余烬燃料 ember代表产生的灰烬能量值|
| `.removeEmberFuel(item as IItemStack)` | void | 移除余烬燃料 |

#### 金属块增加参能倍数

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addMetalCoefficient(item as IIngredient, coefficient as double)` | void | 添加系数 |

#### 燃烧/催化室

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addCombustionFuel(item as IIngredient, coefficient as double)` | void | 添加燃烧燃料 |
| `.removeCombustionFuel(item as IItemStack)` | void | 移除燃烧燃料 |
| `.addCatalysisFuel(item as IIngredient, coefficient as double)` | void | 添加催化燃料 |
| `.removeCatalysisFuel(item as IItemStack)` | void | 移除催化燃料 |

#### 锅炉

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addBoilerFluid(fluid as ILiquidStack, gas as ILiquidStack)` | void | 添加锅炉流体 |
| `.removeBoilerFluid(input as ILiquidStack)` | void | 移除锅炉流体 |

#### 反应锅炉

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addSteamEngineFuel(fluid as ILiquidStack, multiplier as double)` | void | 添加燃料 |
| `.removeSteamEngineFuel(fluid as ILiquidStack)` | void | 移除燃料 |

### Alchemy（炼金台）

> `import mods.embers.Alchemy;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(output as IItemStack, inputs as IIngredient[], aspectRange as int[][string])` | void | 添加炼金台配方 |

**注意**: `inputs` 的第一个元素对应炼金台中心。`aspectRange` 必须是关联数组，键为 `string aspect`，值为 `int[] range`。

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(output as IItemStack)` | void | 按输出移除配方 |

#### 自定义方面

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addAspect(name as string, item as IItemStack)` | void | 添加自定义方面 |

### HeatCoil（线圈炉）

> `import mods.embers.HeatCoil;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(output as IItemStack, input as IIngredient)` | void | 添加配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(output as IItemStack)` | void | 按输出移除配方 |

### Melter（熔炼炉）

> `import mods.embers.Melter;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(outputfluid as ILiquidStack, input as IIngredient, @Optional secondaryfluidoutput as ILiquidStack)` | void | 添加熔炼配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(outputfluid as ILiquidStack)` | void | 按输出移除配方 |

### Mixer（混合离心机）

> `import mods.embers.Mixer;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(outputfluid as ILiquidStack, inputfluids as ILiquidStack[])` | void | 添加混合离心机配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(outputfluid as ILiquidStack)` | void | 按输出移除配方 |

### Stamper（压印锤）

> `import mods.embers.Stamper;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(output as IItemStack, liquid as ILiquidStack, stamp as IIngredient, @Optional input as IIngredient)` | void | 添加冲压机配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(output as IItemStack)` | void | 按输出移除配方 |