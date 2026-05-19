# Better With Mods CraftTweaker API 参考

> Mod ID: `betterwithmods`
> 前置条件: Modtweaker
> 导入: `import mods.betterwithmods.*;`

## API 列表

### Anvil（熔魂钢钢砧，4x4 合成）

> `import mods.betterwithmods.Anvil;`

**注意**: 由于 ModTweaker 的旧 bug，熔魂钢钢砧配方会沿对角线翻转。使用 `addShapedFixed`/`removeShapedFixed` 可修复此问题。

#### 有序合成方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addShaped(IItemStack output, IIngredient[][] inputs)` | void | 添加 4x4 有序配方（有翻转 bug） |
| `.addShapedFixed(IItemStack output, IIngredient[][] inputs)` | void | 添加 4x4 有序配方（修复版） |
| `.removeShaped(IItemStack output, @Optional IIngredient[][] inputs)` | void | 移除有序配方 |
| `.removeShapedFixed(IItemStack output, @Optional IIngredient[][] inputs)` | void | 移除有序配方（修复版） |

#### 无序合成方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addShapeless(IItemStack output, IIngredient[] inputs)` | void | 添加无序配方 |
| `.removeShapeless(IItemStack output, @Optional IIngredient[] inputs)` | void | 移除无序配方 |

#### 清除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeAll()` | void | 清除所有熔魂钢钢砧配方 |

### Bellows（风箱）

> `import mods.betterwithmods.Bellows;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.set(IItemStack stack, float value)` | void | 设置物品被风吹动的距离。`value` 范围 (0, 128]，数值越大吹得越远 |

### Buoyancy（浮力）

> `import mods.betterwithmods.Buoyancy;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.set(IItemStack stack, float value)` | void | 设置物品浮力。`value` 范围 -1 到 1：-1 直接沉底，0 悬浮，1 浮在水面 |

### Cauldron（釜锅）

> `import mods.betterwithmods.Cauldron;`

#### 基础配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addUnstoked(IIngredient[] inputs, IItemStack[] outputs)` | void | 添加无火釜锅配方 |
| `.addStoked(IIngredient[] inputs, IItemStack[] outputs)` | void | 添加有火釜锅配方 |
| `.remove(IItemStack[] outputs)` | void | 按输出移除配方 |
| `.removeAll()` | void | 清除所有配方 |

#### Builder 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.builder()` | CauldronBuilder | 创建配方构建器 |
| `builder.buildRecipe(IIngredient[] inputs, IItemStack[] outputs)` | CauldronBuilder | 设置输入输出 |
| `builder.setPriority(int priority)` | CauldronBuilder | 设置优先级（越低越优先，默认 0） |
| `builder.setHeat(int heat)` | CauldronBuilder | 设置热量需求（无火=1，有火=2） |
| `builder.setIgnoreHeat(boolean ignoreHeat)` | CauldronBuilder | 设置忽略热量 |
| `builder.build()` | void | 注册配方 |

### Crucible（坩埚）

> `import mods.betterwithmods.Crucible;`

#### 基础配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addUnstoked(IIngredient[] inputs, IItemStack[] outputs)` | void | 添加无火坩埚配方 |
| `.addStoked(IIngredient[] inputs, IItemStack[] outputs)` | void | 添加有火坩埚配方 |
| `.remove(IItemStack[] outputs)` | void | 按输出移除配方 |
| `.removeAll()` | void | 清除所有配方 |

#### Builder 方法（同 Cauldron）

### Kiln（窑炉）

> `import mods.betterwithmods.Kiln;`

**注意**: 输入**必须**有关联的方块状态。

#### 基础配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IIngredient input, IItemStack[] output)` | void | 添加窑炉配方 |
| `.remove(IIngredient input)` | void | 按输入移除配方 |
| `.remove(IItemStack[] outputs)` | void | 按输出移除配方 |
| `.removeAll()` | void | 清除所有配方 |
| `.registerBlock(IItemStack input)` | void | 注册窑炉结构方块（输入必须是方块） |

#### Builder 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.builder()` | KilnBuilder | 创建配方构建器 |
| `builder.buildRecipe(IIngredient input, IItemStack[] outputs)` | KilnBuilder | 设置输入输出 |
| `builder.setHeat(int heat)` | KilnBuilder | 设置热量需求 |
| `builder.setIgnoreHeat(boolean ignoreHeat)` | KilnBuilder | 设置忽略热量 |
| `builder.build()` | void | 注册配方 |

### Mill（磨石）

> `import mods.betterwithmods.Mill;`

#### 基础配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient[] inputs, IItemStack[] outputs)` | void | 添加磨石配方 |
| `.remove(IItemStack[] outputs)` | void | 按输出移除配方 |
| `.removeAll()` | void | 清除所有配方 |

#### Builder 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.builder()` | MillBuilder | 创建配方构建器 |
| `builder.buildRecipe(IIngredient[] inputs, IItemStack[] outputs)` | MillBuilder | 设置输入输出 |
| `builder.setPriority(int priority)` | MillBuilder | 设置优先级 |
| `builder.setGrindType(String soundLocation)` | MillBuilder | 设置研磨音效 |
| `builder.setTicks(int ticks)` | MillBuilder | 设置配方时长(tick) |
| `builder.build()` | void | 注册配方 |

### Saw（锯）

> `import mods.betterwithmods.Saw;`

**注意**: 输入**必须**有关联的方块状态。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IIngredient input, IItemStack[] output)` | void | 添加锯配方 |
| `.remove(IIngredient input)` | void | 按输入移除配方 |
| `.remove(IItemStack[] outputs)` | void | 按输出移除配方 |
| `.removeAll()` | void | 清除所有配方 |

### Turntable（螺杆旋转台）

> `import mods.betterwithmods.Turntable;`

**注意**: 输入**必须**有关联的方块状态。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IIngredient input, IItemStack productState, IItemStack[] output)` | void | 添加螺杆旋转台配方（带变换后方块） |
| `.add(IIngredient input, IItemStack[] output)` | void | 添加螺杆旋转台配方 |
| `.remove(IIngredient input)` | void | 按输入移除配方 |
| `.removeAll()` | void | 清除所有配方 |
| `.removeRecipe(IItemStack productState)` | void | 按变换后方块移除配方 |

### FilteredHopper（滤筛漏斗）

> `import mods.betterwithmods.FilteredHopper;`

#### 过滤器管理

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFilter(String name, IIngredient item)` | void | 创建新过滤器并指定过滤槽物品 |
| `.addFilteredItem(String name, IIngredient item)` | void | 向过滤器添加允许通过的物品 |
| `.clearFilter(String name)` | void | 清除指定过滤器的允许物品 |

#### 过滤配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFilterRecipe(String name, IIngredient input, IIngredient[] insideOutput, IIngredient[] outsideOutput)` | void | 添加过滤配方。`insideOutput` 进入漏斗库存，`outsideOutput` 弹出到世界 |
| `.addSoulUrnRecipe(IIngredient input, IItemStack[] outputs, IItemStack[] secondary)` | void | 添加灵魂瓮配方 |
| `.removeRecipe(IIngredient[] insideOutput, IIngredient[] outsideOutput)` | void | 按输出移除配方 |
| `.removeRecipeByInput(IIngredient input)` | void | 按输入移除配方 |

### HeatRegistry（热量注册表）

> `import mods.betterwithmods.HeatRegistry;`

**默认值**: 原版火焰 = 1，助燃火焰 = 2

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addHeatSource(IItemStack stack, int heat)` | void | 添加热量源（物品需有关联方块状态） |
| `.addHeatSource(IBlockState stack, int heat)` | void | 添加热量源（方块状态） |
| `.addHeatSource(IBlockState[] stacks, IItemStack displayStack, int heat)` | void | 添加热量源（多方块状态合并显示） |

### HCFurnace（熔炉）

> `import mods.betterwithmods.Misc;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setFurnaceSmeltingTime(IIngredient ingredient, int time)` | void | 设置熔炉冶炼时间(tick) |

### HCMovement（移动）

> `import mods.betterwithmods.Movement;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.set(IItemStack stack, float value)` | void | 设置方块移动速度。`value` 0-2：1 为正常速度，<1 减速，>1 加速。**只接受方块** |

### MiniBlocks（迷你方块）

> `import mods.betterwithmods.MiniBlocks;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getMiniBlock(String type, IIngredient parentBlock)` | IIngredient | 获取迷你方块。`type` 为 "siding"、"moulding" 或 "corner" |

### PulleyManager（滑轮管理器）

> `import mods.betterwithmods.PulleyManager;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addPulleyBlock(IBlockState state)` | void | 添加锚和滑轮可拉动的方块 |

## 使用示例

### 添加釜锅 Builder 配方

```zenscript
import mods.betterwithmods.Cauldron;

Cauldron.builder().buildRecipe([<ore:stone>], [<minecraft:dirt>]).setHeat(2).setPriority(-1).build();
```

### 添加磨石配方

```zenscript
import mods.betterwithmods.Mill;

Mill.addRecipe([<minecraft:dirt>], [<minecraft:stone>]);
```

### 添加窑炉配方

```zenscript
import mods.betterwithmods.Kiln;

Kiln.add(<minecraft:fence>, [<minecraft:stick>, <minecraft:stick>]);
```
