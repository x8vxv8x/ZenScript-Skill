# EnderIO CraftTweaker API 参考

> Mod ID: `enderio`
> 前置条件: EnderTweaker
> 导入: `import mods.enderio.*;`

EnderIO 模组的 CraftTweaker 集成，支持修改合金冶炼炉、SAG 磨粉机、巫术酿造釜、灵魂绑定器、储罐、附魔台、燃烧发电机等机器的配方。

---

## API 列表

### AlloySmelter（合金炉）

> `import mods.enderio.AlloySmelter;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient[] input, @Optional int energyCost, @Optional float xp)` | void | 添加配方。input 需 1~3 个材料；energyCost 默认 5000 FE；xp 不可为负 |
| `.removeRecipe(IItemStack output)` | void | 按输出移除配方 |
| `.removeByInputs(IItemStack... input)` | void | 按输入移除配方 |

---

### SagMill（SAG 磨粉机）

> `import mods.enderio.SagMill;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack[] output, float[] chances, IIngredient input, @Optional String bonusType, @Optional int energyCost, @Optional float[] xp)` | void | 添加配方。chances 长度须与 output 相同；bonusType 影响研磨球效果：`NONE`（无加成）、`MULTIPLY_OUTPUT`（概率可超 1.0）、`CHANCE_ONLY`（概率上限 1.0）；energyCost 默认 5000 FE |
| `.addRecipe(WeightedItemStack[] output, IIngredient input, @Optional String bonusType, @Optional int energyCost, @Optional float[] xp)` | void | 添加配方（使用 WeightedItemStack 形式） |
| `.removeRecipe(IItemStack input)` | void | 按输入移除配方 |

---

### Vat（酿液桶）

> `import mods.enderio.Vat;`

巫术酿造釜使用乘数系统计算输出。输入→输出流体比例恒定，等于 `inMult`。

- 每次合成消耗输入流体：`slot1Mult × slot2Mult × 1000 mb`
- 输出流体量：`inMult × slot1Mult × slot2Mult × 1000 mb`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, float inMult, ILiquidStack input, IIngredient[] slot1Solids, float[] slot1Mults, IIngredient[] slot2Solids, float[] slot2Mults, @Optional int energyCost)` | void | 添加配方。output/input 的数量参数被忽略；slot1Mults 长度须与 slot1Solids 相同；slot2Mults 长度须与 slot2Solids 相同；energyCost 默认 5000 FE |
| `.removeRecipe(ILiquidStack output)` | void | 按输出流体移除配方 |

---

### SliceNSplice（头颅装配机）

> `import mods.enderio.SliceNSplice;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient[] input, @Optional int energyCost, @Optional float xp)` | void | 添加配方。input 需 1~6 个材料；energyCost 默认 5000 FE |
| `.removeRecipe(IItemStack output)` | void | 按输出移除配方 |

---

### SoulBinder（灵魂绑定器）

> `import mods.enderio.SoulBinder;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input, String[] entities, int xp, @Optional int energyCost)` | void | 添加配方。input 为非灵魂瓶主材料；entities 为允许的实体 ID 数组，需在灵魂瓶中存在；xp 为经验等级消耗；energyCost 默认 5000 FE |
| `.removeRecipe(IItemStack output)` | void | 按输出移除配方 |

---

### Enchanter（附魔器）

> `import mods.enderio.Enchanter;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IEnchantmentDefinition output, IIngredient input, int amountPerLevel, double costMultiplier)` | void | 添加配方。amountPerLevel 为每级附魔所需输入物品数；costMultiplier 用于调整配方花费 |
| `.removeRecipe(IEnchantmentDefinition output)` | void | 按输出附魔移除配方 |

---

### CombustionGen（燃烧发电机）

> `import mods.enderio.CombustionGen;`

燃烧发电机不使用配方系统，而是通过燃料和冷却液决定能量产出。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(ILiquidStack fuel, int powerPerCycleRF, int totalBurnTime)` | void | 添加燃料。powerPerCycleRF 为基准机器每 tick 产能；totalBurnTime 为一桶燃料的总燃烧时间 |
| `.addCoolant(ILiquidStack coolant, float degreesCoolingPerMB)` | void | 添加冷却液。degreesCoolingPerMB 为每 mb 冷却液吸收的热量（升温 1K 所需） |
| `.removeFuel(ILiquidStack fuel)` | void | 移除燃料 |
| `.removeCoolant(ILiquidStack coolant)` | void | 移除冷却液 |

---

### Tank（储罐）

> `import mods.enderio.Tank;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(boolean fill, IIngredient input, ILiquidStack fluid, IItemStack output)` | void | 添加配方。fill 为 true 时消耗流体（填充），为 false 时产生流体（排空） |
| `.removeRecipe(boolean fill, ILiquidStack fluid, IItemStack output)` | void | 按参数移除配方 |

---

## 使用示例

### 合金炉

```zenscript
import mods.enderio.AlloySmelter;

// 添加配方：铁锭 + 金锭 + 红石 → 合金锭，消耗 10000 FE
AlloySmelter.addRecipe(<minecraft:diamond>, [<minecraft:iron_ingot>, <minecraft:gold_ingot>, <minecraft:redstone>], 10000, 0.5);

// 按输出移除
AlloySmelter.removeRecipe(<enderio:item_alloy_ingot:0>);

// 按输入移除
AlloySmelter.removeByInputs(<minecraft:iron_ingot>, <minecraft:gold_ingot>);
```

### SAG 磨粉机

```zenscript
import mods.enderio.SagMill;

// 添加配方：圆石 → 沙砾(50%) + 沙子(30%) + 燧石(10%)
SagMill.addRecipe(
    [<minecraft:gravel>, <minecraft:sand>, <minecraft:flint>],
    [0.5, 0.3, 0.1],
    <minecraft:cobblestone>,
    "MULTIPLY_OUTPUT",
    5000,
    [0.1, 0.1, 0.1]
);

// 按输入移除
SagMill.removeRecipe(<minecraft:cobblestone>);
```

### 酿液桶

```zenscript
import mods.enderio.Vat;

// 添加配方：水 + 铁锭(乘数 2.0) + 红石(乘数 1.5) → 岩浆
// 每次消耗: 2.0 × 1.5 × 1000 = 3000 mb 水
// 输出: inMult × 2.0 × 1.5 × 1000 mb 岩浆
Vat.addRecipe(<liquid:lava>, 1.0, <liquid:water>,
    [<minecraft:iron_ingot>], [2.0],
    [<minecraft:redstone>], [1.5],
    8000
);
```

### 灵魂绑定器

```zenscript
import mods.enderio.SoulBinder;

// 添加配方：需要苦力怕灵魂瓶
SoulBinder.addRecipe(<minecraft:diamond>, <minecraft:coal_block>, ["minecraft:creeper"], 5, 10000);
```

### 附魔器

```zenscript
import mods.enderio.Enchanter;

// 添加配方：每级锋利需要 3 个烈焰粉，花费倍率 2.0
Enchanter.addRecipe(<enchantment:minecraft:sharpness>, <minecraft:blaze_powder>, 3, 2.0);
```

### 燃烧发电机

```zenscript
import mods.enderio.CombustionGen;

// 添加燃料：每 tick 产出 100 FE，一桶燃烧 1000 tick
CombustionGen.addFuel(<liquid:lava>, 100, 1000);

// 添加冷却液：每 mb 吸收 10 升温
CombustionGen.addCoolant(<liquid:water>, 10.0);
```

---

## 注意事项

- 所有机器默认能量消耗为 5000 FE（@Optional 参数）
- xp 参数不可为负数
- SAG 磨粉机的 bonusType 影响研磨球行为：`NONE` 无加成、`MULTIPLY_OUTPUT` 允许概率超 100%、`CHANCE_ONLY` 概率上限 100%
- 酿液桶的输出/输入流体数量参数被忽略，实际量由乘数系统计算
- 灵魂绑定器需要实体以灵魂瓶形式存在
- 燃烧发电机不是配方系统，使用独立的燃料和冷却液管理
