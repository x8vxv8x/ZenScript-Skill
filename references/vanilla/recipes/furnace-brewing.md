# 熔炉、酿造与其他配方 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.recipes.IFurnaceRecipe;`

熔炉配方、酿造台配方和其他配方操作。

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

---

## 遍历所有配方

```zenscript
for recipe in recipes.all {
    if (recipe.ingredients1D has <minecraft:iron_ingot>) {
        recipes.removeByRecipeName(recipe.name);
    }
}
```

---

## 数据驱动合成修改

使用映射保存配方信息，批量处理。

```zenscript
import crafttweaker.item.IItemStack;
import crafttweaker.item.IIngredient;

// 有序配方映射
val shapedRecipes as IIngredient[][][IItemStack] = {
    <minecraft:iron_block> : [
        [<ore:ingotIron>, <ore:ingotIron>, <ore:ingotIron>],
        [<ore:ingotIron>, <ore:ingotGold>, <ore:ingotIron>],
        [<ore:ingotIron>, <ore:ingotIron>, <ore:ingotIron>]
    ],
    <minecraft:stick> * 4 : [
        [<ore:plankWood>, null],
        [null, <ore:plankWood>]
    ]
};

// 无序配方映射
val shapelessRecipes as IIngredient[][IItemStack] = {
    <minecraft:grass> : [<minecraft:dirt>, <minecraft:sapling:*>]
};

// 禁用物品列表
val bannedItems as IItemStack[] = [
    <extrautils2:angelring:*>,
    <mekanism:basicblock:6>
];

// 执行修改
for item, ingredients in shapedRecipes {
    recipes.remove(item);
    recipes.addShaped(item, ingredients);
}

for item, ingredients in shapelessRecipes {
    recipes.remove(item);
    recipes.addShapeless(item, ingredients);
}

for item in bannedItems {
    recipes.remove(item);
}
```

---

## 常见配方模式

### 批量修改配方（循环）

```zenscript
import crafttweaker.item.IItemStack;

var logs as IItemStack[] = [
    <minecraft:log>, <minecraft:log:1>, <minecraft:log:2>,
    <minecraft:log:3>, <minecraft:log:4>, <minecraft:log:5>
];
var planks as IItemStack[] = [
    <minecraft:planks>, <minecraft:planks:1>, <minecraft:planks:2>,
    <minecraft:planks:3>, <minecraft:planks:4>, <minecraft:planks:5>
];

for i, log in logs {
    var plank = planks[i];
    recipes.removeShapeless(plank, [log]);
    recipes.addShapeless(plank * 2, [log]);
}
```

### 用 IItemDefinition 批量操作

```zenscript
import crafttweaker.item.IItemDefinition;
val woolDef as IItemDefinition = <minecraft:wool>.definition;

for i in 0 to 16 {
    recipes.remove(woolDef.makeStack(i));
}
```

### NBT 物品配方

```zenscript
// 带 NBT 的输出
recipes.addShapeless("soap", <minecraft:iron_ingot>.withTag({display: {Name: "肥皂"}}),
    [<ore:dirt>, <ore:dirt>, <minecraft:clay_ball>]);

// 带 NBT 的输入（精确匹配）
recipes.addShaped("nbt_recipe", <minecraft:diamond>, [
    [<minecraft:iron_ingot>.withTag({Unbreakable: 1}), null, null],
    [null, null, null],
    [null, null, null]
]);
```

### 条件加载（多 mod 兼容）

```zenscript
#modloaded thermalfoundation
#priority 10
import crafttweaker.item.IItemStack;

// 只有热力基础加载时才执行
recipes.remove(<thermalfoundation:material:128>);
recipes.addShaped("copper_ingot", <thermalfoundation:material:128>, [
    [<ore:oreCopper>]
]);
```

### 物品转换器组合

```zenscript
// 工具不消耗 + 掉耐久
recipes.addShapeless("plank_axe", <minecraft:planks> * 6, [
    <minecraft:iron_axe>.reuse().transformDamage(), <minecraft:log>
]);

// 物品转换：牛奶桶 → 空桶
recipes.addShapeless("cake", <minecraft:cake>, [
    <minecraft:milk_bucket>.transformReplace(<minecraft:bucket>),
    <minecraft:sugar>, <minecraft:wheat>, <minecraft:egg>
]);
```
