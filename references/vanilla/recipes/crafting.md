# 合成配方

## 添加有序合成

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

---

## 添加无序合成

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

---

## 移除配方

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

---

## 查询配方

```zenscript
// 获取所有已注册的工作台配方
var allRecipes = recipes.all;  // 返回 List<ICraftingRecipe>

// 获取包含指定材料的所有配方
var ironRecipes = recipes.getRecipesFor(<minecraft:iron_ingot>);  // 返回 List<ICraftingRecipe>
```

---

## 替换配方材料

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

---

## 模拟合成

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
