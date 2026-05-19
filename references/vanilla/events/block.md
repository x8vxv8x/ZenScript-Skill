# 方块事件 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.event.*;`

方块相关事件，用于监听方块破坏、放置、生长等行为。

---

## API 列表

### BlockBreakEvent（方块破坏事件）

> `import crafttweaker.event.BlockBreakEvent;`

方块被破坏时触发。可取消以阻止方块被破坏。

实现接口：IEventCancelable, IBlockEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 破坏方块的玩家 |
| `isPlayer` | bool | 是否为玩家破坏 |
| `experience` | int | 掉落的经验值（可设置） |
| `result` | string | 事件结果，值为 `default`、`deny` 或 `allow` |

继承自 IBlockEvent 的 `world`、`blockState`、`block`、`position`、`x`、`y`、`z`。

方法：
- `event.deny()` 设置结果为 `deny`
- `event.allow()` 设置结果为 `allow`
- `event.default()` 设置结果为 `default`

### BlockHarvestDropsEvent（方块掉落事件）

> `import crafttweaker.event.BlockHarvestDropsEvent;`

方块即将掉落物品时触发。可修改掉落列表和整体掉率。

实现接口：IBlockEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 挖掘方块的玩家 |
| `isPlayer` | bool | 是否为玩家挖掘 |
| `silkTouch` | bool | 是否精准采集 |
| `fortuneLevel` | int | 时运等级 |
| `drops` | List\<WeightedItemStack\> | 掉落物列表（可设置） |
| `dropChance` | float | 整体掉率（可设置） |

方法：
- `event.addItem(IItemStack)` 向掉落列表添加物品

继承自 IBlockEvent 的 `world`、`blockState`、`block`、`position`、`x`、`y`、`z`。

```zenscript
events.onBlockHarvestDrops(function(event as BlockHarvestDropsEvent) {
    event.drops = [<item:minecraft:apple> % 100];
    event.addItem(<item:minecraft:arrow> * 2 % 20);
});
```

### BlockNeighborNotifyEvent（方块邻居通知事件）

> `import crafttweaker.event.BlockNeighborNotifyEvent;`

方块发生物理更新时触发（类似 BUD 开关）。仅在服务端调用。

实现接口：IEventCancelable, IBlockEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `forceRedstoneUpdate` | bool | 是否在 setBlock 调用时强制红石更新 |
| `notifiedSides` | IFacing[] | 接收更新的方向列表 |

继承自 IBlockEvent 的 `world`、`blockState`、`block`、`position`、`x`、`y`、`z`。

### BlockPlaceEvent（方块放置事件）

> `import crafttweaker.event.BlockPlaceEvent;`

方块被放置时触发。可取消以阻止放置。

实现接口：IEventCancelable, IBlockEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 放置方块的玩家 |
| `current` | IBlockState | 当前方块状态 |
| `placedAgainst` | IBlockState | 放置时对着的方块状态 |
| `hand` | string | 使用的手（主手/副手） |

继承自 IBlockEvent 的 `world`、`blockState`、`block`、`position`、`x`、`y`、`z`。

### FarmlandTrampleEvent（农田踩踏事件）

> `import crafttweaker.event.FarmlandTrampleEvent;`

农田被踩踏时触发。可取消以阻止踩踏。

实现接口：IEventCancelable, IBlockEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `entity` | IEntity | 踩踏农田的实体 |
| `fallDistance` | float | 踩踏前的摔落距离 |

继承自 IBlockEvent 的 `world`、`blockState`、`block`、`position`、`x`、`y`、`z`。

### CropGrowPostEvent（作物生长后事件）

> `import crafttweaker.event.CropGrowPostEvent;`

作物成功生长后触发。不可取消，仅作为通知。

实现接口：IBlockEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `originalBlockState` | IBlockState | 生长前的方块状态 |
| `originalBlock` | IBlock | 生长前的方块 |

继承自 IBlockEvent 的 `world`、`blockState`、`block`、`position`、`x`、`y`、`z`。

### CropGrowPreEvent（作物生长前事件）

> `import crafttweaker.event.CropGrowPreEvent;`

作物尝试生长时触发。可取消。

实现接口：IBlockEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `originalBlockState` | IBlockState | 生长前的方块状态 |
| `originalBlock` | IBlock | 生长前的方块 |
| `result` | string | 事件结果，值为 `default`、`deny` 或 `allow` |

继承自 IBlockEvent 的 `world`、`blockState`、`block`、`position`、`x`、`y`、`z`。

方法：
- `event.deny()` 阻止生长
- `event.allow()` 强制生长
- `event.default()` 使用原版行为

### LivingDestroyBlockEvent（生物破坏方块事件）

> `import crafttweaker.event.LivingDestroyBlockEvent;`

凋灵、末影龙尝试破坏方块或僵尸尝试破门时触发。可取消以阻止破坏。

实现接口：IEventPositionable, IEventCancelable, ILivingEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `state` | IBlockState | 被破坏的方块状态 |

继承自 ILivingEvent 的 `entityLivingBase`；继承自 IEventPositionable 的 `position`、`x`、`y`、`z`。

### PortalSpawnEvent（传送门生成事件）

> `import crafttweaker.event.PortalSpawnEvent;`

尝试生成下界传送门时触发。可取消以阻止传送门生成。

实现接口：IEventCancelable, IBlockEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `valid` | bool | 传送门是否有效（可生成） |
| `height` | int | 传送门高度 |
| `width` | int | 传送门宽度 |

继承自 IBlockEvent 的 `world`、`blockState`、`block`、`position`、`x`、`y`、`z`。
