# ZenUtils CraftTweaker API 参考

> Mod ID: `zenutils`
> 前置条件: 无
> 导入: `import mods.zenutils.*;`

ZenUtils 是 CraftTweaker 的扩展模组，提供全局函数、类型扩展、自定义命令、Mixin 支持、FTB Quests 事件等内容。部分功能未在文档中记录，建议使用 ProbeZS 发现所有类和方法。

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

## ZenUtilsEntity 扩展（IEntity 扩展）

对 `crafttweaker.entity.IEntity` 的扩展，所有实体对象自动可用。

### ZenGetters

| 属性 | 返回 | 说明 |
|------|------|------|
| `nbt` | IData | 获取实体的完整 NBT 数据 |
| `position` | IBlockPos | 获取实体位置（方块坐标） |
| `world` | IWorld | 获取实体所在世界 |
| `id` | int | 获取实体的实体 ID |
| `uuid` | String | 获取实体 UUID 字符串 |
| `name` | String | 获取实体名称 |
| `eyeHeight` | float | 获取实体眼睛高度 |
| `width` | float | 获取实体宽度 |
| `height` | float | 获取实体高度 |
| `isCreatureType(CreatureType, bool)` | bool | 检查实体是否属于指定生物类型 |

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `setNBT(IData)` | IData | void | 设置实体 NBT 数据 |
| `sendMessage(String)` | String | void | 向实体发送消息（仅玩家有效） |
| `getRelatedEntities()` | 无 | IEntity[] | 获取相关实体列表 |
| `getEntitiesNear(double)` | double（距离） | IEntity[] | 获取附近实体 |
| `teleport(IWorld, double, double, double)` | IWorld, double, double, double | void | 传送实体到指定坐标 |

---

## ZenUtilsPlayer 扩展（IPlayer 扩展）

对 `crafttweaker.player.IPlayer` 的扩展，所有玩家对象自动可用。

### ZenGetters

| 属性 | 返回 | 说明 |
|------|------|------|
| `foodStats` | IFoodStats | 获取食物状态 |
| `inventory` | IInventory | 获取玩家背包 |
| `xpLevel` | int | 获取经验等级 |
| `xp` | float | 获取经验值百分比 |

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `setFoodStats(IFoodStats)` | IFoodStats | void | 设置食物状态 |
| `sendTitle(String, int, int, int)` | String, int, int, int | void | 发送标题消息（标题, 淡入, 持续, 淡出） |
| `setXpLevel(int)` | int | void | 设置经验等级 |

---

## ZenUtilsWorld 扩展（IWorld 扩展）

对 `crafttweaker.world.IWorld` 的扩展，所有世界对象自动可用。

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `getCustomTileEntity(IBlockPos)` | IBlockPos | TileEntityInGame | 获取指定位置的 ZenUtils 自定义方块实体，不存在则返回 null |
| `getLiquidHandler(IBlockPos, @Optional IFacing)` | IBlockPos, IFacing（可选） | LiquidHandler | 获取方块实体的流体处理器 |
| `gameRuleHelper` | 无 | GameRuleHelper | 获取游戏规则管理器 |
| `getGameRuleHelper()` | 无 | GameRuleHelper | 获取游戏规则管理器（方法形式） |

---

## ZenUtilsEntityDefinition 扩展（IEntityDefinition 扩展）

对 `crafttweaker.entity.IEntityDefinition` 的扩展。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `onTick(IEntityTick, @Optional int)` | IEntityTick, int（可选间隔） | void | 为特定实体类型添加周期性 tick 回调。仅服务端执行，无需检查 `world.remote` |

```zenscript
// 每 50 tick 对所有苦力怕执行一次
<entity:minecraft:creeper>.onTick(function(entity) {
    print("creeper? " ~ entity.world.time);
}, 50);
```

---

## ExpandedCommandManager 扩展（ICommandManager 扩展）

> 版本要求: 1.10.0+

对 `crafttweaker.command.ICommandManager` 的扩展。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `executeCommandSilent(ICommandSender, String)` | ICommandSender, String | int | 静默执行命令，不发送反馈消息 |

---

## CrTItemHandler（物品处理器）

> 导入: `import mods.zenutils.ItemHandler;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `world.getItemHandler(IBlockPos, @Optional IFacing)` | IBlockPos, IFacing（可选） | ItemHandler | 获取方块实体的物品容器 |
| `sizeSlots` | 无 | int | 获取槽位数量 |
| `getStackInSlot(int)` | int | IItemStack | 获取指定槽位的物品 |
| `insertItem(int, IItemStack, bool)` | int, IItemStack, bool | IItemStack | 向指定槽位插入物品。第三个参数为 false 时仅模拟 |
| `extractItem(int, int, bool)` | int, int, bool | IItemStack | 从指定槽位提取物品。第三个参数为 false 时仅模拟 |
| `setStackInSlot(int, IItemStack)` | int, IItemStack | void | 直接设置指定槽位的物品 |
| `getSlotLimit(int)` | int | int | 获取指定槽位的最大堆叠数 |

---

## CrTLiquidHandler（流体处理器）

> 导入: `import mods.zenutils.LiquidHandler;`
> 版本要求: 1.9.8+

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `world.getLiquidHandler(IBlockPos, @Optional IFacing)` | IBlockPos, IFacing（可选） | LiquidHandler | 获取方块实体的流体容器 |
| `tankProperties` | 无 | List\<ILiquidTankProperties\> | 获取流体槽信息（只读） |
| `drain(int, bool)` | int（最大量）, bool（是否执行） | ILiquidStack | 排出流体。false 时仅模拟 |
| `drain(ILiquidStack, bool)` | ILiquidStack, bool | ILiquidStack | 排出指定类型流体。false 时仅模拟 |
| `fill(ILiquidStack, bool)` | ILiquidStack, bool | int | 填充流体。返回实际填充量。false 时仅模拟 |

---

## ILiquidTankProperties（流体槽信息）

> 导入: `import mods.zenutils.ILiquidTankProperties;`

| 属性/方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `contents` | 无 | ILiquidStack | 流体槽内容的副本，可能为 null |
| `capacity` | 无 | int | 流体槽最大容量（mB） |
| `canFill` | 无 | bool | 是否可以填充 |
| `canDrain` | 无 | bool | 是否可以排出 |
| `canFillFluidType(ILiquidStack)` | ILiquidStack | bool | 检查是否可以填充指定类型的流体（不考虑当前状态） |
| `canDrainFluidType(ILiquidStack)` | ILiquidStack | bool | 检查是否可以排出指定类型的流体（不考虑当前状态） |

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

## GameRuleHelper（游戏规则）

> 导入: `import mods.zenutils.GameRuleHelper;`

通过 `world.gameRuleHelper` 或 `world.getGameRuleHelper()` 获取。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `addGameRule(String, String, String)` | key, value, type | void | 添加自定义游戏规则。type 必须为 `"Any"`、`"Numeric"` 或 `"Boolean"` |
| `hasRule(String)` | String | bool | 检查规则是否存在 |
| `getRules()` | 无 | String[] | 获取所有规则名 |
| `getBoolean(String)` | String | bool | 获取布尔值规则 |
| `getInt(String)` | String | int | 获取整数规则 |
| `getString(String)` | String | String | 获取字符串规则 |

---

## PlayerStat（玩家统计）

> 导入: `import mods.zenutils.PlayerStat;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `PlayerStat.getStat(String)` | String（stat ID） | PlayerStat | 获取统计对象 |
| `player.addStat(PlayerStat, @Optional int)` | PlayerStat, int（可选，默认1） | void | 增加统计计数 |
| `player.getStatCount(PlayerStat)` | PlayerStat | int | 获取统计计数值 |
| `player.setStatFormatter(PlayerStat, IStatFormatter)` | PlayerStat, IStatFormatter | void | 设置统计显示格式化器 |

### IStatFormatter（统计格式化器）

> 导入: `import mods.zenutils.IStatFormatter;`

函数式接口：接收 `int`，返回 `string`。

| 预置格式化器 | 说明 |
|------|------|
| `IStatFormatter.simple()` | 数字分组显示（默认） |
| `IStatFormatter.time()` | 时间格式显示 |
| `IStatFormatter.distance()` | 距离单位显示 |
| `IStatFormatter.divideByTen()` | 除以十后显示 |

| 工具方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `IStatFormatter.numberFormat(int)` | int | string | 格式化整数（分组分隔符） |
| `IStatFormatter.decimalFormat(double)` | double | string | 格式化小数（保留2位） |

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

---

## 自定义命令系统

### ZenCommand

> 导入: `import mods.zenutils.command.ZenCommand;`

| 方法/属性 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `ZenCommand.create(String)` | String（命令名） | ZenCommand | 创建命令实例 |
| `register()` | 无 | void | 注册命令到游戏（必须调用，否则命令不生效） |
| `name` | 无 | String | 获取命令名 |
| `getCommandUsage` | IGetCommandUsage | - | 设置用法说明（返回未本地化键名） |
| `execute` | ICommandExecute | - | 设置执行逻辑 |
| `requiredPermissionLevel` | int | - | 设置权限等级（默认 4） |
| `tabCompletionGetters` | IGetTabCompletion[] | - | 设置 Tab 补全 |

```zenscript
import mods.zenutils.command.ZenCommand;
import mods.zenutils.command.CommandUtils;

var cmd = ZenCommand.create("hello");
cmd.execute = function(command, server, sender, args) {
    CommandUtils.getCommandSenderAsPlayer(sender).sendMessage("Hello!");
};
cmd.register();
```

### ZenCommandTree

> 导入: `import mods.zenutils.command.ZenCommandTree;`

用于创建带子命令的命令树。具体用法参见 wiki。

### IGetCommandUsage（函数式接口）

> 导入: `import mods.zenutils.command.IGetCommandUsage;`

接收 `ZenUtilsCommandSender`，返回 `string`（未本地化的用法键名）。可通过语言文件或 `game.setLocalization` 本地化。

### ICommandExecute（函数式接口）

> 导入: `import mods.zenutils.command.ICommandExecute;`

| 参数 | 类型 | 说明 |
|------|------|------|
| command | ZenCommand | 正在执行的命令 |
| server | IServer | 执行命令的服务器 |
| sender | ZenUtilsCommandSender | 执行命令的发送者 |
| args | String[] | 命令参数 |

### IGetTabCompletion（函数式接口）

> 导入: `import mods.zenutils.command.IGetTabCompletion;`

| 参数 | 类型 | 说明 |
|------|------|------|
| server | IServer | 服务器 |
| sender | ZenUtilsCommandSender | 命令发送者 |
| pos | IBlockPos | @Nullable 目标位置 |

返回 `StringList`。

| 预置方法 | 返回 | 说明 |
|------|------|------|
| `IGetTabCompletion.empty()` | StringList | 空列表 |
| `IGetTabCompletion.item()` | StringList | 所有物品 |
| `IGetTabCompletion.block()` | StringList | 所有方块 |
| `IGetTabCompletion.player()` | StringList | 所有在线玩家 |
| `IGetTabCompletion.potion()` | StringList | 所有药水 |
| `IGetTabCompletion.x()` | StringList | 目标位置 X 坐标 |
| `IGetTabCompletion.y()` | StringList | 目标位置 Y 坐标 |
| `IGetTabCompletion.z()` | StringList | 目标位置 Z 坐标 |

### CommandUtils（命令工具）

> 导入: `import mods.zenutils.command.CommandUtils;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `getCommandSenderAsPlayer(ZenUtilsCommandSender)` | ZenUtilsCommandSender | IPlayer | 将命令发送者转为玩家 |
| `getPlayer(IServer, ZenUtilsCommandSender, String)` | IServer, ZenUtilsCommandSender, String | IPlayer | 通过目标选择器获取单个玩家 |
| `getPlayers(IServer, ZenUtilsCommandSender, String)` | 同上 | List\<IPlayer\> | 获取多个玩家 |
| `getEntity(IServer, ZenUtilsCommandSender, String)` | 同上 | IEntity | 获取单个实体 |
| `getEntityList(IServer, ZenUtilsCommandSender, String)` | 同上 | List\<IEntity\> | 获取多个实体 |
| `getItemByText(ZenUtilsCommandSender, String)` | ZenUtilsCommandSender, String | IItemDefinition | 通过文本 ID 查找物品定义 |
| `getBlockByText(ZenUtilsCommandSender, String)` | ZenUtilsCommandSender, String | IBlockDefinition | 通过文本 ID 查找方块定义 |
| `notifyWrongUsage(String)` | String | void | 抛出用法错误（停止命令执行） |
| `notifyWrongUsage(String, String...)` | String, String... | void | 抛出带替换值的用法错误 |
| `notifyWrongUsage(ZenCommand, ZenUtilsCommandSender)` | ZenCommand, ZenUtilsCommandSender | void | 使用命令定义的用法信息抛出错误 |

### ZenUtilsCommandSender

> 导入: `import mods.zenutils.command.ZenUtilsCommandSender;`

继承 `ICommandSender`，所有 `ICommandSender` 方法可用。**禁止 instanceof 或强转为 ICommandSender 子类**，始终返回 false 或抛出 ClassCastException。使用 `CommandUtils.getCommandSenderAsPlayer` 获取玩家。

---

## 事件系统

### EntityRemoveEvent

> 导入: `import mods.zenutils.event.EntityRemoveEvent;`

当实体从世界中移除时触发。

### EntityItemDeathEvent

> 导入: `import mods.zenutils.event.EntityItemDeathEvent;`
> 版本要求: 1.13.9+

当物品实体被岩浆、火焰、虚空等销毁时触发（不包括漏斗等传输设备）。

| 属性 | 返回 | 说明 |
|------|------|------|
| `item` | IEntityItem | 被销毁的物品实体 |
| `damageSource` | IDamageSource | 销毁原因 |

```zenscript
events.onEntityItemDeath(function(event as EntityItemDeathEvent) {
    print("物品 " ~ event.item.name ~ " 被销毁了");
});
```

### EntityItemFallEvent

当物品实体掉落时触发。具体属性参见 wiki。

### WorldEvents

世界相关事件。具体事件列表参见 wiki。

### GenericEventManager

通用事件管理器，支持注册自定义事件。具体用法参见 wiki。

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

---

## ContentTweaker 扩展

### ExpandVanillaFactory（工厂方法扩展）

对 `VanillaFactory` 的扩展。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `VanillaFactory.createEnergyItem(String, int, int, int)` | unlocalizedName, capacity, maxReceive, maxExtract | EnergyItem | 创建能量物品 |
| `VanillaFactory.createExpandBlock(String, IBlockMaterialDefinition)` | unlocalizedName, blockMaterial | ExpandBlock | 创建扩展方块 |
| `VanillaFactory.createExpandItem(String)` | unlocalizedName | ExpandItem | 创建扩展物品 |
| `VanillaFactory.createActualTileEntity(int)` | id | TileEntity | 创建自定义方块实体 |

### ExpandItem（扩展物品）

> 导入: `import mods.zenutils.cotx.Item;`

继承 ContentTweaker 的 `ItemRepresentation`。

| 属性 | 类型 | 默认值 | 说明 |
|------|------|------|------|
| `onEntityItemUpdate` | IEntityItemUpdate | null | 物品实体更新回调。返回 true 跳过后续更新 |
| `noRepair` | bool | false | 是否不可修复 |
| `getEntityLifeSpan` | IGetEntityLifeSpan | null | 掉落物存活时间回调。返回 tick 数（默认 6000） |

#### IEntityItemUpdate（函数式接口）

> 导入: `import mods.zenutils.cotx.IEntityItemUpdate;`

参数：`IEntityItem`。返回 `bool`（true=跳过后续更新）。

#### IGetEntityLifeSpan（函数式接口）

> 导入: `import mods.zenutils.cotx.IGetEntityLifeSpan;`

参数：`IItemStack`, `IWorld`。返回 `int`（tick 数，默认 6000）。

### ExpandBlock（扩展方块）

> 导入: `import mods.zenutils.cotx.Block;`

继承 ContentTweaker 的 `BlockRepresentation`。

| 属性 | 类型 | 默认值 | 说明 |
|------|------|------|------|
| `onBlockActivated` | IBlockActivated | null | 方块右键交互回调 |
| `onEntityWalk` | IEntityWalk | null | 实体踩踏回调 |
| `onEntityCollidedWithBlock` | IEntityCollided | null | 实体碰撞回调 |
| `tileEntity` | TileEntity | null | 关联的方块实体 |

#### IBlockActivated（函数式接口）

> 导入: `import mods.zenutils.cotx.IBlockActivated;`

| 参数 | 类型 |
|------|------|
| world | IWorld |
| pos | IBlockPos |
| state | ICTBlockState |
| player | ICTPlayer |
| hand | Hand |
| facing | Facing |
| blockHit | Position3f |

返回 `bool`。

#### IEntityWalk（函数式接口）

> 导入: `import mods.zenutils.cotx.IEntityWalk;`

参数：`IWorld`, `IBlockPos`, `IEntity`。返回 void。

#### IEntityCollided（函数式接口）

> 导入: `import mods.zenutils.cotx.IEntityCollided;`

参数：`IWorld`, `IBlockPos`, `ICTBlockState`, `IEntity`。返回 void。

### EnergyItem（能量物品）

> 导入: `import mods.zenutils.cotx.EnergyItem;`

继承 `ExpandItem`，无额外 ZenProperties。通过 `VanillaFactory.createEnergyItem` 创建。

### TileEntity（方块实体定义）

> 导入: `import mods.zenutils.cotx.TileEntity;`

用于定义自定义方块实体的行为。通过 `VanillaFactory.createActualTileEntity` 创建。

### TileEntityInGame（方块实体实例）

> 导入: `import mods.zenutils.cotx.TileEntityInGame;`
> 版本要求: 1.4.0+

表示游戏中的自定义方块实体实例。通过 `world.getCustomTileEntity(IBlockPos)` 获取。

| 属性 | 类型 | 读/写 | 说明 |
|------|------|------|------|
| `id` | int | 读 | 方块实体 ID |
| `data` | IData | 读/写 | 自定义数据 |

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `updateCustomData(IData)` | IData | void | 更新自定义数据 |

### LateSetCoTFunction（延迟设置函数）

> 版本要求: 1.8.0+

允许在 CraftTweaker 脚本中设置 ContentTweaker 物品/方块的函数（支持脚本重载）。

#### Bracket Handlers

| Bracket | 返回 | 说明 |
|------|------|------|
| `<cotItem:name>` | IItemRepresentation | 获取 ContentTweaker 物品 |
| `<cotBlock:name>` | IBlockRepresentation | 获取 ContentTweaker 方块 |

#### 可设置属性

| 属性 | 回调签名 | 说明 |
|------|------|------|
| `IItemRepresentation.onItemUse` | (player, world, pos, hand, facing, blockHit) → ActionResult | 物品使用回调 |

#### 静态方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `VanillaFactory.putTileEntityTickFunction(int, ITileEntityTick)` | id, tickFunction | void | 注册方块实体 tick 函数（可重载） |

```zenscript
#loader crafttweaker reloadable
import mods.zenutils.cotx.LateSetCoTFunction;

<cotItem:test_item>.onItemUse = function(player, world, pos, hand, facing, blockHit) {
    // 自定义物品使用逻辑
    return ActionResult.success();
};
```

---

## FTB Quests 事件集成

### FTBQEventManager

通过全局 `events` 对象访问。

| 方法 | 事件类型 | 说明 |
|------|------|------|
| `events.onTaskCompleted(handler)` | TaskCompletedEvent | 任务完成事件 |
| `events.onQuestCompleted(handler)` | QuestCompletedEvent | 任务线完成事件 |
| `events.onChapterCompleted(handler)` | ChapterCompletedEvent | 章节完成事件 |
| `events.onTaskStarted(handler)` | TaskStartedEvent | 任务开始事件 |
| `events.onCustomReward(handler)` | CustomRewardEvent | 自定义奖励事件 |
| `events.onCustomTask(handler)` | CustomTaskEvent | 自定义任务事件 |
| `events.clearFTBQEvents()` | - | 清除所有 FTB Quests 事件监听器 |

### QuestObjectBase（基础对象）

> 导入: `import mods.zenutils.ftbq.QuestObjectBase;`

所有 FTB Quests 对象的基类。

| 属性 | 返回 | 说明 |
|------|------|------|
| `id` | int | 唯一标识符 |
| `parentID` | int | 父对象 ID |
| `title` | String | 标题 |
| `data` | IData | NBT 数据 |
| `icon` | IItemStack | 图标物品 |
| `codeString` | String | 字符串表示 |
| `type` | String | 对象类型 |
| `tags` | String[] | 标签数组 |
| `hasTag(String)` | bool | 检查是否包含指定标签 |

支持 `==` 运算符。

### Chapter（章节）

> 导入: `import mods.zenutils.ftbq.Chapter;`

继承 `QuestObjectBase`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `quests` | List\<Quest\> | 章节中的所有任务线 |

### Quest（任务线）

> 导入: `import mods.zenutils.ftbq.Quest;`

继承 `QuestObjectBase`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `canRepeat` | bool | 是否可重复 |
| `chapter` | Chapter | 所属章节 |
| `x` | double | GUI 地图 X 位置 |
| `y` | double | GUI 地图 Y 位置 |
| `width` | double | 节点宽度 |
| `height` | double | 节点高度 |
| `tasks` | List\<Task\> | 所有任务 |
| `rewards` | List\<Reward\> | 所有奖励 |
| `dependencies` | List\<QuestObjectBase\> | 依赖的任务对象 |
| `subtitle` | String | 副标题 |
| `shape` | String | 节点形状 |
| `disableJEI` | bool | 是否禁用 JEI 集成 |

### Task（任务）

> 导入: `import mods.zenutils.ftbq.Task;`

继承 `QuestObjectBase`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `quest` | Quest | 所属任务线 |

### Reward（奖励）

> 导入: `import mods.zenutils.ftbq.Reward;`

继承 `QuestObjectBase`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `quest` | Quest | 所属任务线 |

### ObjectCompletedEvent（完成事件基类）

> 导入: `import mods.zenutils.ftbq.ObjectCompletedEvent;`

| 属性 | 返回 | 说明 |
|------|------|------|
| `onlineMembers` | List\<IPlayer\> | 在线成员 |
| `notifyPlayers` | List\<IPlayer\> | 被通知的玩家 |

### QuestCompletedEvent

> 导入: `import mods.zenutils.ftbq.QuestCompletedEvent;`

继承 `ObjectCompletedEvent`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `quest` | Quest | 完成的任务线 |

### ChapterCompletedEvent

> 导入: `import mods.zenutils.ftbq.ChapterCompletedEvent;`

继承 `ObjectCompletedEvent`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `chapter` | Chapter | 完成的章节 |

### TaskCompletedEvent

> 导入: `import mods.zenutils.ftbq.TaskCompletedEvent;`

继承 `ObjectCompletedEvent`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `task` | Task | 完成的任务 |

### TaskStartedEvent

> 导入: `import mods.zenutils.ftbq.TaskStartedEvent;`

| 属性 | 返回 | 说明 |
|------|------|------|
| `task` | Task | 开始的任务 |

### CustomRewardEvent

> 导入: `import mods.zenutils.ftbq.CustomRewardEvent;`

继承 `IEventCancelable`（可取消）。

| 属性 | 返回 | 说明 |
|------|------|------|
| `player` | IPlayer | 相关玩家 |
| `notify` | bool | 是否通知玩家 |
| `reward` | Reward | 奖励对象 |

### CustomTaskEvent

> 导入: `import mods.zenutils.ftbq.CustomTaskEvent;`

继承 `IEventCancelable`（可取消）。具体属性参见 wiki。

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

### 自定义命令

```zenscript
import mods.zenutils.command.ZenCommand;
import mods.zenutils.command.CommandUtils;
import mods.zenutils.command.IGetTabCompletion;

var cmd = ZenCommand.create("greet");
cmd.requiredPermissionLevel = 0; // 无需权限
cmd.getCommandUsage = function(sender) {
    return "/greet <player>";
};
cmd.execute = function(command, server, sender, args) {
    var player = CommandUtils.getPlayer(server, sender, args[0]);
    player.sendMessage("你好, " ~ player.name ~ "!");
};
cmd.tabCompletionGetters = [IGetTabCompletion.player()];
cmd.register();
```

### FTB Quests 事件

```zenscript
events.onQuestCompleted(function(event as QuestCompletedEvent) {
    var quest = event.quest;
    for player in event.notifyPlayers {
        player.sendMessage("完成任务: " ~ quest.title);
    }
});

events.onCustomReward(function(event as CustomRewardEvent) {
    event.player.sendMessage("获得自定义奖励!");
});
```

### 实体 Tick 回调

```zenscript
// 所有僵尸每 20 tick 执行一次
<entity:minecraft:zombie>.onTick(function(entity) {
    if (entity.world.time % 100 == 0) {
        entity.world.broadcast("僵尸在活动!");
    }
}, 20);
```

### 游戏规则

```zenscript
var gr = world.gameRuleHelper;
gr.addGameRule("doDaylightCycle", "true", "Boolean");
if (gr.hasRule("doDaylightCycle")) {
    print("日夜循环: " ~ gr.getBoolean("doDaylightCycle"));
}
```

---

## 注意事项

- 部分功能未在官方文档中记录，建议使用 ProbeZS 模组发现所有可用类和方法
- `arrayOf` 返回 `Object[]`，需要使用 `as` 关键字强转为目标类型
- Mixin 脚本中只能使用原生类型，不能使用 CraftTweaker 注册的类型
- Mixin 脚本不可重载（使用 `#loader mixin` 时）
- `ZenUtilsCommandSender` 禁止 instanceof 或强转为 ICommandSender 子类
- 使用 `#loader crafttweaker reloadable` 配合 `#reloadable` 预处理器可实现脚本热重载
- ContentTweaker 物品/方块仍需在 ContentTweaker 脚本中注册后才能使用 `LateSetCoTFunction`
- 安装 ZenRecipeReload 模组可获得配方重载支持
