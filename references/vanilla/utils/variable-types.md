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