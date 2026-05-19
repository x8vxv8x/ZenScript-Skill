# Cuisine CraftTweaker API 参考

> Mod ID: `cuisine`
> 前置条件: 无
> 导入: `import mods.cuisine.*;`

Cuisine 是一个关于烹饪艺术的模组，提供多种烹饪设备的配方管理。

---

## API 列表

### AxeChopping（斧头砍伐）

> `import mods.cuisine.AxeChopping;`

#### 检查是否启用

```zenscript
if (AxeChopping.isEnabled()) {
    // 执行操作
}
```

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(input as IItemStack, output as IItemStack)` | void | 添加斧头砍伐配方 |
| `.add(input as IOreEntry, output as IItemStack)` | void | 使用矿辞添加配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(input as IItemStack)` | void | 按输入移除配方 |
| `.removeByOutput(output as IItemStack)` | void | 按输出移除配方 |
| `.remove(id as string)` | void | 按ID移除配方 |
| `.removeAll()` | void | 移除所有配方 |

#### 其他方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getDefaultPlanksOutput()` | int | 获取默认木板产出数量 |
| `.getDefaultStickOutput()` | int | 获取默认木棍产出数量 |

### BasinHeating（盆加热）

> `import mods.cuisine.BasinHeating;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(input as ILiquidStack, output as IItemStack)` | void | 添加盆加热配方（热量值为1） |
| `.add(input as ILiquidStack, output as IItemStack, heatValue as int)` | void | 添加盆加热配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(input as ILiquidStack)` | void | 按输入移除配方 |
| `.remove(id as string)` | void | 按ID移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### Mill（磨）

> `import mods.cuisine.Mill;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(input as IIngredient, inputFluid as ILiquidStack, output as IItemStack, outputFluid as ILiquidStack)` | void | 添加磨配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(input as IItemStack, inputFluid as ILiquidStack)` | void | 按输入移除配方 |
| `.remove(input as IOreEntry, inputFluid as ILiquidStack)` | void | 使用矿辞移除配方 |
| `.remove(id as string)` | void | 按ID移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### Mortar（臼）

> `import mods.cuisine.Mortar;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(inputs as IItemStack[], output as IItemStack, step as int)` | void | 添加臼配方 |

**参数说明**:
- `inputs`: 输入物品数组
- `output`: 输出物品
- `step`: 需要按下研杵的次数

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(input as IItemStack[])` | void | 按输入移除配方 |
| `.removeByOutput(output as IIngredient)` | void | 按输出移除配方 |
| `.remove(id as string)` | void | 按ID移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### BasinSqueezing（盆挤压）

> `import mods.cuisine.BasinSqueezing;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(input as IIngredient, output as ILiquidStack, @Optional extraOutput as IItemStack)` | void | 添加盆挤压配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(input as IItemStack, inputFluid as ILiquidStack)` | void | 按输入移除配方 |
| `.remove(id as string)` | void | 按ID移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### BasinThrowing（盆投掷）

> `import mods.cuisine.BasinThrowing;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(input as IIngredient, inputFluid as ILiquidStack, output as IItemStack)` | void | 添加盆投掷配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(input as IItemStack, inputFluid as ILiquidStack)` | void | 按输入移除配方 |
| `.remove(id as string)` | void | 按ID移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### Vessel（容器）

> `import mods.cuisine.Vessel;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(input as IItemStack, inputFluid as ILiquidStack, output as IItemStack, outputFluid as ILiquidStack, @Optional extra as IItemStack)` | void | 添加容器配方 |
| `.add(input as IOreDictEntry, inputFluid as ILiquidStack, output as IItemStack, outputFluid as ILiquidStack, @Optional extra as IOreDictEntry)` | void | 使用矿辞添加配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(input as IItemStack, inputFluid as ILiquidStack, @Optional extra as IItemStack)` | void | 按输入移除配方 |
| `.remove(input as IOreDictEntry, inputFluid as ILiquidStack, @Optional extra as IOreDictEntry)` | void | 使用矿辞移除配方 |
| `.remove(id as string)` | void | 按ID移除配方 |
| `.removeAll()` | void | 移除所有配方 |
