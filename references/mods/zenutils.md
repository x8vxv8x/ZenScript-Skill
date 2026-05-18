# ZenUtils CraftTweaker API 参考

> Mod ID: `zenutils`
> 前置条件: 无
> 导入: `import mods.zenutils.*;`

ZenUtils 是 CraftTweaker 的扩展模组，提供全局函数、Mixin 支持、链式操作、工具类等内容。

> 注意：ZenUtils 对原版类型的扩展已归入 `references/vanilla/` 对应文件：
> - IEntity/IEntityDefinition → `entities.md`
> - IPlayer/PlayerStat → `players.md`
> - IWorld/GameRuleHelper → `world.md`
> - ICommandManager/自定义命令 → `commands.md`
> - 事件系统 → `events.md`
> - 物品处理器 → `container.md`
> - 流体处理器 → `liquids.md`
>
> 对 ContentTweaker 的扩展 → `references/mods/contenttweaker.md`
> FTB Quests 事件集成 → `references/mods/ftbquests.md`

---

## 全局函数

以下函数可直接在 ZenScript 中调用，也可通过 `mods.zenutils.ZenUtils.<方法>` 调用。

| 函数 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `typeof(Object)` | Object | String | 获取对象类型名。不能接收原始类型（int、double 等），需用 `mods.zenutils.ZenUtils.typeof` |
| `toString(Object)` | Object | String | 返回对象的字符串表示 |
| `addRegexLogFilter(String)` | String（正则） | void | 抑制所有匹配正则的日志消息，不会被记录也不会发送给玩家 |
| `arrayOf(int, @Optional Object)` | int, Object（可选） | Object[] | 创建指定长度的对象数组，可选填充元素。结果需要 `as` 强转，如 `as IItemStack[]` |
| `intArrayOf(int, @Optional int)` | int, int（可选） | int[] | 创建 int 数组 |
| `byteArrayOf(int, @Optional byte)` | int, byte（可选） | byte[] | 创建 byte 数组 |
| `shortArrayOf(int, @Optional short)` | int, short（可选） | short[] | 创建 short 数组 |
| `longArrayOf(int, @Optional long)` | int, long（可选） | long[] | 创建 long 数组 |
| `floatArrayOf(int, @Optional float)` | int, float（可选） | float[] | 创建 float 数组 |
| `doubleArrayOf(int, @Optional double)` | int, double（可选） | double[] | 创建 double 数组 |
| `boolArrayOf(int, @Optional bool)` | int, bool（可选） | bool[] | 创建 bool 数组 |
| `scriptStatus()` | 无 | int | 返回当前游戏阶段：0=初始化中，1=重载脚本中，2=游戏已启动 |
| `addReloadableLoader(String)` | String（loader名） | void | 将使用指定 loader 的脚本标记为可重载 |

---

## Catenation（链式操作）

> 导入: `import mods.zenutils.Catenation;`

Catenation 提供延迟执行和链式操作机制，通过 `game.catenation()` 创建。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `game.catenation()` | 无 | Catenation | 创建新的链式操作 |
| `action(function)` | 函数 | Catenation | 添加执行动作 |
| `delay(int)` | int（tick数） | Catenation | 延迟指定 tick |
| `repeat(int)` | int（次数） | Catenation | 重复执行指定次数 |
| `then(function)` | 函数 | Catenation | 链式执行下一个动作 |
| `start()` | 无 | void | 启动链式操作 |
| `stop()` | 无 | void | 停止链式操作 |

---

## 模板字符串

> 版本要求: 1.18.0+

使用反引号 `` ` `` 定义模板字符串，支持 `${expression}` 嵌入表达式。

```zenscript
val name as string = "world";
print(`hello, ${name}!`);

// 动态矿辞查询
function getIngot(type as string) as IItemStack {
    return <ore:ingot${type}>.firstItem;
}

// 动态元数据物品
for i in 0 .. 16 {
    print(<item:minecraft:wool:${i}>.displayName);
}
```

---

## HexHelper（十六进制工具）

> 导入: `import mods.zenutils.HexHelper;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `HexHelper.toHexString(int)` | int | String | 十进制转十六进制字符串 |
| `HexHelper.toDecInteger(String)` | String | int | 十六进制字符串转十进制 |

```zenscript
HexHelper.toDecInteger("ABCDEF"); // 返回 11259375
HexHelper.toHexString(114514);    // 返回 "1bf52"
```

---

## CrTI18n（国际化）

> 导入: `import mods.zenutils.I18n;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `I18n.hasKey(String)` | String | bool | 检查翻译键是否存在 |
| `I18n.format(String)` | String | String | 根据翻译键获取本地化文本（等同于 `game.localize`） |
| `I18n.format(String, Object...)` | String, Object... | String | 翻译并格式化（等同于 `String.format(translate(key), args)`） |

---

## CrTUUID（UUID 工具）

> 导入: `import mods.zenutils.UUID;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `UUID.randomUUID()` | 无 | CrTUUID | 创建随机 UUID |
| `UUID.fromString(String)` | String | CrTUUID | 从字符串解析 UUID |
| `entity.getUUIDObject()` | 无 | CrTUUID | 获取实体的 UUID 对象（实体扩展方法） |
| `getMostSignificantBits()` | 无 | long | 获取高 64 位 |
| `getLeastSignificantBits()` | 无 | long | 获取低 64 位 |
| `asString()` | 无 | String | 转为字符串 |

支持 `==`、`>`、`<` 等比较运算符。

---

## StaticString（静态字符串）

> 导入: `import mods.zenutils.StaticString;`

暴露 Java 的静态字符串方法和 Apache Commons StringUtils 方法。

| 方法 | 说明 |
|------|------|
| `StaticString.valueOf(Object)` | Java `String.valueOf` |
| `StaticString.format(String, Object...)` | Java `String.format` |
| 其他方法 | Apache Commons StringUtils 的大部分方法，详见 [Javadoc](https://commons.apache.org/proper/commons-lang/apidocs/org/apache/commons/lang3/StringUtils.html) |

---

## StringList（字符串列表）

> 导入: `import mods.zenutils.StringList;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `StringList.create(String[])` | String[] | StringList | 创建字符串列表 |

> 自定义命令系统已移至 `references/vanilla/commands.md`。
> 事件系统扩展已移至 `references/vanilla/events.md`。

---

## Mixin 支持

> 导入: `import mixin.*;`

ZenUtils 支持通过 ZenScript 编写 Mixin，实现 Java 字节码级别的类修改。

### 可用类型

| 类型 | 说明 |
|------|------|
| `CallbackInfo` | 回调信息，用于 Inject 钩子 |
| `CallbackInfoReturnable` | 带返回值的回调信息。`getReturnValue()` 返回 `java.lang.Object`，需要强转 |
| `Operation` | 用于 WrapOperation 钩子。`call` 方法接受 `Object...` 并返回 `Object` |

### 内置变量

| 变量 | 说明 |
|------|------|
| `this0` | 目标类实例的引用（当只有一个目标类时）。可访问私有和受保护成员，不处理静态成员 |

### 预处理器指令

| 指令 | 说明 |
|------|------|
| `#loader mixin` | 加载为 mixin loader（脚本不可重载） |
| `#mixin NAME` | Mixin 注解头（如 `Mixin`、`ModifyConstant`、`Shadow`、`Static`） |
| `#mixin` (v1.21.2+) | 当注解为 `Mixin` 时的简写 |
| `#{...}` | JSON 注解体，每行需以 `#` 开头 |
| `#sideonly client` | 仅客户端加载 |
| `#mixin Static` | 标记为静态方法 |
| `#mixin Shadow` | Shadow 目标类字段 |
| `#mixin Local` | 本地变量捕获注解。支持 `parameter`、`ordinal`、`index`、`name`、`ref` 参数 |
| `#mixin Share` | 共享本地变量注解 |
| `#mixin Cancellable` | 可取消钩子注解 |

参数索引约定：`0`=第一个，`1`=第二个，`-1`=最后一个，`-2`=倒数第二个。

无注解的函数会被直接注入到目标类中，可添加新方法或暴露私有成员。

**限制：** Mixin 脚本中只能使用原生类型（因为 mixin 脚本在 CraftTweaker 注册类型之前加载）。SRG 名称必须用于注入点，MCP 名称不可在注解中使用但可在函数体中使用。

> FTB Quests 事件集成已移至 `references/mods/ftbquests.md`。

---

## 预处理器

### #suppress

> 版本要求: 1.5.0+

| 指令 | 说明 |
|------|------|
| `#suppress warning` / `#suppress warnings` | 抑制当前脚本的警告 |
| `#suppress error` / `#suppress errors` / `#suppress all` | 抑制当前脚本的警告和错误 |

解析错误仍会显示，错误仍会记录到 `crafttweaker.log`。使用后 `#ikwid` 和 `#nowarn` 失效。

### #hardfail

> 版本要求: 1.6.6+

| 指令 | 说明 |
|------|------|
| `#hardfail` | 脚本产生未被 `#suppress` 抑制的错误时使游戏崩溃 |

---

## 使用示例

### 基础用法

```zenscript
#loader crafttweaker
import mods.zenutils.HexHelper;
import mods.zenutils.I18n;
import mods.zenutils.UUID;

// 十六进制转换
print(HexHelper.toHexString(255)); // "ff"

// 国际化
print(I18n.format("item.apple.name")); // 获取苹果的本地化名称

// UUID
var uuid = UUID.randomUUID();
print(uuid.asString());
```

---

## 注意事项

- 部分功能未在官方文档中记录，建议使用 ProbeZS 模组发现所有可用类和方法
- `arrayOf` 返回 `Object[]`，需要使用 `as` 关键字强转为目标类型
- Mixin 脚本中只能使用原生类型，不能使用 CraftTweaker 注册的类型
- Mixin 脚本不可重载（使用 `#loader mixin` 时）
- 使用 `#loader crafttweaker reloadable` 配合 `#reloadable` 预处理器可实现脚本热重载
- ContentTweaker 物品/方块仍需在 ContentTweaker 脚本中注册后才能使用 `LateSetCoTFunction`
- 安装 ZenRecipeReload 模组可获得配方重载支持
