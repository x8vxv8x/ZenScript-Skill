# 配方系统完整参考

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

// 移除特定有序配方（inputBox 可省略表示匹配所有）
recipes.removeShaped(<minecraft:stick> * 4, [
    [<ore:plankWood>],
    [<ore:plankWood>]
]);

// 移除特定无序配方
recipes.removeShapeless(<minecraft:book>, [
    <minecraft:paper>, <minecraft:paper>, <minecraft:paper>, <minecraft:leather>
]);

// 按配方 ID 移除
recipes.removeByRecipeName("minecraft:golden_chestplate");

// 按正则匹配移除
recipes.removeByRegex("minecraft:.*_sword");

// 移除某 mod 所有配方
recipes.removeByMod("botania");

// 移除所有配方
recipes.removeAll();
```

---

## 熔炉配方

```zenscript
// 添加：输出, 输入, 经验值（float，可省略）
furnace.addRecipe(<minecraft:iron_ingot>, <minecraft:iron_ore>, 0.7);

// 移除：输出, 输入（输入可省略，移除所有产出该物品的配方）
furnace.remove(<minecraft:iron_ingot>);
furnace.remove(<minecraft:iron_ingot>, <minecraft:iron_ore>);

// 设置燃料：物品, 燃烧时间（ticks）。煤炭=1600，烧一个物品=200
furnace.setFuel(<minecraft:coal>, 1600);
furnace.setFuel(<minecraft:coal>, 0);  // 移除燃料
```

---

## 矿物词典（Ore Dictionary）

```zenscript
// 添加物品到矿辞（不存在则创建）
<ore:ingotCopper>.add(<thermalfoundation:material:128>);

// 从矿辞移除
<ore:sand>.remove(<minecraft:sand>);

// 将一个矿辞的所有物品加入另一个
<ore:ingotMyMetal>.addAll(<ore:ingotIron>);

// 映射：A 的物品全部加入 B，但 B 的不加入 A
<ore:ingotA>.mirror(<ore:ingotB>);
```

---

## 物品条件（Item Conditions）

附加到物品上，用于配方的特殊需求。

> **注意：** 使用耐久相关条件时，先加 meta 通配符禁用默认精确耐久匹配：
> `<minecraft:iron_pickaxe:*>.onlyDamaged()`

| 条件 | 说明 |
|------|------|
| `.anyDamage()` | 耐久值不影响合成 |
| `.onlyDamaged()` | 只有有损耗的物品才能参与 |
| `.onlyDamageAtLeast(int)` | 耐久不小于指定值 |
| `.onlyDamageAtMost(int)` | 耐久不大于指定值 |
| `.onlyDamageBetween(int, int)` | 耐久在两者之间 |
| `.withTag(IData)` | 需要带有指定 NBT |
| `.onlyWithTag(IData)` | 需要**只**带有指定 NBT |
| `.withDamage(int)` | 输出带有指定耐久 |
| `.only(function)` | 自定义条件函数 |

```zenscript
// 有损耗的铁镐才能参与合成
<minecraft:iron_pickaxe:*>.onlyDamaged().withTag({display: {Lore: ["损坏的铁镐"]}});

// 自定义条件：只在下界生效
recipes.addShapeless("nether_recipe", <minecraft:netherrack>,
    [<ore:cobblestone>, <ore:cobblestone>, <ore:cobblestone>],
    function(output, ins, info) {
        return info.player.world.dimension == -1 ? output : null;
    },
null);
```

---

## 物品转换器（Item Transformers）

用于合成后物品不消耗、转换为其他物品等场景。

| 转换器 | 说明 |
|--------|------|
| `.reuse()` | 物品不消耗，留在工作台 |
| `.giveBack()` | 物品不消耗，回到物品栏 |
| `.transformReplace(IItemStack)` | 合成后变为指定物品 |
| `.transformDamage()` | 合成后掉 1 点耐久 |
| `.transformDamage(int)` | 合成后掉指定点耐久 |
| `.noReturn()` | 强制消耗（即使有容器物品） |
| `.transformConsume(int)` | 消耗指定个数 |
| `.transformNew(function)` | 自定义转换函数 |

```zenscript
// 石斧 + 木板 = 3 木棍，石斧掉 1 耐久
recipes.addShapeless(<minecraft:stick> * 3, [
    <minecraft:stone_axe>.transformDamage(), <ore:plankWood>
]);

// 牛奶桶合成蛋糕后变空桶（自动，无需手动转换）
// 如需阻止返回空桶：用 .noReturn()
```

---

## 草丛掉落

```zenscript
// 添加打草掉落（百分比权重）
vanilla.seeds.addSeed(<minecraft:carrot> % 1);  // 1% 几率

// 移除打草掉落
vanilla.seeds.removeSeed(<minecraft:wheat_seeds>);
```

---

## 生物掉落

```zenscript
val sheep = <entity:minecraft:sheep>;

// 添加掉落：物品, 最小数量, 最大数量, 几率
sheep.addDrop(<minecraft:apple>);
sheep.addDrop(<minecraft:stone> % 20);  // 权重 20

// 仅玩家击杀掉落
sheep.addPlayerOnlyDrop(<minecraft:gold_ingot>, 10, 64);
sheep.addPlayerOnlyDrop(<minecraft:iron_ingot> % 20, 1, 3);

// 移除掉落
sheep.removeDrop(<minecraft:wool>);

// 清除所有掉落
sheep.clearDrops();
```
