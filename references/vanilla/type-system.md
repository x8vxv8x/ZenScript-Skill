# 类型系统参考

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

## IData 类型

> `import crafttweaker.data.IData;`

IData 是数据接口，用于操作 NBT 等数据。

### 基本类型转 IData

```zenscript
val data = "hello" as IData;
val num = 42 as IData;
val list = [1, 2, 3] as IData;
```

### 子类

| 子类 | 支持的操作 |
|------|-----------|
| DataBool | `&` `\|` `^` `in` `==` |
| DataInt/Long/Short/Byte | 所有算术和比较运算符 |
| DataFloat/Double | 所有算术和比较运算符 |
| DataString | `+` `\|` `^` `in` `==` |
| DataMap | `+` `-` `\|` `^`，支持 `.member` 访问 |
| DataList | `+` `\|` `^`，支持 `[i]` 索引 |

### 类型转换

```zenscript
data.asInt();
data.asLong();
data.asDouble();
data.asFloat();
data.asBool();
data.asString();
data.asList();
data.asMap();
```

### 通用属性

- `.length` — 长度（标量返回 0）
- `.immutable` — 是否不可变
- `.update(value)` — 更新值

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
