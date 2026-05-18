# 语言基础

## 尖括号语法

尖括号 `<...>` 是 ZenScript 中最常用的获取游戏对象的方式。

### 物品

```zenscript
<minecraft:apple>                    // 物品
<minecraft:stone:3>                  // 带 Meta 的物品
<minecraft:wool:*>                   // 任意 Meta（通配符）
<minecraft:wool:0>                   // Meta 0
```

### 矿物词典

```zenscript
<ore:ingotIron>                      // 矿辞
<ore:ingotGold>                      // 矿辞
<ore:dirt>                           // 矿辞
```

### 流体

```zenscript
<liquid:water>                       // 流体
<liquid:lava>                        // 流体
<liquid:lava> * 1000                 // 带数量的流体
```

### 实体

```zenscript
<entity:minecraft:sheep>             // 实体定义
<entity:minecraft:creeper>           // 实体定义
```

### 方块

```zenscript
<block:minecraft:stone>              // 方块定义
<block:minecraft:dirt>               // 方块定义
```

### 附魔

```zenscript
<enchantment:fortune>                // 附魔定义
<enchantment:fortune> * 3            // 附魔等级 3
<enchantment:sharpness>              // 附魔定义
```

### 药水效果

```zenscript
<potion:minecraft:speed>             // 药水效果
<potion:minecraft:slowness>          // 药水效果
```

### 伤害来源

```zenscript
<damageSource:MAGIC>                 // 魔法伤害
<damageSource:GENERIC>               // 通用伤害
<damageSource:IN_FIRE>               // 火焰伤害
<damageSource:LAVA>                  // 岩浆伤害
<damageSource:OUT_OF_WORLD>          // 虚空伤害
```

### 生物群系

```zenscript
<biome:minecraft:plains>             // 生物群系
<biome:minecraft:desert>             // 生物群系
```

### 获取对象的其他方式

```zenscript
// 从物品定义获取
<minecraft:wool>.definition.makeStack(3)

// 从矿辞获取
<ore:ingotIron>.items                // 所有物品列表
<ore:ingotIron>.firstItem            // 第一个物品

// 从 mod 获取
loadedMods["minecraft"].items        // mod 所有物品

// 从游戏对象获取
game.getBlock("minecraft:stone")     // 方块
game.getItem("minecraft:apple")      // 物品
game.getEntity("minecraft:sheep")    // 实体定义
game.getPotion("minecraft:speed")    // 药水效果
game.getBiome("minecraft:plains")    // 生物群系
```

---

## 控制流

### if-else

```zenscript
if (condition) { ... }
else if (condition) { ... }
else { ... }
```

### 三元操作符

```zenscript
val result = condition ? valueA : valueB;
```

### for 循环

```zenscript
for i in 0 .. 10 { print(i); }         // 0 到 9
for i in 0 to 10 { print(i); }         // 同上
for item in array { print(item); }      // 遍历数组
for i, item in array { print(i); }      // 带索引遍历
for key in map { print(key); }          // 遍历映射键
for key, val in map { print(key); }     // 遍历映射键值
for entry in map.entrySet { }           // 遍历 Entry
```

### while 循环

```zenscript
var i = 0;
while (i < 10) { i = i + 1; }
```

### break / continue

```zenscript
for i in 0 .. 5 {
    if (i == 3) break;      // 跳出循环
    if (i == 2) continue;   // 跳过本次
    print(i);
}
```

---

## 函数

### 匿名函数

```zenscript
// 基本格式
function(参数列表) {
    return 返回值;
}

// 用于物品条件
<minecraft:iron_pickaxe>.only(function(item) {
    return !isNull(item) && item.damage > 100;
});

// 用于配方函数（第4个参数）
recipes.addShapeless("test", <minecraft:stone>, [<minecraft:dirt>],
    function(output, ins, info) {
        // output: 输出物品
        // ins: 输入物品映射
        // info: IRecipeFunctionInfo（含 player, world 等）
        return info.player.world.dimension == -1 ? output : null;
    },
null);

// 匿名函数内只能读取外部变量，不能重新赋值
// 但可以修改数组/映射的元素
```

### 自定义函数

#### 基本格式

```zenscript
function 函数名(参数表) as 返回类型 {
    // 代码
    return 返回值;
}
```

- 无参数：只写 `()`
- 无返回值：省略 `as 返回类型` 和 `return`
- 单行函数：直接写在 return 行

#### 示例

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

### 全局函数变量

```zenscript
global addition as function(int, int)int = function(a as int, b as int) as int {
    return a + b;
};
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
