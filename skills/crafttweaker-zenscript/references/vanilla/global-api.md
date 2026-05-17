# 全局 API 参考

## 全局函数

无需 import，直接使用。

| 函数 | 签名 | 说明 |
|------|------|------|
| `print` | `print(string)` | 输出到 crafttweaker.log |
| `isNull` | `isNull(Object)` | 检测是否为 null（对基本类型无效） |
| `pow` | `pow(double, double)` | 幂运算，返回 double |
| `min` | `min(int, int)` | 取较小值 |
| `max` | `max(int, int)` | 取较大值 |
| `totalActions` | `totalActions()` | 已注册的全局函数数量 |
| `enableDebug` | `enableDebug()` | 开启调试模式 |
| `instanceof` | `obj instanceof Type` | 类型检查 |

```zenscript
print("Hello World!");
if (!isNull(<minecraft:dirt>)) { ... }
pow(2.0, 4.0);  // 16.0
min(10, 11);     // 10
max(10, 11);     // 11
```

## 全局字段

无需 import，直接使用的全局对象。

| 字段 | 类型 | 说明 |
|------|------|------|
| `recipes` | IRecipeManager | 工作台配方管理 |
| `furnace` | IFurnaceManager | 熔炉配方管理 |
| `brewing` | IBrewingManager | 酿造台管理 |
| `game` | IGame | 游戏相关函数 |
| `server` | IServer | 服务器相关 |
| `client` | IClient | 客户端相关 |
| `events` | IEventManager | 事件管理 |
| `format` | IFormatter | 格式化处理 |
| `itemUtils` | IItemUtils | 物品工具 |
| `loadedMods` | ILoadedMods | 已加载 mod 列表 |
| `logger` | ILogger | 日志工具 |
| `oreDict` | IOreDict | 矿物词典管理 |
| `vanilla` | IVanilla | 原版函数（如 seeds） |

---

## Math 包

> `import crafttweaker.util.Math;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `Math.max` | 2个 double/float/int/long | 同类型 | 最大值 |
| `Math.min` | 2个 double/float/int/long | 同类型 | 最小值 |
| `Math.floor` | double | int | 向下取整 |
| `Math.ceil` | double | int | 向上取整 |
| `Math.round` | double | int | 四舍五入 |
| `Math.abs` | double/float/int/long | 同类型 | 绝对值 |
| `Math.sqrt` | double | double | 开方 |
| `Math.log` | double | double | 自然对数 |
| `Math.log10` | double | double | 常用对数 |
| `Math.sin` | double | double | 正弦（弧度） |
| `Math.cos` | double | double | 余弦（弧度） |
| `Math.tan` | double | double | 正切（弧度） |
| `Math.asin` | double | double | 反正弦 |
| `Math.acos` | double | double | 反余弦 |
| `Math.atan` | double | double | 反正切 |
| `Math.sinh` | double | double | 双曲正弦 |
| `Math.cosh` | double | double | 双曲余弦 |
| `Math.tanh` | double | double | 双曲正切 |
| `Math.clamp` | 3个同类型 | 同类型 | 区间限制 clamp(x, min, max) |

```zenscript
import crafttweaker.util.Math;
Math.clamp(15, 10, 19);  // 15
Math.clamp(10, 12, 19);  // 12
Math.floor(3.7);          // 3
Math.ceil(3.2);           // 4
```

---

## Format 格式化

`format` 全局字段提供文本格式化方法，支持 `§` 颜色代码。

### 颜色

| 方法 | 颜色 |
|------|------|
| `format.black()` | 黑色 |
| `format.darkBlue()` | 深蓝 |
| `format.darkGreen()` | 深绿 |
| `format.darkAqua()` | 深青 |
| `format.darkRed()` | 深红 |
| `format.darkPurple()` | 紫色 |
| `format.gold()` | 金色 |
| `format.gray()` | 灰色 |
| `format.darkGray()` | 深灰 |
| `format.blue()` | 蓝色 |
| `format.green()` | 绿色 |
| `format.aqua()` | 青色 |
| `format.red()` | 红色 |
| `format.lightPurple()` | 粉红 |
| `format.yellow()` | 黄色 |
| `format.white()` | 白色 |

### 样式

| 方法 | 效果 |
|------|------|
| `format.obfuscated()` | 乱码 |
| `format.bold()` | 粗体 |
| `format.strikethrough()` | 删除线 |
| `format.underline()` | 下划线 |
| `format.italic()` | 斜体 |

```zenscript
<minecraft:stick>.addTooltip(format.green("这不是绳子"));
<minecraft:stick>.addTooltip(format.green(format.italic("绿色斜体")));
<minecraft:stick>.addTooltip(format.red(format.bold("红色粗体")) ~ " 普通文本");
```

---

## Game 函数

```zenscript
// 设置本地化（语言文件覆盖）
game.setLocalization("zh_cn", "tile.chest.name", "箱子");
game.setLocalization("tile.chest.name", "Box");  // 省略语言代码

// 获取所有物品
for item in game.items { ... }
```

---

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

## 预处理器

必须放在脚本最顶部（import 之前）。

| 预处理器 | 说明 |
|---------|------|
| `#priority <数字>` | 加载优先级（越大越先加载） |
| `#modloaded <modID>` | mod 加载时才执行（支持 `!` 取反） |
| `#loader <loaderName>` | 指定加载器（默认 `crafttweaker`） |
| `#sideonly <side>` | 只在 client 或 server 执行 |
| `#debug` | 输出编译的 class 文件 |
| `#ignoreBracketErrors` | 忽略尖括号错误 |
| `#norun` | 不执行脚本（仍检查语法） |
| `#ikwid` | 警告和错误只写日志 |
| `#profile` | 日志打印配方修改耗时 |
| `#disable_search_tree` | 禁用配方表重算（加速加载） |

```zenscript
#priority 100
#modloaded thermalfoundation
#modloaded !ic2
import crafttweaker.item.IItemStack;
// ...
```

---

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
