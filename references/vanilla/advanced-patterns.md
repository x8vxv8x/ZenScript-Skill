# 高级用法参考

## 自定义函数

### 基本格式

```zenscript
function 函数名(参数表) as 返回类型 {
    // 代码
    return 返回值;
}
```

- 无参数：只写 `()`
- 无返回值：省略 `as 返回类型` 和 `return`
- 单行函数：直接写在 return 行

### 示例

```zenscript
// 获取物品名
function getItemName(input as IItemStack) as string {
    val id = input.definition.id;
    val meta = input.metadata;
    if (meta == 0) {
        return id;
    } else {
        return id ~ ":" ~ meta;
    }
}

// 打包操作（无返回值）
function recipeTweak(isShaped as bool, out as IItemStack, input as IIngredient[][]) {
    recipes.remove(out, true);
    if (isShaped) {
        recipes.addShaped(getItemName(out), out, input);
    } else {
        recipes.addShapeless(getItemName(out), out, input[0]);
    }
}
```

### 全局函数

```zenscript
global addition as function(int, int)int = function(a as int, b as int) as int {
    return a + b;
};
```

---

## 配方函数（Recipe Function）

配方函数是 `recipes.addShaped` / `recipes.addShapeless` 的第 4 个参数，用于动态决定输出。

```zenscript
recipes.addShaped(recipeName, output, inputBox, recipeFunction, recipeAction);
```

### 参数说明

- `out`: IItemStack — 配方定义的输出
- `ins`: 映射 — 包含所有 `.marked()` 标记的输入物品
- `info`: ICraftingInfo — 合成信息（player, inventory 等）

### 返回值

- 返回 IItemStack 作为实际输出
- 返回 null 表示不可合成

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

---

## 配方事件（Recipe Action）

配方事件是第 5 个参数，在合成完成后执行。

### 参数说明

- `out`: IItemStack — 合成结果
- `info`: ICraftingInfo — 合成信息
- `player`: IPlayer — 合成的玩家

### 示例

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

## ZenClass（自定义类）

ZenScript 支持自定义类，本质上是 Java 类。

### 关键字

| 关键字 | 说明 |
|--------|------|
| `zenClass` | 声明类 |
| `zenConstructor` | 构造函数 |
| `val` / `var` | 字段（val 不可变，var 可变） |
| `static` | 静态字段 |
| `function` | 方法 |
| `this` | 当前对象 |

### 示例

```zenscript
zenClass MyClass {
    zenConstructor(arg as string, arg1 as int) {
        myValue = arg;
        myValueTwo = arg1;
    }

    zenConstructor(arg as string) {
        myValue = arg;
        myValueTwo = 25;
    }

    val myValue as string;
    val myValueTwo as int;
    var myValueThree as int;
    static myStaticValue as int = 233;

    function getMyValue() as string {
        return this.myValue;
    }

    function setMyValueThree(arg as int) as MyClass {
        this.myValueThree = arg;
        return this;  // 返回自身支持链式调用
    }
}
```

### 使用

```zenscript
import scripts.Class.MyClass;  // 导入

val obj = MyClass("abc", 1);   // 构造
print(obj.getMyValue());       // 调用方法
print(obj.myValueTwo);         // 访问字段
print(MyClass.myStaticValue);  // 访问静态字段
```

---

## 穷举与遍历

### 遍历所有配方

```zenscript
for recipe in recipes.all {
    if (recipe.ingredients1D has <minecraft:iron_ingot>) {
        recipes.removeByRecipeName(recipe.name);
    }
}
```

### 遍历所有矿辞

```zenscript
import crafttweaker.oredict.IOreDictEntry;

for entry in oreDict.entries {
    var name = entry.name;
    if (name.startsWith("gear")) {
        // 处理齿轮矿辞
    }
}
```

### 遍历所有模组物品

```zenscript
for mod in loadedMods {
    for item in mod.items {
        // 处理每个物品
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
