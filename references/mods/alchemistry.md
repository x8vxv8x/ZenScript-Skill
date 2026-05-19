# Alchemistry CraftTweaker API 参考

> Mod ID: `alchemistry`
> 前置条件: 无
> 导入: `import mods.alchemistry.<ClassName>;`

## API 列表

### Atomizer（雾化器）

> `import mods.alchemistry.Atomizer;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, ILiquidStack input)` | void | 添加雾化配方 |
| `.removeRecipe(ILiquidStack input)` | void | 移除指定输入的配方（不论数量） |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Combiner（化学化合机）

> `import mods.alchemistry.Combiner;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack[] input)` | void | 添加配方 |
| `.addStagedRecipe(IItemStack output, IItemStack[] input, String stage)` | void | 添加带 GameStage 限制的配方 |
| `.setAsStaged(IItemStack output, String stage)` | void | 将已有配方设为需要 GameStage |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Dissolver（化学溶解机）

> `import mods.alchemistry.Dissolver;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient input, boolean relativeProbability, int rolls, Object[][] probabilityGroups)` | void | 添加溶解配方 |
| `.removeRecipe(IIngredient input)` | void | 移除指定输入的配方 |
| `.removeAllRecipes()` | void | 移除所有配方 |

**参数说明：**
- `relativeProbability`：概率计算方式，true 为相对概率，false 为绝对概率
- `rolls`：抽取次数
- `probabilityGroups`：概率组数组，格式为 `[概率值, 输出物品1, 输出物品2, ...]`

### Electrolyzer（电解机）

> `import mods.alchemistry.Electrolyzer;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack input, IItemStack electrolyte, int electrolyteConsumptionChance, IItemStack output1, IItemStack output2, @Nullable IItemStack output3, @Nullable int output3Chance, @Nullable IItemStack output4, @Nullable int output4Chance)` | void | 添加电解配方 |
| `.removeRecipe(ILiquidStack input, IItemStack electrolyte)` | void | 移除指定输入和电解质的配方 |
| `.removeAllRecipes()` | void | 移除所有配方 |

**参数说明：**
- `input`：液体输入
- `electrolyte`：电解质物品
- `electrolyteConsumptionChance`：电解质消耗概率
- `output1-4`：输出物品（output3、output4 可为 null）
- `output3Chance`、`output4Chance`：对应输出的产出概率

### Evaporator（蒸发皿）

> `import mods.alchemistry.Evaporator;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, ILiquidStack input)` | void | 添加蒸发配方 |
| `.removeRecipe(ILiquidStack input)` | void | 移除指定输入的配方（不论数量） |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Liquifier（液化器）

> `import mods.alchemistry.Liquifier;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, IItemStack input)` | void | 添加液化配方 |
| `.removeRecipe(IItemStack input)` | void | 移除指定输入的配方 |
| `.removeAllRecipes()` | void | 移除所有配方 |

### Util（工具类）

> `import mods.alchemistry.Util;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createElement(int atomicNumber, String name, String abbreviation, int red, int green, int blue)` | void | 创建自定义元素 |
| `.createCompound(int meta, String name, int red, int green, int blue, Object[][] components)` | void | 创建自定义化合物 |
| `.get(String name)` | IItemStack | 根据名称获取元素/化合物物品 |

**参数说明：**
- `atomicNumber`：原子序数（唯一标识符，不能与已有元素冲突）
- `name`：元素名称（建议小写）
- `abbreviation`：元素缩写
- `red`、`green`、`blue`：RGB 颜色值
- `meta`：元数据值（唯一标识符，建议从 1000 开始）
- `components`：成分数组，格式为 `[["元素名", 数量], ...]`

**注意：** 创建元素和化合物需要在文件顶部添加 `#loader alchemistry`，且此文件只能用于创建元素和化合物。

## 使用示例

### 示例一：雾化器配方

```zenscript
import mods.alchemistry.Atomizer;

// 将铍液体雾化成红石
Atomizer.addRecipe(<minecraft:redstone>, <liquid:beryllium> * 500);

// 移除配方
Atomizer.removeRecipe(<liquid:iron>);
```

### 示例二：化学溶解机配方

```zenscript
import mods.alchemistry.Dissolver;

// 粉品染料溶解配方
Dissolver.addRecipe(<minecraft:dye:9>, false, 5,
    [[10, <minecraft:stone>],
     [20, <minecraft:sand>, <minecraft:iron_ore>]]);

// 相对概率：33.3% 出石头，66.6% 出沙子和铁矿
// 绝对概率：10% 出石头，20% 出沙子和铁矿
```

### 示例三：创建自定义元素和化合物

```zenscript
#loader alchemistry

import mods.alchemistry.Util;

// 创建自定义元素
Util.createElement(150, "vibranium", "Vrb", 70, 90, 250);

// 创建自定义化合物
Util.createCompound(1000, "vibranium_sulfide", 20, 69, 185,
    [["vibranium", 1],
     ["sulfur", 3]]);
```

### 示例四：使用 GameStage 限制配方

```zenscript
import mods.alchemistry.Combiner;

// 添加需要 GameStage 的配方
Combiner.addStagedRecipe(<minecraft:diamond>, [<minecraft:coal>, <minecraft:coal>], "advanced_technology");

// 将已有配方设为需要 GameStage
Combiner.setAsStaged(<minecraft:gold_ingot>, "advanced_technology");
```

## 注意事项

- 使用 `/dissolver` 命令可以获取手持物品的溶解配方并复制到剪贴板
- 创建元素和化合物的文件必须使用 `#loader alchemistry` 预处理器
- 元素的 atomicNumber 和化合物的 meta 值必须唯一，建议化合物从 1000 开始编号
- 概率支持浮点数，如 4.5 表示 4.5%
