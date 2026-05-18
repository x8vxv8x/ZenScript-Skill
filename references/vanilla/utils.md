# Utils API

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

## 常见错误及原因

### 编译时错误

| 错误信息 | 原因 | 修复 |
|---------|------|------|
| `unexpected end of file - ; expected` | 缺少分号 | 补上 `;` |
| `No such member: xxx` | import 路径错误 | 检查 import 拼写 |
| `could not find type XXX` | 忘记 import | 在文件顶部添加 import |
| `import must be at top` | import 不在文件开头 | 移到最顶部 |
| `No such member in IItemStack: xxx` | 方法不存在 | **查阅 API 文档，不要自造方法** |
| `Could not resolve <xxx:yyy>` | 物品 ID 错误 | 用 `/ct hand` 获取正确 ID |
| `value cannot be changed` | 对 val 重新赋值 | 改用 var |
| `not a valid lvalue` | 对函数参数赋值 | 创建新变量接收 |
| `2 methods available but none matches` | 参数类型错误 | 检查输入类型（输出必须 IItemStack） |

### 运行时错误

| 错误信息 | 原因 | 修复 |
|---------|------|------|
| `NumberFormatException` | 用 `+` 连接字符串和数字 | 改用 `~` |
| `ArrayIndexOutOfBoundsException` | 数组越界 | 检查循环范围 |
| `NullPointerException` | 空指针 | 用 `isNull()` 检查 |

### Null 安全模式

```zenscript
// 错误：直接访问可能为 null 的对象
var offItem as IItemStack = player.offHandHeldItem;
if (offItem.definition.id == "minecraft:sand") { ... }  // NPE!

// 正确：先检查 null
if (!isNull(offItem) && offItem.definition.id == "minecraft:sand") { ... }

// && 短路：第一个为 false 时第二个不会执行
```
