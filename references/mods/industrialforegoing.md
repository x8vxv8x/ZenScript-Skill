# Industrial Foregoing CraftTweaker API 参考

> Mod ID: `industrialforegoing`
> 前置条件: 无
> 导入: `import mods.industrialforegoing.<ClassName>;`

Industrial Foregoing 是一个工业模组，提供多种自动化机器。

---

## API 列表

### BioReactor（生物质炉）

> `import mods.industrialforegoing.BioReactor;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack input)` | void | 添加输入物品 |
| `.remove(IItemStack input)` | void | 移除输入物品 |

---

### FluidDictionary（流体词典转换器）

> `import mods.industrialforegoing.FluidDictionary;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(String input, String output, double rate)` | void | 添加流体转换。`rate` 为转换率（输入mB * rate = 输出mB） |
| `.remove(String input, String output)` | void | 移除流体转换 |

---

### LaserDrill（镭射钻）

> `import mods.industrialforegoing.LaserDrill;`

物品权重说明：选中概率 = 物品权重 / 总权重 * 100%

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(int itemLensMetaColor, IItemStack output, int itemWeight)` | void | 添加镭射钻物品。`itemLensMetaColor` 为透镜颜色元数据 |
| `.remove(IItemStack output)` | void | 移除物品 |

---

### ProteinReactor（蛋白质反应器）

> `import mods.industrialforegoing.ProteinReactor;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack input)` | void | 添加输入物品 |
| `.remove(IItemStack input)` | void | 移除输入物品 |

---

### SludgeRefiner（污泥精炼机）

> `import mods.industrialforegoing.SludgeRefiner;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, int itemWeight)` | void | 添加输出物品 |
| `.remove(IItemStack output)` | void | 移除物品 |

---

### Extractor（树液提取器）

> `import mods.industrialforegoing.Extractor;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, ILiquidStack fluid)` | void | 添加树液提取配方 |
| `.remove(IItemStack input)` | void | 移除配方 |

---

## Integration Foregoing 扩展（需安装 Integration Foregoing）

> Mod ID: `industrialforegoing`

### FermentationStation（发酵站）

> `import mods.industrialforegoing.FermentationStation;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(ILiquidStack fluidInput, ILiquidStack fluidOutput)` | void | 添加发酵配方 |
| `.remove(ILiquidStack fluidInput)` | void | 移除配方（输入流体数量必须匹配） |

### FluidSievingMachine（流体筛分机）

> `import mods.industrialforegoing.FluidSievingMachine;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(ILiquidStack fluidInput, IItemStack itemOutput, IItemStack sieveItemInput)` | void | 添加筛分配方 |
| `.remove(IItemStack itemOutput)` | void | 移除配方（按输出物品） |

### WashingFactory（洗矿厂）

> `import mods.industrialforegoing.WashingFactory;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(String oreDictInput, ILiquidStack fluidInput, ILiquidStack fluidOutput)` | void | 添加配方。`oreDictInput` 为矿辞字符串 |
| `.remove(String oreDictInput)` | void | 移除配方（按矿辞） |