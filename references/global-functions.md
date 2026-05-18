# 全局函数与工具 API

## 全局函数

无需 import，直接使用。

### print

```zenscript
print("Hello World!");
```

将字符串打印到 CraftTweaker 日志。无返回值。

### isNull

```zenscript
isNull(<minecraft:dirt>);
```

检查给定对象是否为 null。返回 bool。不适用于基本类型。

注意：如果不起作用，尝试将对象转换为 bool：`<minecraft:dirt> as bool`

### instanceof

```zenscript
entity instanceof IEntity;
```

检查对象是否为指定类型的实例。返回 bool。

### max

```zenscript
max(10, 11);  // 返回 11
```

返回两个 int 中较大的数。

### min

```zenscript
min(10, 11);  // 返回 10
```

返回两个 int 中较小的数。

### pow

```zenscript
pow(2.0, 4.0);  // 返回 16.0
```

计算幂运算。返回 double。

### totalActions

```zenscript
totalActions();
```

返回已注册的全局函数数量。返回 int。

### enableDebug

```zenscript
enableDebug();
```

启用调试模式。推荐使用 Debug 预处理器替代。

---

## 全局字段

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
