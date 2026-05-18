# Variable Types API

## 基本类型（无需 import）

| 类型 | 说明 | 示例 |
|------|------|------|
| `int` | 整数 (-2147483648 ~ 2147483647) | `var x as int = 10;` |
| `bool` | 布尔值 | `var b as bool = true;` |
| `long` | 大整数 | `var l as long = 2147483648;` |
| `float` | 单精度浮点 | `var f as float = 1.5;` |
| `double` | 双精度浮点 | `var d as double = 1.2345;` |
| `void` | 空 | `var v as void = null;` |
| `string` | 字符串（支持 Java String 方法） | `var s as string = "hello";` |

## 对象类型（需要 import）

| 类型 | 导入路径 | 说明 |
|------|---------|------|
| IItemStack | `crafttweaker.item.IItemStack` | 一个物品 |
| IIngredient | `crafttweaker.item.IIngredient` | 一个或多个物品（接口） |
| IOreDictEntry | `crafttweaker.oredict.IOreDictEntry` | 矿辞 |
| ILiquidStack | `crafttweaker.liquid.ILiquidStack` | 流体 |
| IItemDefinition | `crafttweaker.item.IItemDefinition` | 物品定义 |
| IBlockDefinition | `crafttweaker.block.IBlockDefinition` | 方块定义 |
| IData | `crafttweaker.data.IData` | 数据接口 |
| IEnchantment | `crafttweaker.enchantments.IEnchantment` | 附魔 |
| IEntity | `crafttweaker.entity.IEntity` | 实体 |
| IPlayer | `crafttweaker.player.IPlayer` | 玩家 |
| IWorld | `crafttweaker.world.IWorld` | 世界 |
| IBlock | `crafttweaker.block.IBlock` | 方块 |
| IBlockState | `crafttweaker.block.IBlockState` | 方块状态 |

## 变量声明

```zenscript
// val: 不可重新赋值
val a as int = 10;
// a = 20;  // 错误！

// var: 可重新赋值
var b as int = 10;
b = 20;  // 正确

// 类型可省略（自动推断）
var c = 10;  // 推断为 int
```

## 全局和静态变量

```zenscript
import crafttweaker.item.IItemStack;

// 全局变量：所有脚本可直接访问
global stone as IItemStack = <minecraft:stone>;

// 静态变量：需要通过脚本路径访问
static dirt as IItemStack = <minecraft:dirt>;

// 需要 #priority 确保定义脚本先加载
#priority 100
```

- 全局/静态变量声明时**必须**带 `as 类型`
- 局部变量会遮蔽全局变量
- 可变 workaround：定义数组/映射，修改其元素

```zenscript
static arr as int[] = [1];
arr[0] = 10;  // 可以修改元素！
```

## 跨脚本引用

```zenscript
// a.zs
static myVal as string = "hello";
function makeLine() { print("---"); }

// b.zs
print(scripts.a.myVal);      // 通过脚本路径
scripts.a.makeLine();

// 或用 import
import scripts.a;
print(a.myVal);
a.makeLine();
```

- 必须以 `scripts.` 开头
- 匹配相对路径
- 不能跨 loader 引用

## 类型强制转换

ZenScript 将第二个操作数的类型转换为第一个操作数的类型：

```zenscript
13 % 6.5  // 6.5 转为 int 变成 6，结果为 13 % 6 = 1
```

**字符串连接用 `~` 不是 `+`：**

```zenscript
"hello" ~ " world";  // 正确："hello world"
// "hello" + 123;     // 可能报错
```

## 数组

```zenscript
var arr as int[] = [10, 20, 30];
arr[0];           // 访问
arr[1] = 25;      // 修改
arr += 40;        // 追加
arr.length;       // 长度
```

## 映射（关联数组）

```zenscript
var map as string[int] = {1: "一", 2: "二", 3: "三"};
map[1];           // 访问："一"
map[4] = "四";    // 添加
map[1] = "one";   // 修改

// 字符串键可用点号
var items as IItemStack[string] = {
    gold: <minecraft:gold_ingot>,
    iron: <minecraft:iron_ingot>
};
items.gold;       // 等同于 items["gold"]

// 遍历
for key in map { }                    // 键
for key, value in map { }             // 键值
for entry in map.entrySet { }         // Entry

// 属性
map.keys / map.keySet;     // 键集合
map.values / map.valueSet; // 值集合
map.entrySet;              // Entry 集合
```

## 作用域规则

```zenscript
import crafttweaker.item.IItemStack;

global a as int = 450;                        // 全局作用域
static b as int = 100;                        // 全局作用域
val item as IItemStack = <minecraft:apple>;   // 脚本作用域

for i in 0 .. 10 {                            // i = 参数作用域
    val j as int = i * 5;                     // j = 局部作用域
    // val i as int = 233;  // 错误：i 已在参数作用域
    // val item = ...;      // 错误：item 已在脚本作用域
    if (i < 4) {
        val k as int = i + 1;                 // k = if 块内局部
        print(k);
    }
    // print(k);  // 错误：k 不在此作用域
}
// print(i);  // 错误：i 只在 for 循环内
```

## 基本变量功能

### 字符串

```zenscript
"Hello".length              // 长度，返回 int
"Hello"[1]                  // 索引字符，返回 string
"Hello" in "Hell"           // 包含检查，返回 bool（也可用 has）
"Hel" ~ "lo " + "World"    // 连接（~ 和 + 都可以）
string += "assignAdd"       // 赋值连接
```

支持所有不使用 `char` 类型的 Java String 方法，如 `toLowerCase`、`toUpperCase`、`trim`、`split`、`isEmpty` 等。

### 整数

```zenscript
+-*/%          // 基本数学运算
0 to 10        // 返回整数范围（0 到 9）
1 ~ 10         // 连接整数，返回 "110"
```

### 布尔值

```zenscript
true ~ false   // 连接，返回 "truefalse"
& | ^          // 与/或/异或
```

### 数组

```zenscript
array[1]       // 访问元素
array[1] = "Hello"  // 设置元素
array.length   // 长度
```

## 运算符

| 运算符 | 赋值 | 用途 |
|--------|------|------|
| `+` | `+=` | 加 |
| `-` | `-=` | 减 |
| `*` | `*=` | 乘 |
| `/` | `/=` | 除 |
| `%` | `%=` | 取余 |
| `~` | `~=` | 连接字符串 |
| `&&` | `&=` | 逻辑与 |
| `\|\|` | `\|=` | 逻辑或 |
| `^` | `^=` | 异或 |
| `!` | | 逻辑非 |
| `==` | | 等于 |
| `!=` | | 不等于 |
| `<` `<=` `>` `>=` | | 比较 |

**`in` / `has` 操作符：**

```zenscript
// 检查 A 是否包含 B（in 和 has 等价）
if (loadedMods has "thermalfoundation") { ... }
if (<ore:ingotIron> has <minecraft:iron_ingot>) { ... }
```

## IIngredient

> `import crafttweaker.item.IIngredient;`

IIngredient 是配方的原料接口，可以是 IItemStack、IOreDictEntry、ILiquidStack 等。

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `commandString` | string | 在 ZS 中的调用字符串 |
| `mark` | string | 标记名称 |
| `amount` | int | 数量 |
| `items` | List\<IItemStack\> | 所有可能的物品列表 |
| `itemArray` | IItemStack[] | 所有可能的物品数组 |
| `liquids` | List\<ILiquidStack\> | 所有可能的流体列表 |

### 标记

```zenscript
val markedPick = <minecraft:diamond_pickaxe>.marked("Picky");
print(markedPick.mark);  // "Picky"
```

### 数量

```zenscript
val multipleApples = <minecraft:apple> * 3;
print(multipleApples.amount);  // 3
```

### OR 操作

```zenscript
val either = <minecraft:apple> | <minecraft:carrot>;
val either2 = <minecraft:apple>.or(<minecraft:carrot>);
```

### 变换器（Transformer）

```zenscript
item.reuse();              // 不消耗，留在合成格
item.giveBack();           // 不消耗，返还整个堆叠
item.giveBack(<minecraft:potato>);  // 消耗，返还指定物品
item.transformReplace(<minecraft:potato>);  // 替换为指定物品
item.transformDamage();    // 损耗 1 耐久
item.transformDamage(3);   // 损耗指定耐久
item.noReturn();           // 强制消耗
item.transformConsume(3);  // 消耗多个
```

### 条件

```zenscript
item.onlyDamaged();                    // 仅接受有损伤的
item.onlyDamageAtLeast(10);            // 最少 10 点损伤
item.onlyDamageAtMost(100);            // 最多 100 点损伤
item.onlyDamageBetween(10, 100);       // 损伤在 10-100 之间
item.onlyWithTag({display: {Name: "Tomato"}});  // 仅接受指定 NBT（JEI 不显示）
item.withTag({display: {Name: "Tomato"}});      // 仅接受指定 NBT（JEI 显示）
item.onlyStack(32);                    // 仅接受至少 32 个的堆叠
```

### 匹配

```zenscript
<ore:ingotIron>.matches(<minecraft:iron_ingot>);      // true
<ore:ingotIron>.matchesExact(<minecraft:iron_ingot>);  // 精确匹配

// IIngredient 间匹配
val ingots = <minecraft:iron_ingot> | <minecraft:gold_ingot>;
ingots has <minecraft:gold_ingot>;  // true
```

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

## 匿名函数

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
