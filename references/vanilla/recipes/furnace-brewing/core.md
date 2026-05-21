# 熔炉、酿造与草丛掉落 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.recipes.IFurnaceRecipe;`

熔炉配方、酿造台配方和草丛掉落操作。

---

## API 列表

### IFurnaceRecipe（熔炉配方）

> `import crafttweaker.recipes.IFurnaceRecipe;`

熔炉配方在 ZenScript 中的表示对象。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `input` | IIngredient | 输入物品 |
| `output` | IItemStack | 输出物品 |
| `xp` | float | 烧炼经验值 |
| `commandString` | string | 配方的命令字符串表示 |

#### 方法

```zenscript
// 获取配方的命令字符串表示（等同于 commandString 属性）
rec.toCommandString();
```

---

## 熔炉配方

### 添加熔炉配方

```zenscript
// 添加：输出, 输入, 经验值（double，可省略）
furnace.addRecipe(<minecraft:iron_ingot>, <minecraft:iron_ore>, 0.7);
furnace.addRecipe(<minecraft:golden_apple>, <minecraft:apple>);  // 不给经验
```

- `furnace.addRecipe(output, input)`: 不给经验值
- `furnace.addRecipe(output, input, xp)`: `xp` 是 double 类型经验值

### 移除熔炉配方

```zenscript
// 移除：输出（移除所有产出该物品的配方）
furnace.remove(<minecraft:iron_ingot>);

// 移除：输出, 输入
furnace.remove(<minecraft:iron_ingot>, <minecraft:iron_ore>);

// 移除所有熔炉配方
furnace.removeAll();
```

- `furnace.remove(output)`: `output` 是 IIngredient
- `furnace.remove(output, input)`: `output` 和 `input` 都是 IIngredient
- `furnace.removeAll()`: 移除所有已注册的熔炉配方

### 燃料

```zenscript
// 设置燃料：物品, 燃烧时间（ticks）。煤炭=1600，烧一个物品=200
furnace.setFuel(<minecraft:coal>, 1600);
furnace.setFuel(<minecraft:coal>, 0);  // 移除燃料

// 获取物品的燃料值（返回 int）
var fuelValue = furnace.getFuel(<minecraft:coal>);
```

- `furnace.setFuel(input, burnTime)`: `input` 是 IIngredient，`burnTime` 是 int（单位 ticks）
- `furnace.getFuel(item)`: `item` 是 IItemStack，返回 int 类型燃烧时间

### 查询熔炉配方

```zenscript
// 获取所有已注册的熔炉配方
var allFurnaceRecipes = furnace.all;  // 返回 List<IFurnaceRecipe>

// 获取物品的熔炉烧炼结果
var result = furnace.getSmeltingResult(<minecraft:iron_ore>);  // 返回 IItemStack
```

---

## 酿造台配方

通过 `brewing` 全局关键字访问酿造台配方处理器。

### 添加酿造配方

```zenscript
// 单个材料
brewing.addBrew(input, ingredient, output);
brewing.addBrew(input, ingredient, output, hidden);  // hidden=true 在 JEI 中隐藏

// 多个材料
brewing.addBrew(input, ingredients, output);
brewing.addBrew(input, ingredients, output, hidden);
```

- `brewing.addBrew(input, ingredient, output, hidden)`:
  - `input`: IIngredient — 瓶子槽中的物品
  - `ingredient`: IIngredient — 顶部槽中的材料
  - `output`: IItemStack — 输出物品
  - `hidden`: 可选 boolean — 是否在 JEI 中隐藏

- `brewing.addBrew(input, ingredients, output, hidden)`:
  - `ingredients`: IIngredient[] — 多个材料的数组

```zenscript
// 简单配方
brewing.addBrew(<ore:blockGlass>, <ore:logWood>, <minecraft:beacon>);

// 在 JEI 中隐藏
brewing.addBrew(<ore:ingotGold>, <minecraft:obsidian>, <minecraft:wool:3>, true);

// 多个材料
brewing.addBrew(<minecraft:bedrock>, [<minecraft:lapis_ore>], <minecraft:sponge:1>);
brewing.addBrew(<minecraft:gold_block>, [<minecraft:iron_block>, <minecraft:lapis_block>], <minecraft:sponge:1>, true);
```

### 移除酿造配方

需要 JEI 4.15.0.275 或更高版本。

```zenscript
brewing.removeRecipe(input, ingredient);
```

- `brewing.removeRecipe(input, ingredient)`:
  - `input`: IItemStack — 瓶子槽中的物品
  - `ingredient`: IItemStack — 顶部槽中的材料

```zenscript
brewing.removeRecipe(<minecraft:potion>.withTag({Potion: "minecraft:water"}), <minecraft:gunpowder>);
```

---

## 草丛掉落

### 控制台命令

在游戏内或控制台执行以下命令可将所有已注册的种子掉落打印到日志（不能写在 zs 文件中）：

```
/ct seeds
```

```zenscript
// 添加打草掉落（百分比权重）
vanilla.seeds.addSeed(<minecraft:carrot> % 1);  // 1% 几率

// 移除打草掉落
vanilla.seeds.removeSeed(<minecraft:wheat_seeds>);

// 获取所有已注册的种子掉落（返回 WeightedItemStack 列表）
var seedList = vanilla.seeds.seeds;
for item in seedList {
    print("Item: " ~ item.stack.displayName ~ " || Chance: " ~ item.percent ~ "%");
}
```

- `vanilla.seeds.addSeed(item)`: `item` 是 WeightedItemStack（使用 `%` 运算符设置权重，小麦种子权重为 10）
- `vanilla.seeds.removeSeed(item)`: `item` 是 IIngredient
- `vanilla.seeds.seeds`: 返回所有已注册种子的 WeightedItemStack 列表
