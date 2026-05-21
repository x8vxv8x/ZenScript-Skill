# 世界事件 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 部分事件需要 ZenUtils
> 导入: `import crafttweaker.event.*;` 或 `import mods.zenutils.event.*;`

世界 Tick、实体移除、物品销毁、物品掉落、睡觉、矿车等事件。

---

## API 列表

### Tick 事件

#### WorldTickEvent（世界 Tick 事件）

> `import crafttweaker.event.WorldTickEvent;`

每个世界每 Tick 触发（客户端和服务端都会触发）。

实现接口：ITickEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |
| `phase` | string | Tick 阶段，值为 `START` 或 `END` |
| `side` | string | 执行端，值为 `CLIENT` 或 `SERVER` |

#### ClientTickEvent（客户端 Tick 事件）

> `import crafttweaker.event.ClientTickEvent;`

客户端每 Tick 触发。

实现接口：ITickEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `phase` | string | Tick 阶段，值为 `START` 或 `END` |
| `side` | string | 执行端，值为 `CLIENT` 或 `SERVER` |

#### ServerTickEvent（服务端 Tick 事件）

> `import crafttweaker.event.ServerTickEvent;`

服务端每 Tick 触发。

实现接口：ITickEvent

#### RenderTickEvent（渲染 Tick 事件）

> `import crafttweaker.event.RenderTickEvent;`

客户端渲染 Tick 时触发。

实现接口：ITickEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `renderTickTime` | float | 渲染 Tick 时间（插值值） |
| `phase` | string | Tick 阶段，值为 `START` 或 `END` |
| `side` | string | 执行端，值为 `CLIENT` 或 `SERVER` |

### 矿车事件

#### MinecartCollisionEvent（矿车碰撞事件）

> `import crafttweaker.event.MinecartCollisionEvent;`

矿车与实体碰撞时触发。

实现接口：IMinecartEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `collider` | IEntity | 碰撞的实体 |
| `minecart` | IEntity | 矿车实体 |

#### MinecartInteractEvent（矿车交互事件）

> `import crafttweaker.event.MinecartInteractEvent;`

玩家与矿车交互时触发。可取消以阻止打开容器。

实现接口：IMinecartEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 交互的玩家 |
| `item` | IItemStack | 手持物品 |
| `hand` | string | 使用的手 |
| `minecart` | IEntity | 矿车实体 |

### 睡觉事件

#### SleepingTimeCheckEvent（睡觉时间检查事件）

> `import crafttweaker.event.SleepingTimeCheckEvent;`

检查睡觉中的玩家是否可以继续睡觉时触发。

结果说明：
- **default**：使用原版逻辑（`World.isDaytime`）
- **allow**：强制允许玩家继续睡觉
- **deny**：在此事件中被**忽略**，不起作用

此事件允许你让玩家继续睡觉，但不允许你阻止他们睡觉。

实现接口：IEventPositionable, IPlayerEvent, IEventHasResult

| 属性 | 类型 | 说明 |
|------|------|------|
| `result` | string | 事件结果，值为 `default`、`deny` 或 `allow` |
| `player` | IPlayer | 睡觉的玩家 |

方法：
- `event.deny()` 设置结果为 `deny`
- `event.allow()` 设置结果为 `allow`
- `event.default()` 设置结果为 `default`

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`；继承自 IPlayerEvent 的 `entityLivingBase`。

#### SleepingLocationCheckEvent（睡觉位置检查事件）

> `import crafttweaker.event.SleepingLocationCheckEvent;`

检查睡觉中的玩家是否可以在当前位置继续睡觉时触发。

结果说明：
- **default**：使用原版床方块逻辑
- **allow**：强制允许玩家继续睡觉
- **deny**：在此事件中被**忽略**，不起作用

此事件允许你让玩家继续睡觉，但不允许你绕过默认的床逻辑。

实现接口：IEventPositionable, IPlayerEvent, IEventHasResult

| 属性 | 类型 | 说明 |
|------|------|------|
| `result` | string | 事件结果，值为 `default`、`deny` 或 `allow` |
| `player` | IPlayer | 睡觉的玩家 |

方法：
- `event.deny()` 设置结果为 `deny`
- `event.allow()` 设置结果为 `allow`
- `event.default()` 设置结果为 `default`

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`；继承自 IPlayerEvent 的 `entityLivingBase`。

### ZenUtils 扩展事件（需安装 ZenUtils）

#### EntityRemoveEvent（实体移除事件）

> `import mods.zenutils.event.EntityRemoveEvent;`
> 版本要求: 1.12.2+

当实体被销毁或卸载时触发。不可取消。

实现接口：IEntityEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 实体所在世界 |

#### EntityItemDeathEvent（物品实体销毁事件）

> `import mods.zenutils.event.EntityItemDeathEvent;`
> 版本要求: 1.13.9+

当物品实体被岩浆、火焰、虚空等销毁时触发（不包括漏斗等传输设备）。

实现接口：IEntityEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IEntityItem | 被销毁的物品实体 |
| `damageSource` | IDamageSource | 销毁原因 |

```zenscript
events.onEntityItemDeath(function(event as EntityItemDeathEvent) {
    print("物品 " ~ event.item.name ~ " 被销毁了");
});
```

#### EntityItemFallEvent（物品实体掉落事件）

> `import mods.zenutils.event.EntityItemFallEvent;`
> 版本要求: 1.13.8+

当物品实体掉落时触发。不可取消。

实现接口：IEntityEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IEntityItem | 掉落的物品实体 |
| `distance` | float | 掉落距离 |
| `blockStates` | List\<IBlockState\> | 碰撞的方块状态列表 |

#### WorldEvents（世界事件）

> 版本要求: 1.14.6+

世界加载/保存/卸载事件，可用于保存或读取世界数据。

| 事件 | 导入 | 说明 |
|------|------|------|
| `events.onWorldLoad(handler)` | `mods.zenutils.event.WorldLoadEvent` | 世界加载时触发 |
| `events.onWorldSave(handler)` | `mods.zenutils.event.WorldSaveEvent` | 世界保存时触发 |
| `events.onWorldUnload(handler)` | `mods.zenutils.event.WorldUnloadEvent` | 世界卸载时触发 |

均包含 `world` getter 获取 IWorld 对象。
