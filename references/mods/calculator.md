# Calculator CraftTweaker API 参考

> Mod ID: `calculator`
> 前置条件: 无
> 导入: `import mods.calculator.*;`

Calculator 是一个提供多种计算器和处理机器的模组。

---

## API 列表

### Basic Calculator（基础计算器）

> `import mods.calculator.basic;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input1 as IIngredient, input2 as IIngredient, output as IIngredient)` | void | 添加基础计算器配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(output as IIngredient)` | void | 按输出移除配方 |

### Scientific Calculator（科学计算器）

> `import mods.calculator.scientific;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input1 as IIngredient, input2 as IIngredient, output as IIngredient)` | void | 添加科学计算器配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(output as IIngredient)` | void | 按输出移除配方 |

### Atomic Calculator（原子计算器）

> `import mods.calculator.atomic;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input1 as IIngredient, input2 as IIngredient, input3 as IIngredient, output as IIngredient)` | void | 添加原子计算器配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(output as IIngredient)` | void | 按输出移除配方 |

### Flawless Calculator（完美计算器）

> `import mods.calculator.flawless;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input1 as IIngredient, input2 as IIngredient, input3 as IIngredient, input4 as IIngredient, output as IIngredient)` | void | 添加完美计算器配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(output as IIngredient)` | void | 按输出移除配方 |

### Extraction Chamber（提取室）

> `import mods.calculator.extractionChamber;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, output1 as IIngredient, output2 as IIngredient)` | void | 添加提取室配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(output as IIngredient, output2 as IIngredient)` | void | 按输出移除配方 |

### Precision Chamber（精密室）

> `import mods.calculator.precisionChamber;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, output1 as IIngredient, output2 as IIngredient)` | void | 添加精密室配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(output1 as IIngredient, output2 as IIngredient)` | void | 按输出移除配方 |

### Processing Chamber（处理室）

> `import mods.calculator.processingChamber;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, output as IIngredient)` | void | 添加处理室配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(output as IIngredient)` | void | 按输出移除配方 |

### Reassembly Chamber（重组室）

> `import mods.calculator.reassemblyChamber;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, output as IIngredient)` | void | 添加重组室配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(output as IIngredient)` | void | 按输出移除配方 |

### Restoration Chamber（修复室）

> `import mods.calculator.restorationChamber;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, output as IIngredient)` | void | 添加修复室配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(output as IIngredient)` | void | 按输出移除配方 |

### Fabrication Chamber（制造室）

> `import mods.calculator.fabricationChamber;`

注意：未完全实现，只接受一个输入。

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, output as IIngredient)` | void | 添加制造室配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(input as IIngredient)` | void | 按输入移除配方 |

### Algorithm Separator（算法分离器）

> `import mods.calculator.algorithmSeparator;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, output1 as IIngredient, output2 as IIngredient)` | void | 添加算法分离器配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(output1 as IIngredient, output2 as IIngredient)` | void | 按输出移除配方 |

### Stone Separator（石头分离器）

> `import mods.calculator.stoneSeparator;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, output1 as IIngredient, output2 as IIngredient)` | void | 添加石头分离器配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(output as IIngredient, output2 as IIngredient)` | void | 按输出移除配方 |

### Conductor Mast（导体桅杆）

> `import mods.calculator.conductorMast;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, powercost as int, output as IIngredient)` | void | 添加导体桅杆配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(output as IIngredient)` | void | 按输出移除配方 |

### Redstone Extractor（红石提取器）

> `import mods.calculator.redstone;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, value as int)` | void | 添加红石提取器配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(input as IIngredient)` | void | 按输入移除配方 |

### Glowstone Extractor（萤石提取器）

> `import mods.calculator.glowstone;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, value as int)` | void | 添加萤石提取器配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(input as IIngredient)` | void | 按输入移除配方 |

### Starch Extractor（淀粉提取器）

> `import mods.calculator.starch;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, value as int)` | void | 添加淀粉提取器配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(input as IIngredient)` | void | 按输入移除配方 |

### Health Processor（健康处理器）

> `import mods.calculator.health;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, value as int)` | void | 添加健康处理器配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(input as IIngredient)` | void | 按输入移除配方 |

---

## 使用示例

### 基础计算器配方

```zenscript
import mods.calculator.basic;

basic.addRecipe(<minecraft:iron_ingot>, <minecraft:gold_ingot>, <minecraft:diamond>);
```

### 提取室配方

```zenscript
import mods.calculator.extractionChamber;

extractionChamber.addRecipe(<minecraft:iron_ore>, <minecraft:iron_ingot>, <minecraft:gold_nugget>);
```

### 导体桅杆配方

```zenscript
import mods.calculator.conductorMast;

conductorMast.addRecipe(<minecraft:redstone>, 100, <minecraft:redstone_block>);
```

---

## 注意事项

- 所有配方方法都使用 IIngredient 类型
- 移除配方时，某些机器需要指定所有输出
- 制造室未完全实现，只接受一个输入
- 能量消耗单位因机器而异
