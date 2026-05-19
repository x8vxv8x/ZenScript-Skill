# 玩家事件 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.event.*;`

玩家相关事件，用于监听玩家合成、登录、交互等行为。

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

### PlayerLoggedInEvent（玩家登录事件）

> `import crafttweaker.event.PlayerLoggedInEvent;`

玩家登录时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 登录的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerLoggedOutEvent（玩家登出事件）

> `import crafttweaker.event.PlayerLoggedOutEvent;`

玩家登出时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 登出的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerRespawnEvent（玩家重生事件）

> `import crafttweaker.event.PlayerRespawnEvent;`

玩家重生时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `endConquered` | bool | 是否因跳过末地折跃门（Credits 传送门）而重生 |
| `player` | IPlayer | 重生的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerChangedDimensionEvent（玩家切换维度事件）

> `import crafttweaker.event.PlayerChangedDimensionEvent;`

玩家切换维度时触发（如进入/离开下界）。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `from` | int | 来源维度 ID |
| `fromWorld` | IWorld | 来源世界 |
| `to` | int | 目标维度 ID |
| `toWorld` | IWorld | 目标世界 |
| `player` | IPlayer | 切换维度的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerCloneEvent（玩家克隆事件）

> `import crafttweaker.event.PlayerCloneEvent;`

玩家被克隆时触发。通常在重生或从末地返回时发生。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `originalPlayer` | IPlayer | 原始玩家对象 |
| `wasDeath` | bool | 是否因死亡而克隆（维度传送时为 false） |
| `player` | IPlayer | 克隆后的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerTickEvent（玩家 Tick 事件）

> `import crafttweaker.event.PlayerTickEvent;`

每个玩家每 Tick 触发（客户端和服务端都会触发）。

实现接口：IPlayerEvent, ITickEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 玩家 |
| `phase` | string | Tick 阶段，值为 `START` 或 `END` |
| `side` | string | 执行端，值为 `CLIENT` 或 `SERVER` |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerAttackEntityEvent（玩家攻击实体事件）

> `import crafttweaker.event.PlayerAttackEntityEvent;`

玩家攻击实体时触发。可取消以阻止攻击。

实现接口：IEventCancelable, IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `target` | IEntity | 被攻击的实体 |
| `player` | IPlayer | 攻击的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerInteractEvent（玩家交互事件）

> `import crafttweaker.event.PlayerInteractEvent;`

玩家与方块交互时触发。可取消。

实现接口：IEventCancelable, IPlayerEvent, IEventPositionable

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |
| `blockState` | IBlockState | 方块状态 |
| `block` | IBlock | 方块对象 |
| `face` | IFacing | 交互面 |
| `item` | IItemStack | 手持物品 |
| `dimension` | int | 维度 ID |
| `hand` | string | 使用的手（主手/副手） |
| `player` | IPlayer | 交互的玩家 |

方法：
- `event.damageItem(int amount)` 对手持物品造成指定耐久损伤

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`；继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerInteractBlockEvent（玩家右键方块事件）

> `import crafttweaker.event.PlayerInteractBlockEvent;`

玩家右键方块时触发。可取消。取消后可设置 `cancellationResult` 为 `success`、`fail` 或 `pass`（默认为 `pass`）。

实现接口：IEventCancelable, IProcessableEvent, IEventPositionable, IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `hitvector` | IVector3d | 命中向量 |
| `useblock` | string | 方块使用结果（可设置，值为 `allow` / `deny` / `default`） |
| `useitem` | string | 物品使用结果（可设置，值为 `allow` / `deny` / `default`） |
| `cancellationResult` | string | 取消结果（可设置，值为 `success` / `pass` / `fail`） |
| `world` | IWorld | 世界对象 |
| `blockState` | IBlockState | 方块状态 |
| `block` | IBlock | 方块对象 |
| `face` | IFacing | 交互面 |
| `item` | IItemStack | 手持物品 |
| `dimension` | int | 维度 ID |
| `hand` | string | 使用的手 |
| `player` | IPlayer | 交互的玩家 |

方法：
- `event.damageItem(int amount)` 对手持物品造成指定耐久损伤

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`；继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerInteractEntityEvent（玩家右键实体事件）

> `import crafttweaker.event.PlayerInteractEntityEvent;`

玩家右键实体时触发。可取消。取消后可设置结果。

实现接口：IEventCancelable, IProcessableEvent, IEventPositionable, IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `target` | IEntity | 被交互的实体 |
| `world` | IWorld | 世界对象 |
| `blockState` | IBlockState | 方块状态 |
| `block` | IBlock | 方块对象 |
| `face` | IFacing | 交互面 |
| `item` | IItemStack | 手持物品 |
| `dimension` | int | 维度 ID |
| `hand` | string | 使用的手 |
| `player` | IPlayer | 交互的玩家 |

方法：
- `event.damageItem(int amount)` 对手持物品造成指定耐久损伤

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`；继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerRightClickItemEvent（玩家右键物品事件）

> `import crafttweaker.event.PlayerRightClickItemEvent;`

在物品功能触发前触发（当玩家未指向方块或实体时）。可取消以阻止后续事件。

实现接口：IEventCancelable, IProcessableEvent, IEventPositionable, IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `cancellationResult` | string | 取消结果（可设置，值为 `success` / `pass` / `fail`） |
| `world` | IWorld | 世界对象 |
| `blockState` | IBlockState | 方块状态 |
| `block` | IBlock | 方块对象 |
| `face` | IFacing | 交互面 |
| `item` | IItemStack | 手持物品 |
| `dimension` | int | 维度 ID |
| `hand` | string | 使用的手 |
| `player` | IPlayer | 交互的玩家 |

方法：
- `event.damageItem(int amount)` 对手持物品造成指定耐久损伤

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`；继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerLeftClickBlockEvent（玩家左键方块事件）

> `import crafttweaker.event.PlayerLeftClickBlockEvent;`

玩家左键方块时触发。可取消以阻止左键操作（阻止方块破坏，但在创造模式下无效）。按住左键时即使取消也会持续触发。取消后可设置结果。

实现接口：IEventCancelable, IProcessableEvent, IEventPositionable, IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `hitvector` | IVector3d | 命中向量 |
| `useblock` | string | 方块使用结果（可设置，值为 `allow` / `deny` / `default`） |
| `useitem` | string | 物品使用结果（可设置，值为 `allow` / `deny` / `default`） |
| `cancellationResult` | string | 取消结果（可设置，值为 `success` / `pass` / `fail`） |
| `world` | IWorld | 世界对象 |
| `blockState` | IBlockState | 方块状态 |
| `block` | IBlock | 方块对象 |
| `face` | IFacing | 交互面 |
| `item` | IItemStack | 手持物品 |
| `dimension` | int | 维度 ID |
| `hand` | string | 使用的手 |
| `player` | IPlayer | 交互的玩家 |

方法：
- `event.damageItem(int amount)` 对手持物品造成指定耐久损伤

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`；继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerDeathDropsEvent（玩家死亡掉落事件）

> `import crafttweaker.event.PlayerDeathDropsEvent;`

玩家死亡导致物品掉落时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `items` | List\<IEntityItem\> | 掉落物列表（可设置） |
| `damageSource` | IDamageSource | 伤害来源 |
| `player` | IPlayer | 死亡的玩家 |

方法：
- `event.addItem(IItemStack)` 向掉落列表添加物品
- `event.addItem(IEntityItem)` 向掉落列表添加物品实体

继承自 IPlayerEvent 的 `entityLivingBase`。

```zenscript
events.onPlayerDeathDrops(function(event as PlayerDeathDropsEvent) {
    event.items = []; // 清空掉落
    event.addItem(<item:minecraft:iron_ingot>); // 添加物品
});
```

### PlayerDestroyItemEvent（玩家物品损坏事件）

> `import crafttweaker.event.PlayerDestroyItemEvent;`

玩家物品损坏（耐久耗尽）时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `originalItem` | IItemStack | 损坏前的物品 |
| `hand` | string | 使用的手（主手/副手） |
| `player` | IPlayer | 物品损坏的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerFillBucketEvent（玩家填充桶事件）

> `import crafttweaker.event.PlayerFillBucketEvent;`

玩家填充桶时触发。可取消。

实现接口：IEventCancelable, IProcessableEvent, IEventPositionable, IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `result` | IItemStack | 填充后的桶物品（可设置） |
| `emptyBucket` | IItemStack | 空桶物品 |
| `world` | IWorld | 世界对象 |
| `blockState` | IBlockState | 方块状态 |
| `block` | IBlock | 方块对象 |
| `dimension` | int | 维度 ID |
| `rayTraceResult` | IRayTraceResult | 射线追踪结果 |
| `player` | IPlayer | 填充桶的玩家 |

方法：
- `event.deny()` 设置结果为 `deny`
- `event.allow()` 设置结果为 `allow`
- `event.default()` 设置结果为 `default`

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`；继承自 IPlayerEvent 的 `entityLivingBase`。

注：此事件同时继承 IProcessableEvent 的 `result`（string 类型，值为 `default`/`deny`/`allow`）和自身的 `result`（IItemStack 类型，用于设置填充后的物品）。使用 `event.result = <item:minecraft:stick>` 会将玩家手中的桶替换为木棍。

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

### PlayerOpenContainerEvent（玩家打开容器事件）

> `import crafttweaker.event.PlayerOpenContainerEvent;`

玩家打开容器时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `container` | IContainer | 被打开的容器 |
| `player` | IPlayer | 打开容器的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerCloseContainerEvent（玩家关闭容器事件）

> `import crafttweaker.event.PlayerCloseContainerEvent;`

玩家关闭容器时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `container` | IContainer | 被关闭的容器 |
| `player` | IPlayer | 关闭容器的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerBonemealEvent（玩家使用骨粉事件）

> `import crafttweaker.event.PlayerBonemealEvent;`

玩家在方块上使用骨粉时触发。可取消。

实现接口：IEventCancelable, IProcessableEvent, IEventPositionable, IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |
| `block` | IBlock | 方块对象 |
| `blockState` | IBlockState | 方块状态 |
| `dimension` | int | 维度 ID |
| `item` | IItemStack | 手持物品（骨粉） |
| `player` | IPlayer | 使用骨粉的玩家 |

方法：
- `event.deny()` 设置结果为 `deny`
- `event.allow()` 设置结果为 `allow`
- `event.default()` 设置结果为 `default`

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`；继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerUseHoeEvent（玩家使用锄头事件）

> `import crafttweaker.event.PlayerUseHoeEvent;`

玩家使用锄头时触发。可取消。

实现接口：IEventCancelable, IProcessableEvent, IEventPositionable, IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |
| `block` | IBlock | 方块对象 |
| `blockState` | IBlockState | 方块状态 |
| `dimension` | int | 维度 ID |
| `item` | IItemStack | 手持物品（锄头） |
| `player` | IPlayer | 使用锄头的玩家 |

方法：
- `event.deny()` 设置结果为 `deny`
- `event.allow()` 设置结果为 `allow`
- `event.default()` 设置结果为 `default`

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`；继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerBreakSpeedEvent（玩家挖掘速度事件）

> `import crafttweaker.event.PlayerBreakSpeedEvent;`

玩家尝试破坏方块时计算挖掘速度触发。可取消以阻止破坏。

实现接口：IEventCancelable, IPlayerEvent, IEventPositionable

| 属性 | 类型 | 说明 |
|------|------|------|
| `blockState` | IBlockState | 方块状态 |
| `block` | IBlock | 方块对象 |
| `originalSpeed` | float | 原始挖掘速度 |
| `newSpeed` | float | 新挖掘速度（可设置） |
| `player` | IPlayer | 挖掘的玩家 |

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`；继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerBrewedPotionEvent（玩家酿造药水事件）

> `import crafttweaker.event.PlayerBrewedPotionEvent;`

玩家从酿造台取出药水时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `potion` | IItemStack | 药水物品 |
| `player` | IPlayer | 取出药水的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerSleepInBedEvent（玩家睡觉事件）

> `import crafttweaker.event.PlayerSleepInBedEvent;`

玩家尝试睡觉时触发。可通过设置 `result` 控制是否允许睡觉。

实现接口：IPlayerEvent, IEventPositionable

| 属性 | 类型 | 说明 |
|------|------|------|
| `result` | string | 结果（可设置），值为 `NOT_POSSIBLE_HERE`、`NOT_POSSIBLE_NOW`、`NOT_SAFE`、`OK` 或 `OTHER_PROBLEM` |
| `player` | IPlayer | 尝试睡觉的玩家 |

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`；继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerAdvancementEvent（玩家获得进度事件）

> `import crafttweaker.event.PlayerAdvancementEvent;`

玩家获得进度时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `id` | string | 进度 ID（如 `minecraft:story/mine_diamond`） |
| `player` | IPlayer | 获得进度的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerAnvilRepairEvent（玩家铁砧修复事件）

> `import crafttweaker.event.PlayerAnvilRepairEvent;`

玩家在铁砧合成物品时触发。可修改铁砧损坏概率。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `itemInput` | IItemStack | 左侧输入物品 |
| `itemIngredient` | IItemStack | 右侧输入物品 |
| `itemResult` | IItemStack | 输出物品 |
| `breakChance` | float | 铁砧损坏概率（可设置） |
| `player` | IPlayer | 修复的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerAnvilUpdateEvent（玩家铁砧更新事件）

> `import crafttweaker.event.PlayerAnvilUpdateEvent;`

玩家在铁砧左右槽位都放入物品时触发。可取消。取消后原版行为不执行且输出设为 null。若未取消但 `outputItem` 不为 null，则使用自定义输出。若 `outputItem` 为 null 且未取消，执行原版行为。

实现接口：IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `leftItem` | IItemStack | 左侧输入物品 |
| `rightItem` | IItemStack | 右侧输入物品 |
| `outputItem` | IItemStack | 输出物品（可设置，设置后跳过原版行为） |
| `itemName` | string | 玩家设置的物品名称 |
| `xpCost` | int | 经验消耗（可设置） |
| `materialCost` | int | 右侧消耗物品数量（可设置，0 表示消耗整个堆叠） |

### PlayerSetSpawnEvent（玩家设置重生点事件）

> `import crafttweaker.event.PlayerSetSpawnEvent;`

玩家重生点位置变化时触发。可取消。

实现接口：IPlayerEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `isForced` | bool | 是否强制设置 |
| `newSpawn` | IBlockPos | 新重生点位置 |
| `player` | IPlayer | 设置重生点的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerVisibilityEvent（玩家可见性事件）

> `import crafttweaker.event.PlayerVisibilityEvent;`

确定玩家可见性时触发，用于计算生物发现玩家的距离。无法直接设置 `modifier`，需要通过 `modifyVisibility` 方法修改。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `modifier` | double | 可见性修正值 |
| `player` | IPlayer | 玩家 |

方法：
- `event.modifyVisibility(double value)` 将 `modifier` 替换为 `modifier * value`

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerUseItemStartEvent（玩家开始使用物品事件）

> `import crafttweaker.event.PlayerUseItemStartEvent;`

玩家开始使用物品时触发（如开始拉弓、食用食物等）。可取消。

实现接口：IEventCancelable, IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IItemStack | 被使用的物品 |
| `player` | IPlayer | 使用物品的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerUseItemTickEvent（玩家使用物品 Tick 事件）

> `import crafttweaker.event.PlayerUseItemTick;`

玩家持续使用物品时每 Tick 触发。可取消。

实现接口：IEventCancelable, IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IItemStack | 被使用的物品 |
| `duration` | int | 使用持续时间 |
| `player` | IPlayer | 使用物品的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

---

## HungerTweaker 扩展（需安装 HungerTweaker + AppleCore）

> `import mods.hungertweaker.events.HungerEvents;`

HungerTweaker 暴露的 AppleCore 事件，用于玩家相关的饥饿/疲劳/恢复控制。事件处理器中可访问 `event.player`（IPlayer）。

### 食物事件

#### GetFoodValuesEvent（获取食物属性事件）

每次获取食物属性时触发，可用于根据玩家动态修改食物属性。

| 属性 | 类型 | 读写 | 说明 |
|------|------|------|------|
| `hunger` | int | 可修改 | 饥饿值 |
| `saturationModifier` | float | 可修改 | 饱和度修正值 |
| `unmodifiedHunger` | int | 只读 | 原始饥饿值 |
| `unmodifiedSaturationModifier` | float | 只读 | 原始饱和度修正值 |
| `food` | IItemStack | 只读 | 食物物品 |
| `player` | IPlayer | 只读 | 玩家 |

#### FoodEatenEvent（食物食用后事件）

食物被食用后触发。

| 属性 | 类型 | 说明 |
|------|------|------|
| `hunger` | int | 食物饥饿值 |
| `saturationModifier` | float | 饱和度修正值 |
| `hungerAdded` | int | 实际增加的饥饿值 |
| `saturationAdded` | float | 实际增加的饱和度 |
| `food` | IItemStack | 食物物品 |
| `player` | IPlayer | 玩家 |

#### CTFoodStatsAdditionEvent（食物食用前事件）

食物即将被食用时触发。可取消，取消后食物不会被食用。

| 属性 | 类型 | 说明 |
|------|------|------|
| `hunger` | int | 食物饥饿值 |
| `saturationModifier` | float | 饱和度修正值 |
| `player` | IPlayer | 玩家 |

### 疲劳事件

#### AllowExhaustionEvent（允许疲劳事件）

判断玩家是否可以疲劳。可通过方法控制：

| 方法 | 说明 |
|------|------|
| `allow()` | 强制允许疲劳 |
| `deny()` | 强制禁止疲劳 |
| `pass()` | 使用原版条件 |

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 玩家 |

#### ExhaustedEvent（疲劳事件）

玩家疲劳时触发。

| 属性 | 类型 | 读写 | 说明 |
|------|------|------|------|
| `deltaHunger` | int | 可修改 | 饥饿值变化量 |
| `deltaSaturation` | float | 可修改 | 饱和度变化量 |
| `currentExhaustionLevel` | float | 只读 | 当前疲劳值 |
| `player` | IPlayer | 只读 | 玩家 |

#### ExhaustingActionEvent（疲劳行为事件）

玩家执行疲劳行为时触发。

| 属性 | 类型 | 读写 | 说明 |
|------|------|------|------|
| `deltaExhaustion` | float | 可修改 | 疲劳值获取量 |
| `action` | string | 只读 | 行为类型（如 `HARVEST_BLOCK`、`SPRINTING_JUMP` 等） |
| `player` | IPlayer | 只读 | 玩家 |

#### GetMaxExhaustionEvent（获取最大疲劳值事件）

获取玩家最大疲劳值时触发。

| 属性 | 类型 | 读写 | 说明 |
|------|------|------|------|
| `maxExhaustionLevel` | float | 可修改 | 最大疲劳值 |
| `player` | IPlayer | 只读 | 玩家 |

### 饥饿值事件

#### GetMaxHungerEvent（获取最大饥饿值事件）

获取玩家最大饥饿值时触发。

| 属性 | 类型 | 读写 | 说明 |
|------|------|------|------|
| `maxHunger` | int | 可修改 | 最大饥饿值 |
| `player` | IPlayer | 只读 | 玩家 |

### 饥饿伤害事件

#### AllowStarvationEvent（允许饥饿伤害事件）

判断玩家是否可以受到饥饿伤害。可通过 `allow()`/`deny()`/`pass()` 控制。

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 玩家 |

#### GetStarveTickPeriodEvent（获取饥饿伤害间隔事件）

获取饥饿伤害间隔时触发。

| 属性 | 类型 | 读写 | 说明 |
|------|------|------|------|
| `starveTickPeriod` | int | 可修改 | 饥饿伤害间隔（tick），原版为 80 |
| `player` | IPlayer | 只读 | 玩家 |

#### StarveEvent（饥饿伤害事件）

玩家受到饥饿伤害时触发。可取消。

| 属性 | 类型 | 读写 | 说明 |
|------|------|------|------|
| `starveDamage` | float | 可修改 | 饥饿伤害值 |
| `player` | IPlayer | 只读 | 玩家 |

### 生命恢复事件

#### AllowRegenEvent（允许生命恢复事件）

判断玩家是否可以恢复生命。可通过 `allow()`/`deny()`/`pass()` 控制。

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 玩家 |

#### AllowSaturatedRegenEvent（允许饱和恢复事件）

判断玩家是否可以通过饱和恢复生命。可通过 `allow()`/`deny()`/`pass()` 控制。

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 玩家 |

#### GetRegenTickPeriodEvent（获取恢复间隔事件）

获取生命恢复间隔时触发。

| 属性 | 类型 | 读写 | 说明 |
|------|------|------|------|
| `regenTickPeriod` | int | 可修改 | 恢复间隔（tick），原版为 80 |
| `player` | IPlayer | 只读 | 玩家 |

#### GetSaturatedRegenTickPeriodEvent（获取饱和恢复间隔事件）

获取饱和恢复间隔时触发。

| 属性 | 类型 | 读写 | 说明 |
|------|------|------|------|
| `regenTickPeriod` | int | 可修改 | 饱和恢复间隔（tick），原版为 10 |
| `player` | IPlayer | 只读 | 玩家 |

#### RegenEvent（生命恢复事件）

玩家恢复生命时触发。可取消。

| 属性 | 类型 | 读写 | 说明 |
|------|------|------|------|
| `deltaHealth` | float | 可修改 | 恢复生命值 |
| `deltaExhaustion` | float | 可修改 | 恢复产生的疲劳值 |
| `player` | IPlayer | 只读 | 玩家 |

#### SaturatedRegenEvent（饱和恢复事件）

玩家通过饱和恢复生命时触发。可取消。

| 属性 | 类型 | 读写 | 说明 |
|------|------|------|------|
| `deltaHealth` | float | 可修改 | 恢复生命值 |
| `deltaExhaustion` | float | 可修改 | 恢复产生的疲劳值 |
| `player` | IPlayer | 只读 | 玩家 |

#### PeacefulRegenEvent（和平模式恢复事件）

和平模式下恢复生命时触发。可取消。

| 属性 | 类型 | 读写 | 说明 |
|------|------|------|------|
| `deltaHealth` | float | 可修改 | 恢复生命值 |
| `player` | IPlayer | 只读 | 玩家 |

### 事件注册示例

```zenscript
import mods.hungertweaker.events.HungerEvents;

// 禁止特定玩家疲劳
HungerEvents.onAllowExhaustion(function(event) {
    if (event.player.name == "Steve") event.deny();
});

// 修改食物属性（根据玩家）
HungerEvents.onGetFoodValues(function(event) {
    if (event.player.isCreative) {
        event.hunger = 1;
    }
});

// 饥饿伤害加倍
HungerEvents.onStarve(function(event) {
    event.starveDamage = event.starveDamage * 2;
});
```
