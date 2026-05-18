# 其他事件

## 箭矢事件

### ArrowLooseEvent

> `import crafttweaker.event.ArrowLooseEvent;`

玩家松开弓弦（射箭）时触发。可取消。

实现接口：IPlayerEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `bow` | IItemStack | 弓 |
| `charge` | int | 蓄力值（可设置） |
| `world` | IWorld | 世界对象 |
| `player` | IPlayer | 射箭的玩家 |

### ArrowNockEvent

> `import crafttweaker.event.ArrowNockEvent;`

玩家开始拉弓（搭箭）时触发。

实现接口：IPlayerEvent, IEventHasResult

| 属性 | 类型 | 说明 |
|------|------|------|
| `bow` | IItemStack | 弓 |
| `hand` | string | 使用的手 |
| `player` | IPlayer | 玩家 |
| `result` | string | 事件结果 |

方法：
- `event.deny()` / `event.allow()` / `event.default()`

---

## 附魔事件

### EnchantmentLevelSetEvent

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

---

## 命令事件

### CommandEvent

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

---

## 暴击事件

### CriticalHitEvent

> `import crafttweaker.event.CriticalHitEvent;`

玩家攻击时暴击判定触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `target` | IEntity | 攻击目标 |
| `oldDamageModifier` | float | 原始伤害倍率 |
| `damageModifier` | float | 伤害倍率（可设置） |
| `isVanillaCrit` | boolean | 是否原版暴击 |
| `player` | IPlayer | 攻击的玩家 |

方法：
- `event.deny()` 阻止暴击
- `event.allow()` 强制暴击
- `event.default()` 使用原版行为

---

## 爆炸事件

### ExplosionStartEvent

> `import crafttweaker.event.ExplosionStartEvent;`

爆炸即将开始时触发。可取消以阻止爆炸。

实现接口：IExplosionEvent, IEventCancelable

继承自 IExplosionEvent 的 `world`、`explosion`、`position`、`x`、`y`、`z`。

### ExplosionDetonateEvent

> `import crafttweaker.event.ExplosionDetonateEvent;`

爆炸引爆时触发。不可取消。

实现接口：IExplosionEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `affectedEntities` | IEntity[] | 受影响的实体列表 |
| `affectedPositions` | IBlockPos[] | 受影响的位置列表 |

继承自 IExplosionEvent 的 `world`、`explosion`、`position`、`x`、`y`、`z`。

---

## Tick 事件

### WorldTickEvent

> `import crafttweaker.event.WorldTickEvent;`

每个世界每 Tick 触发（客户端和服务端都会触发）。

实现接口：ITickEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |
| `phase` | string | Tick 阶段，值为 `START` 或 `END` |
| `side` | string | 执行端，值为 `CLIENT` 或 `SERVER` |

### ClientTickEvent

> `import crafttweaker.event.ClientTickEvent;`

客户端每 Tick 触发。

实现接口：ITickEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `phase` | string | Tick 阶段，值为 `START` 或 `END` |
| `side` | string | 执行端，值为 `CLIENT` 或 `SERVER` |

### ServerTickEvent

> `import crafttweaker.event.ServerTickEvent;`

服务端每 Tick 触发。

实现接口：ITickEvent

### RenderTickEvent

> `import crafttweaker.event.RenderTickEvent;`

渲染 Tick 时触发。

实现接口：ITickEvent

---

## 物品事件

### ItemExpireEvent

> `import crafttweaker.event.ItemExpireEvent;`

物品实体达到最大寿命时触发。可取消以阻止物品消失，取消后会将 `extraLife` 添加到物品寿命中。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IEntityItem | 物品实体 |
| `extraLife` | int | 额外寿命（可设置） |

继承自 IEntityEvent 的 `entity`。

### ItemFishedEvent

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

### ItemTossEvent

> `import crafttweaker.event.ItemTossEvent;`

玩家从背包丢弃物品时触发。取消后物品不会进入世界（物品会被删除）。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IEntityItem | 物品实体 |
| `player` | IPlayer | 丢弃物品的玩家 |

继承自 IEntityEvent 的 `entity`。

---

## 使用物品事件

### EntityLivingUseItemEvent（系列事件）

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

---

## 药水酿造事件

### PotionBrewPreEvent

> `import crafttweaker.event.PotionBrewPreEvent;`

药水酿造前触发。

### PotionBrewPostEvent

> `import crafttweaker.event.PotionBrewPostEvent;`

药水酿造后触发。

---

## 投射物命中事件

### ProjectileImpactArrowEvent

> `import crafttweaker.event.ProjectileImpactArrowEvent;`

箭矢命中时触发。

### ProjectileImpactFireballEvent

> `import crafttweaker.event.ProjectileImpactFireballEvent;`

火球命中时触发。

### ProjectileImpactThrowableEvent

> `import crafttweaker.event.ProjectileImpactThrowableEvent;`

投掷物（如雪球、末影珍珠）命中时触发。

---

## 矿车事件

### MinecartCollisionEvent

> `import crafttweaker.event.MinecartCollisionEvent;`

矿车碰撞时触发。

### MinecartInteractEvent

> `import crafttweaker.event.MinecartInteractEvent;`

玩家与矿车交互时触发。

---

## 睡觉事件

### SleepingTimeCheckEvent

> `import crafttweaker.event.SleepingTimeCheckEvent;`

睡觉时间检查时触发。

### SleepingLocationCheckEvent

> `import crafttweaker.event.SleepingLocationCheckEvent;`

睡觉位置检查时触发。

---

## 其他事件

### AnimalTameEvent

> `import crafttweaker.event.AnimalTameEvent;`

动物即将被驯服时触发。可取消以阻止驯服。

实现接口：IPlayerEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `animal` | IEntityAnimal | 被驯服的动物 |
| `player` | IPlayer | 驯服的玩家 |

### MobGriefingEvent

> `import crafttweaker.event.MobGriefingEvent;`

生物破坏方块（如苦力怕爆炸、末影人搬方块等）时触发。

### LootingLevelEvent

> `import crafttweaker.event.LootingLevelEvent;`

抢夺等级判定时触发。

---

## ZenUtils 扩展（需安装 ZenUtils）

> `import mods.zenutils.event.*;`

### EntityRemoveEvent

> `import mods.zenutils.event.EntityRemoveEvent;`

当实体从世界中移除时触发。

### EntityItemDeathEvent

> `import mods.zenutils.event.EntityItemDeathEvent;`
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
