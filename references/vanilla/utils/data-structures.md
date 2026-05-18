# 数据结构 API

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
