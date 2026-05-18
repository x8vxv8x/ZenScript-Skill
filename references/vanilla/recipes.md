# Recipes API

## 工作台配方

### 添加有序合成

```zenscript
recipes.addShaped(recipeName, output, inputBox);
recipes.addShapedMirrored(recipeName, output, inputBox);  // 可翻转
recipes.addHiddenShaped(recipeName, output, inputBox);    // JEI 隐藏
```

- `recipeName`: string，配方 ID，不能重复。省略则自动生成哈希名
- `output`: IItemStack，输出物品
- `inputBox`: IIngredient[][]，二维数组，每行最多 3 个，最多 3 行

`addHiddenShaped` 还支持一个可选的 `mirrored` boolean 参数，省略则为 false。

```zenscript
// 铁腿甲
recipes.addShaped("iron_leggings", <minecraft:iron_leggings>, [
    [<ore:ingotIron>, <ore:ingotIron>, <ore:ingotIron>],
    [<ore:ingotIron>, null, <ore:ingotIron>],
    [<ore:ingotIron>, null, <ore:ingotIron>]
]);

// 多输出数量
recipes.addShaped("sticks", <minecraft:stick> * 4, [
    [null, <ore:plankWood>],
    [null, <ore:plankWood>]
]);

// 可翻转（像弓）
recipes.addShapedMirrored("bow", <minecraft:bow>, [
    [null, <minecraft:stick>, <minecraft:string>],
    [<minecraft:stick>, null, <minecraft:string>],
    [null, <minecraft:stick>, <minecraft:string>]
]);
```

### 添加无序合成

```zenscript
recipes.addShapeless(recipeName, output, inputList);
recipes.addHiddenShapeless(recipeName, output, inputList);
```

- `inputList`: IIngredient[]，一维数组

```zenscript
recipes.addShapeless("ender_eye", <minecraft:ender_eye>, [
    <minecraft:ender_pearl>, <minecraft:blaze_powder>
]);
```

### 移除配方

```zenscript
// 移除物品的所有配方
recipes.remove(<minecraft:iron_pickaxe>);

// 移除物品的所有配方（可选 NBT 匹配）
recipes.remove(<minecraft:iron_pickaxe>, true);  // true = 仅移除 NBT 完全匹配的配方

// 移除特定有序配方（inputBox 可省略表示匹配所有）
recipes.removeShaped(<minecraft:stick> * 4, [
    [<ore:plankWood>],
    [<ore:plankWood>]
]);

// 移除特定无序配方
recipes.removeShapeless(<minecraft:book>, [
    <minecraft:paper>, <minecraft:paper>, <minecraft:paper>, <minecraft:leather>
]);

// 移除特定无序配方（wildcard=true 时允许配方含有未指定的额外材料）
recipes.removeShapeless(<minecraft:book>, [
    <minecraft:paper>, <minecraft:leather>
], true);

// 按配方 ID 移除
recipes.removeByRecipeName("minecraft:golden_chestplate");

// 按正则匹配移除
recipes.removeByRegex("minecraft:.*_sword");

// 按输入材料移除（移除所有以该物品为输入的配方）
recipes.removeByInput(<minecraft:iron_ingot>);

// 移除某 mod 所有配方
recipes.removeByMod("botania");

// 移除所有配方
recipes.removeAll();
```

- `recipes.remove(output, NBTMatch)`: `output` 是 IIngredient，`NBTMatch` 是可选的 boolean（默认 false），为 true 时仅移除 NBT 数据完全匹配的配方
- `recipes.removeShapeless(output, inputs, wildcard)`: `wildcard` 是可选的 boolean（默认 false），为 true 时会移除含有指定材料但不限制其他材料的无序配方
- `recipes.removeByInput(ingredient)`: `ingredient` 是 IIngredient，移除所有包含该材料作为输入的配方

### 查询配方

```zenscript
// 获取所有已注册的工作台配方
var allRecipes = recipes.all;  // 返回 List<ICraftingRecipe>

// 获取包含指定材料的所有配方
var ironRecipes = recipes.getRecipesFor(<minecraft:iron_ingot>);  // 返回 List<ICraftingRecipe>
```

### 替换配方材料

```zenscript
// 将配方中所有某材料替换为另一材料
recipes.replaceAllOccurences(<minecraft:stick>, <minecraft:stone>);

// 仅替换特定输出配方中的材料
recipes.replaceAllOccurences(<ore:gemDiamond>, <ore:blockDiamond>, <minecraft:diamond_sword>);

// 替换时可使用条件过滤输出
recipes.replaceAllOccurences(<ore:gunpowder>, <minecraft:tnt>, <*>.only(function(item) {
    return !isNull(item) & !<minecraft:tnt>.matches(item);
}));
```

- `recipes.replaceAllOccurences(toReplace, replaceWith, forOutput)`: `toReplace` 是要被替换的 IIngredient，`replaceWith` 是替换后的 IIngredient，`forOutput` 是可选的 IIngredient 用于限定只替换特定输出的配方

### 模拟合成

```zenscript
// 根据输入内容模拟合成，返回 IItemStack 或 null
var result = recipes.craft([[<minecraft:iron_ingot>]]);
```

- `recipes.craft(content)`: `content` 是 IItemStack[][]，返回 IItemStack（找到配方时）或 null（未找到配方时）

---

## 配方函数（Recipe Function）

配方函数是 `recipes.addShaped` / `recipes.addShapeless` 的第 4 个参数，用于动态决定输出。

```zenscript
recipes.addShaped(recipeName, output, inputBox, recipeFunction, recipeAction);
```

### IRecipeFunction

- `out`: IItemStack — 配方定义的输出
- `ins`: 映射 — 包含所有 `.marked()` 标记的输入物品
- `info`: ICraftingInfo — 合成信息（player, inventory 等）

返回值：
- 返回 IItemStack 作为实际输出
- 返回 null 表示不可合成

注意：此函数在合成网格每次变化时触发，而非取出结果时。不建议在此函数中修改 `ins`。

### IRecipeAction

配方事件是第 5 个参数，在合成完成后执行。此函数仅在结果与配方输出完全相同时触发。

- `out`: IItemStack — 合成结果
- `info`: ICraftingInfo — 合成信息
- `player`: IPlayer — 合成的玩家（**可能为 null**）

### 示例

#### 假合成（JEI 可见但不可用）

```zenscript
recipes.addShapeless("fake", <minecraft:diamond>, [<ore:dirt>, <ore:dirt>, <ore:dirt>],
    function(out, ins, info) {
        return null;  // 永不输出
    },
null);
```

#### 条件合成（仅下界可用）

```zenscript
recipes.addShapeless("nether_recipe", <minecraft:netherrack>,
    [<ore:cobblestone>, <ore:cobblestone>, <ore:cobblestone>],
    function(out, ins, info) {
        return info.player.world.dimension == -1 ? out : null;
    },
null);
```

#### 继承 NBT 的升级配方

```zenscript
import crafttweaker.data.IData;

recipes.addShaped("upgrade", <minecraft:diamond_pickaxe>, [
    [<ore:gemDiamond>, <ore:gemDiamond>, <ore:gemDiamond>],
    [null, <minecraft:golden_pickaxe:*>.marked("p"), null]
],
function(out, ins, info) {
    var data as IData = ins.p.tag;  // 获取标记物品的 NBT
    return out.withTag(data);        // 继承到输出
},
null);
```

#### 修复工具（Meta 值操控）

```zenscript
recipes.addShapeless("repair", <minecraft:diamond_pickaxe>,
    [<minecraft:diamond_pickaxe>.onlyDamaged().marked("p"), <minecraft:diamond>],
    function(out, ins, info) {
        return ins.p.withDamage(max(0, ins.p.damage - 500));
    },
null);
```

#### 合成后扣血

```zenscript
recipes.addShapeless("hurt_recipe", <minecraft:sapling>,
    [<minecraft:stick>, <minecraft:leaves>],
    function(out, ins, info) {
        return info.player.health > 5 ? out : null;  // 血量 > 5 才能合成
    },
    function(out, info, player) {
        player.attackEntityFrom(<damageSource:MAGIC>, 5.0f);  // 扣 5 血
    }
);
```

---

## 标记物品（Marked）

使用 `.marked("name")` 标记输入物品，配方函数中通过 `ins.name` 访问。

```zenscript
recipes.addShaped("test", <minecraft:iron_pickaxe>, [
    [<ore:ingotIron>, <ore:ingotIron>, <ore:ingotIron>],
    [null, <minecraft:stick>.marked("stick"), null],
    [null, <minecraft:stick>, null]
],
function(out, ins, info) {
    // ins.stick 访问标记的木棍
    return out;
},
null);
```

---

## ICraftingRecipe

工作台配方在 ZenScript 中的表示对象。

导入：`import crafttweaker.recipes.ICraftingRecipe`

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `output` | IItemStack | 配方输出（可能为 null） |
| `ingredients1D` | IIngredient[] | 一维材料列表 |
| `ingredients2D` | IIngredient[][] | 二维材料列表 |
| `shaped` | boolean | 是否为有序配方 |
| `hidden` | boolean | 是否隐藏 |
| `hasTransformers` | boolean | 是否含有转换器 |
| `hasRecipeFunction` | boolean | 是否含有配方函数 |
| `hasRecipeAction` | boolean | 是否含有配方事件 |
| `resourceDomain` | string | 添加该配方的 mod 的 modid |
| `fullResourceDomain` | string | 完整的 resourceDomain |
| `name` | string | 配方名称 |
| `commandString` | string | 配方的命令字符串表示 |

---

## ICraftingInventory

合成过程中工作台容器的信息对象。

导入：`import crafttweaker.recipes.ICraftingInventory`

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 拥有该容器的玩家 |
| `size` | int | 容器大小 |
| `width` | int | 容器宽度 |
| `height` | int | 容器高度 |
| `stackCount` | int | 实际填充的物品槽位数量 |
| `items` | IItemStack[][] | 工作台中的物品（二维） |
| `itemArray` | IItemStack[] | 工作台中的物品（一维） |

### 方法

```zenscript
// 按索引获取物品（返回 IItemStack 或 null）
inventory.getStack(index);       // index: int

// 按索引设置物品（传 null 清空槽位）
inventory.setStack(index, item); // index: int, item: IItemStack

// 按行列获取物品（左上角为 0,0）
inventory.getStack(row, column); // row: int, column: int

// 按行列设置物品（传 null 清空槽位）
inventory.setStack(row, column, item); // row: int, column: int, item: IItemStack
```

---

## ICraftingInfo

合成过程本身的信息对象。

导入：`import crafttweaker.recipes.ICraftingInfo`

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `inventory` | ICraftingInventory | 合成所在的容器 |
| `player` | IPlayer | 执行合成的玩家 |
| `dimensionID` | int | 合成所在维度的 ID |
| `world` | IWorld | 合成所在的世界 |

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

## IFurnaceRecipe

熔炉配方在 ZenScript 中的表示对象。

导入：`import crafttweaker.recipes.IFurnaceRecipe`

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `input` | IIngredient | 输入物品 |
| `output` | IItemStack | 输出物品 |
| `xp` | float | 烧炼经验值 |
| `commandString` | string | 配方的命令字符串表示 |

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
