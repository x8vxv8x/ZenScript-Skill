# 玩家物品事件 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.event.*;`

玩家合成、熔炼、拾取物品等相关事件。

---

## API 列表

### PlayerCraftedEvent（玩家合成事件）

> `import crafttweaker.event.PlayerCraftedEvent;`

玩家取出合成结果时触发（不是在网格中放入物品时）。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `output` | IItemStack | 合成结果 |
| `inventory` | ICraftingInventory | 合成网格 |
| `player` | IPlayer | 合成的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerSmeltedEvent（玩家熔炼事件）

> `import crafttweaker.event.PlayerSmeltedEvent;`

玩家从熔炉取出物品时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `output` | IItemStack | 熔炼结果 |
| `player` | IPlayer | 取出物品的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerItemPickupEvent（玩家拾取物品事件）

> `import crafttweaker.event.PlayerItemPickupEvent;`

玩家与物品实体交互并拾取物品后触发。在 `PlayerPickupItemEvent` 之后触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `stackCopy` | IItemStack | 被拾取的物品副本（已放入背包的部分） |
| `originalEntity` | IEntityItem | 原始物品实体（可能包含剩余数量） |
| `player` | IPlayer | 拾取物品的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerPickupItemEvent（玩家拾取物品实体事件）

> `import crafttweaker.event.PlayerPickupItemEvent;`

玩家与物品实体交互时触发。

实现接口：IPlayerEvent, IEventHasResult, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IEntityItem | 物品实体 |
| `player` | IPlayer | 拾取的玩家 |

方法：
- `event.deny()` 设置结果为 `deny`
- `event.allow()` 设置结果为 `allow`
- `event.default()` 设置结果为 `default`

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerPickupEntityEvent（玩家拾取实体事件）

> `import crafttweaker.event.PlayerPickupEvent;`

玩家与实体交互时触发。

| 属性 | 类型 | 说明 |
|------|------|------|
| `canceled` | bool | 是否已取消 |
| `processed` | bool | 是否已处理 |
| `player` | IPlayer | 拾取的玩家 |
| `entity` | IEntity | 被拾取的实体 |

方法：
- `event.cancel()` 取消事件
- `event.process()` 将事件标记为已处理

### PlayerPickupXpEvent（玩家拾取经验事件）

> `import crafttweaker.event.PlayerPickupXpEvent;`

玩家拾取经验球时触发。可取消。

实现接口：IEventCancelable, IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `entityXp` | IEntityXp | 经验球实体 |
| `xp` | float | 经验值 |
| `player` | IPlayer | 拾取经验的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。
