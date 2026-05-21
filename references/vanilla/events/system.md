# 系统事件 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 部分事件需要 ZenUtils
> 导入: `import crafttweaker.event.*;` 或 `import mods.zenutils.*;`

命令、物品、附魔、酿造、通用事件管理器等系统事件。

---

## API 列表

### 命令事件

#### CommandEvent（命令执行事件）

> `import crafttweaker.event.CommandEvent;`

命令执行时触发。可取消。

实现接口：IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `commandSender` | ICommandSender | 命令发送者 |
| `command` | ICommand | 命令对象 |
| `parameters` | string[] | 命令参数（可设置） |

```zenscript
events.onCommand(function(event as CommandEvent) {
    if (event.command.name == "gamemode" && (event.parameters in "creative")) {
        event.cancel();
    }
});
```

### 附魔事件

#### EnchantmentLevelSetEvent（附魔台等级生成事件）

> `import crafttweaker.event.EnchantmentLevelSetEvent;`

附魔台生成三个附魔等级时触发。

实现接口：IEventPositionable

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |
| `enchantRow` | int | 附魔台行号（1-3） |
| `power` | int | 书架总能量 |
| `item` | IItemStack | 被附魔的物品 |
| `originalLevel` | int | 原始附魔等级 |
| `level` | int | 附魔等级（可设置，0-30） |

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`。

### 物品事件

#### ItemExpireEvent（物品过期事件）

> `import crafttweaker.event.ItemExpireEvent;`

物品实体达到最大寿命时触发。可取消以阻止物品消失，取消后会将 `extraLife` 添加到物品寿命中。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IEntityItem | 物品实体 |
| `extraLife` | int | 额外寿命（可设置） |

继承自 IEntityEvent 的 `entity`。

#### ItemFishedEvent（钓鱼事件）

> `import crafttweaker.event.ItemFishedEvent;`

玩家即将钓到物品时触发。取消后玩家不会收到物品，但鱼竿仍会消耗耐久。

实现接口：IPlayerEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `damage` | int | 鱼竿伤害 |
| `additionalDamage` | int | 额外鱼竿伤害（可设置） |
| `drops` | IItemStack[] | 将钓到的物品列表（不可修改） |
| `fishHook` | IEntityFishHook | 鱼钩实体 |
| `player` | IPlayer | 钓鱼的玩家 |

#### ItemTossEvent（丢弃物品事件）

> `import crafttweaker.event.ItemTossEvent;`

玩家从背包丢弃物品时触发。取消后物品不会进入世界（物品会被删除）。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IEntityItem | 物品实体 |
| `player` | IPlayer | 丢弃物品的玩家 |

继承自 IEntityEvent 的 `entity`。

### 使用物品事件

#### EntityLivingUseItemEvent（实体使用物品事件系列）

> `import crafttweaker.event.EntityLivingUseItemEvent.All;`
> `import crafttweaker.event.EntityLivingUseItemEvent.Start;`
> `import crafttweaker.event.EntityLivingUseItemEvent.Tick;`
> `import crafttweaker.event.EntityLivingUseItemEvent.Stop;`
> `import crafttweaker.event.EntityLivingUseItemEvent.Finish;`

实体使用物品时触发。分为 5 个子事件（All 包含所有阶段，其他 4 个为特定阶段）。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 使用物品的玩家（如果玩家） |
| `isPlayer` | bool | 是否为玩家 |
| `item` | IItemStack | 被使用的物品 |
| `duration` | int | 使用持续时间（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

### 药水酿造事件

#### PotionBrewPreEvent（药水酿造前事件）

> `import crafttweaker.event.PotionBrewPreEvent;`

药水酿造前触发。可取消以阻止酿造。取消后若修改了物品，则会自动触发 `PotionBrewPostEvent`，可用于模拟自定义酿造。

实现接口：IPotionBrewEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `length` | int | 酿造台中的物品数量 |

方法：
- `event.getItem(int index)` 获取酿造台中指定索引的物品（IItemStack），索引超出 `length` 时返回空 IItemStack
- `event.setItem(int index, IItemStack item)` 替换酿造台中指定索引的物品，索引超出 `length` 时无效

#### PotionBrewPostEvent（药水酿造后事件）

> `import crafttweaker.event.PotionBrewPostEvent;`

药水酿造后立即触发，此时输出物品已被替换。若 `PotionBrewPreEvent` 被取消但物品被修改，此事件仍会触发。若 Pre 事件被取消且未修改物品，则此事件**不会**触发。

实现接口：IPotionBrewEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `length` | int | 酿造台中的物品数量 |

方法：
- `event.getItem(int index)` 获取酿造台中指定索引的物品（IItemStack）
- `event.setItem(int index, IItemStack item)` 替换酿造台中指定索引的物品

### 其他事件

#### AnimalTameEvent（动物驯服事件）

> `import crafttweaker.event.AnimalTameEvent;`

动物即将被驯服时触发。可取消以阻止驯服。

实现接口：IPlayerEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `animal` | IEntityAnimal | 被驯服的动物 |
| `player` | IPlayer | 驯服的玩家 |

#### MobGriefingEvent（生物破坏事件）

> `import crafttweaker.event.MobGriefingEvent;`

生物破坏方块（如苦力怕爆炸、末影人搬方块等）时触发。

实现接口：ILivingEvent, IEventHasResult

| 属性 | 类型 | 说明 |
|------|------|------|
| `result` | string | 事件结果，值为 `default`、`deny` 或 `allow` |

方法：
- `event.deny()` 阻止破坏
- `event.allow()` 允许破坏
- `event.default()` 使用原版逻辑

继承自 ILivingEvent 的 `entityLivingBase`。

#### LootingLevelEvent（抢夺等级事件）

> `import crafttweaker.event.LootingLevelEvent;`

生物被杀死时计算抢夺等级触发。可增加、减少或保持抢夺等级。

实现接口：ILivingEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `lootingLevel` | int | 抢夺等级（可设置） |
| `damageSource` | IDamageSource | 伤害来源 |

继承自 ILivingEvent 的 `entityLivingBase`。

### ZenUtils 通用事件管理器（需安装 ZenUtils）

> `import mods.zenutils.EventPriority;`
> 版本要求: 1.16.0+

扩展事件管理器，支持为几乎所有事件（包括 Forge 原生和模组事件）注册处理器，并可设置事件优先级和是否接收已取消事件。

#### 注册方法

| 方法 | 说明 |
|------|------|
| `events.register(handler, @Optional priority, @Optional receiveCanceled, @Optional busID)` | 注册通用事件处理器 |

- `handler`：事件处理函数
- `priority`：事件优先级（默认 `EventPriority.normal()`）
- `receiveCanceled`：是否接收已取消事件（默认 false）
- `busID`：事件总线 ID（0=主总线，1=地形生成总线，2=矿石生成总线）

#### EventPriority

> `import mods.zenutils.EventPriority;`

| 方法 | 说明 |
|------|------|
| `EventPriority.highest()` | 最高优先级 |
| `EventPriority.high()` | 高优先级 |
| `EventPriority.normal()` | 普通优先级（默认） |
| `EventPriority.low()` | 低优先级 |
| `EventPriority.lowest()` | 最低优先级 |
