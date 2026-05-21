# 语言基础 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: 无需导入

ZenScript 语言基础语法。

---

## 括号处理器列表

### 物品括号处理器（Item）

返回 `IItemStack` 对象。

```zenscript
<minecraft:apple>                    // 苹果
<minecraft:coal:0>                   // 煤炭（meta 0）
<minecraft:coal:1>                   // 木炭（meta 1）
<minecraft:coal:*>                   // 所有 meta 值
<item:minecraft:coal:*>              // 显式指定为物品（可选）
```

- `modid`：物品所属 mod 的 ID
- `itemname`：物品名称（用 `/ct hand` 获取）
- `meta`：meta 值（整数，可选，默认 0，可用 `*` 通配符）

### 方块状态括号处理器（BlockState）

返回 `IBlockState` 对象。

```zenscript
<blockstate:minecraft:dirt>                              // 泥土默认状态
<blockstate:minecraft:log>                               // 原木默认状态
<blockstate:minecraft:log:variant=oak,axis=y>            // 橡木原木，垂直
<blockstate:minecraft:log:variant=spruce,axis=x>         // 云杉原木，水平 X 轴
```

- 用逗号分隔的 `name=value` 对指定方块属性
- 未指定的属性使用默认方块状态的值

### 流体括号处理器（Liquid）

返回 `ILiquidStack` 对象。

```zenscript
<liquid:lava>       // 岩浆
<fluid:lava>        // 同上，fluid 别名
```

### 矿物辞典括号处理器（Ore）

返回 `IOreDictEntry` 对象。如果矿辞不存在，会创建一个新的空矿辞。

```zenscript
<ore:ingotIron>     // 铁锭矿辞
```

### 实体括号处理器（Entity）

返回 `IEntityDefinition` 对象。

```zenscript
<entity:minecraft:sheep>     // 羊
```

### 药水括号处理器（Potion）

返回 `IPotion` 对象。

```zenscript
<potion:minecraft:strength>      // 力量效果
```

### 药水类型括号处理器（PotionType）

返回 `IPotionType` 对象。

```zenscript
<potiontype:minecraft:strength>          // 力量药水
```

### 附魔括号处理器（Enchantment）

返回 `IEnchantmentDefinition` 对象。

```zenscript
<enchantment:minecraft:protection>       // 保护
```

### 伤害来源括号处理器（DamageSource）

返回 `IDamageSource` 对象。如果伤害来源不是预定义的，会创建一个新的。

```zenscript
<damageSource:MAGIC>             // 魔法伤害
<damageSource:GENERIC>           // 通用伤害
<damageSource:IN_FIRE>           // 火焰伤害
<damageSource:LAVA>              // 岩浆伤害
<damageSource:IN_WALL>           // 窒息伤害
<damageSource:STARVE>            // 饥饿伤害
<damageSource:OUT_OF_WORLD>      // 虚空伤害
<damageSource:FALL>              // 摔落伤害
<damageSource:CRAMMING>          // 挤压伤害
<damageSource:DROWN>             // 溺水伤害
<damageSource:LIGHTNING_BOLT>    // 闪电伤害
<damageSource:ON_FIRE>           // 着火伤害
<damageSource:HOT_FLOOR>         // 烫脚伤害
<damageSource:CACTUS>            // 仙人掌伤害
<damageSource:FLY_INTO_WALL>     // 撞墙伤害
<damageSource:WITHER>            // 凋零伤害
<damageSource:ANVIL>             // 铁砧伤害
<damageSource:FALLING_BLOCK>     // 下落方块伤害
<damageSource:DRAGON_BREATH>     // 龙息伤害
<damageSource:FIREWORKS>         // 烟花伤害
```

### 创造标签页括号处理器（CreativeTab）

返回 `ICreativeTab` 对象。

```zenscript
<creativetab:buildingBlocks>  // 建筑方块标签页
```

---

## 变量类型

### 基本类型（无需 import）

| 类型 | 说明 | 示例 |
|------|------|------|
| `int` | 整数 (-2147483648 ~ 2147483647) | `var x as int = 10;` |
| `bool` | 布尔值 | `var b as bool = true;` |
| `long` | 大整数 | `var l as long = 2147483648;` |
| `float` | 单精度浮点 | `var f as float = 1.5;` |
| `double` | 双精度浮点 | `var d as double = 1.2345;` |
| `void` | 空 | `var v as void = null;` |
| `string` | 字符串（支持 Java String 方法） | `var s as string = "hello";` |

### 对象类型（需要 import）

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

### 变量声明

```zenscript
// val: 不可重新赋值
val a as int = 10;

// var: 可重新赋值
var b as int = 10;

// 类型可省略（自动推断）
var c = 10;  // 推断为 int
```

### 类型强制转换

ZenScript 将第二个操作数的类型转换为第一个操作数的类型：

```zenscript
13 % 6.5  // 6.5 转为 int 变成 6，结果为 13 % 6 = 1
```

### 作用域规则

```zenscript
import crafttweaker.item.IItemStack;

global a as int = 450;                        // 全局作用域
static b as int = 100;                        // 全局作用域
val item as IItemStack = <minecraft:apple>;   // 脚本作用域
```

### 基本类型功能

#### 字符串

```zenscript
"Hello".length              // 长度，返回 int
"Hello"[1]                  // 索引字符，返回 string
"Hello" in "Hell"           // 包含检查，返回 bool（也可用 has）
"Hel" ~ "lo"                // 连接（~ 连接字符串）
```

支持所有不使用 `char` 类型的 Java String 方法，如 `toLowerCase`、`toUpperCase`、`trim`、`split`、`isEmpty` 等。

#### 整数

```zenscript
0 to 10        // 返回整数范围（0 到 9）
1 ~ 10         // 连接整数，返回 "110"
```

#### 可变 workaround

全局/静态变量本身不可修改，但可通过数组/映射元素间接修改：

```zenscript
static arr as int[] = [1];
arr[0] = 10;  // 可以修改元素
```
---

## 运算符

### 算术运算符

| 运算符 | 赋值运算符 | 功能 | 示例 |
|--------|-----------|------|------|
| `+` | `+=` | 加法 | `1+2` |
| `-` | `-=` | 减法 | `2-1` |
| `*` | `*=` | 乘法 | `1*1` |
| `/` | `/=` | 除法 | `2/2` |
| `%` | `%=` | 取模 | `13 % 6` |

- `~` 用于字符串拼接：`"Hello" ~ " " ~ "World"`

### 比较与逻辑运算符

| 名称 | 运算符 | 说明 |
|------|--------|------|
| 非 | `!` | 取反布尔值 |
| 等于 | `==` | 相等判断 |
| 不等于 | `!=` | 不等判断 |
| 大于 | `>` | 大于判断 |
| 大于等于 | `>=` | 大于等于判断 |
| 小于 | `<` | 小于判断 |
| 小于等于 | `<=` | 小于等于判断 |
| 逻辑与 | `&&` | 两者为真（短路） |
| 逻辑或 | `\|\|` | 一者为真（短路） |
| 异或 | `^` | 恰好一者为真 |

### `|`/`&` 与 `||`/`&&` 的区别

`||`/`&&` 会短路（第一个条件满足后不再计算后续条件），`|`/`&` 会计算所有条件。短路运算符适合做 null 检查：

```zenscript
var item = ... as IItemStack;
// 安全：短路，item 为 null 时不访问 .amount
if (!isNull(item) && item.amount == 1) { ... }
```

### `in`/`has` 运算符

检查某物是否包含在某集合中。`in` 和 `has` 功能相同，习惯上 `has` 用于集合包含检查，`in` 用于循环。

注意：`A has B` 要求 B 的**所有**匹配物品都在 A 中才为真。

---

### 全局字段

以下字段无需 import 即可直接使用：

| 字段 | 类型 | 说明 |
|------|------|------|
| `recipes` | IRecipeManager | 工作台配方管理 |
| `furnace` | IFurnaceManager | 熔炉配方管理 |
| `brewing` | IBrewingManager | 酿造台管理 |
| `game` | IGame | 游戏相关函数 |
| `server` | IServer | 服务器相关 |
| `client` | IClient | 客户端相关（仅客户端可用） |
| `events` | IEventManager | 事件管理 |
| `format` | IFormatter | 格式化处理 |
| `itemUtils` | IItemUtils | 物品工具 |
| `loadedMods` | ILoadedMods | 已加载 mod 列表 |
| `logger` | ILogger | 日志工具 |
| `oreDict` | IOreDict | 矿物词典管理 |
| `vanilla` | IVanilla | 原版函数（如 seeds） |

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

### 全局函数

无需 import，直接使用。

| 函数 | 返回 | 说明 |
|------|------|------|
| `print(obj)` | void | 打印到 CraftTweaker 日志 |
| `isNull(obj)` | bool | 检查对象是否为 null（不适用于基本类型，可尝试 `as bool`） |
| `instanceof obj Type` | bool | 检查对象是否为指定类型实例 |
| `max(int, int)` | int | 返回较大的 int |
| `min(int, int)` | int | 返回较小的 int |
| `pow(double, double)` | double | 幂运算 |
| `totalActions()` | int | 已注册的全局函数数量 |
| `enableDebug()` | void | 启用调试模式（推荐用 `#debug` 预处理器替代） |

### ZenUtils 全局函数（需安装 ZenUtils）

可直接调用，也可通过 `mods.zenutils.ZenUtils.<方法>` 调用。

| 函数 | 返回 | 说明 |
|------|------|------|
| `typeof(Object)` | String | 获取对象类型名（不能接收原始类型，需用 `mods.zenutils.ZenUtils.typeof`） |
| `toString(Object)` | String | 对象的字符串表示 |
| `addRegexLogFilter(String)` | void | 抑制匹配正则的日志消息 |
| `arrayOf(int, @Optional Object)` | Object[] | 创建对象数组，需 `as` 强转 |
| `intArrayOf(int, @Optional int)` | int[] | 创建 int 数组 |
| `byteArrayOf(int, @Optional byte)` | byte[] | 创建 byte 数组 |
| `shortArrayOf(int, @Optional short)` | short[] | 创建 short 数组 |
| `longArrayOf(int, @Optional long)` | long[] | 创建 long 数组 |
| `floatArrayOf(int, @Optional float)` | float[] | 创建 float 数组 |
| `doubleArrayOf(int, @Optional double)` | double[] | 创建 double 数组 |
| `boolArrayOf(int, @Optional bool)` | bool[] | 创建 bool 数组 |
| `scriptStatus()` | int | 游戏阶段：0=初始化中，1=重载中，2=已启动 |
| `addReloadableLoader(String)` | void | 标记指定 loader 为可重载 |

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
- 无返回值：省略 `as 返回类型` 和 `return`

#### 默认参数

参数可设置默认值，调用时可省略。有默认值的参数之后的参数也必须有默认值。

```zenscript
function name(a as int, b as int = 2, c as int = 3) as void {
    print(a + b + c);
}
```
- 默认值支持括号处理器和函数调用，但不支持变量

### 全局函数变量

```zenscript
global addition as function(int, int)int = function(a as int, b as int) as int {
    return a + b;
};
```
---

## 变量作用域

### global 变量

全局变量，可在脚本中直接使用名称访问。**声明后不可修改，必须在声明时初始化。** 不可在子文件夹中的脚本里声明。

```zenscript
import crafttweaker.item.IItemStack;
global myGlobalValue as IItemStack = <minecraft:dirt>;
```

- 使用 `#priority` 确保声明全局变量的脚本先执行
- 局部变量会遮蔽同名全局变量

### static 变量

脚本绑定变量，需通过跨脚本引用访问。同样不可修改。

```zenscript
static myStaticValue as IItemStack = <minecraft:sand>;
```

---

## 跨脚本引用

声明了 `static` 变量或自定义函数的脚本会注册到跨脚本引用系统。

- 前缀：`scripts.`
- 路径相对于 scripts 目录，用点号分隔（如 `scripts.mySubfolder.a.zs`）
- 可在 import 语句中使用
---

## Import 语法

导入语句必须放在脚本顶部。每个脚本单独声明导入。

### 基本导入

```zenscript
// 导入包
import mods.jei.JEI;
JEI.hide(<minecraft:diamond>);
```

### 别名导入

使用 `as` 为导入指定别名，避免同名冲突或简化调用。

```zenscript
import mods.jei.JEI.hide as h;
h(<minecraft:dirt>);
```
---

## 扩展方法

可为已有类添加新方法。使用 `$expand` 语法，`this` 指向被扩展的实例。

```zenscript
$expand ClassName$MethodName(arguments as ArgType) as ReturnType {
    // 代码
    return VALUE;
}
```

```zenscript
import crafttweaker.item.IItemStack;

$expand IItemStack$show() as void {
    print(this.commandString);
}

$expand string$wrap(prefix as string = "(", suffix as string = ")") as string {
    return prefix ~ this ~ suffix;
}

<minecraft:apple>.show();
print("test".wrap());        // "(test)"
print("test".wrap("[", "]")); // "[test]"
```