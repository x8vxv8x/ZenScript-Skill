# 玩家事件 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.event.*;`

玩家相关事件，用于监听玩家合成、登录、交互等行为。

---

## API 列表

### PlayerCraftedEvent（玩家合成事件）

> `import crafttweaker.event.PlayerCraftedEvent;`

玩家合成物品时触发。

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 合成的玩家 |
| `output` | IItemStack | 合成结果 |
| `inventory` | ICraftingInventory | 合成网格 |

### PlayerSmeltedEvent（玩家熔炼事件）

> `import crafttweaker.event.PlayerSmeltedEvent;`

玩家从熔炉取出物品时触发。

### PlayerLoggedInEvent（玩家登录事件）

> `import crafttweaker.event.PlayerLoggedInEvent;`

玩家登录时触发。

### PlayerLoggedOutEvent（玩家登出事件）

> `import crafttweaker.event.PlayerLoggedOutEvent;`

玩家登出时触发。

### PlayerRespawnEvent（玩家重生事件）

> `import crafttweaker.event.PlayerRespawnEvent;`

玩家重生时触发。

### PlayerChangedDimensionEvent（玩家切换维度事件）

> `import crafttweaker.event.PlayerChangedDimensionEvent;`

玩家切换维度时触发。

### PlayerCloneEvent（玩家克隆事件）

> `import crafttweaker.event.PlayerCloneEvent;`

玩家被克隆时触发（如从末地返回）。

### PlayerTickEvent（玩家 Tick 事件）

> `import crafttweaker.event.PlayerTickEvent;`

玩家 Tick 时触发。

### PlayerAttackEntityEvent（玩家攻击实体事件）

> `import crafttweaker.event.PlayerAttackEntityEvent;`

玩家攻击实体时触发。

### PlayerInteractEvent（玩家交互事件）

> `import crafttweaker.event.PlayerInteractEvent;`

玩家交互时触发。

### PlayerInteractBlockEvent（玩家右键方块事件）

> `import crafttweaker.event.PlayerInteractBlockEvent;`

玩家右键方块时触发。

### PlayerInteractEntityEvent（玩家右键实体事件）

> `import crafttweaker.event.PlayerInteractEntityEvent;`

玩家右键实体时触发。

### PlayerRightClickItemEvent（玩家右键物品事件）

> `import crafttweaker.event.PlayerRightClickItemEvent;`

玩家右键物品时触发。

### PlayerLeftClickBlockEvent（玩家左键方块事件）

> `import crafttweaker.event.PlayerLeftClickBlockEvent;`

玩家左键方块时触发。

### PlayerDeathDropsEvent（玩家死亡掉落事件）

> `import crafttweaker.event.PlayerDeathDropsEvent;`

玩家死亡掉落时触发。

### PlayerDestroyItem（玩家物品损坏事件）

> `import crafttweaker.event.PlayerDestroyItem;`

玩家物品损坏时触发。

### PlayerFillBucketEvent（玩家填充桶事件）

> `import crafttweaker.event.PlayerFillBucketEvent;`

玩家填充桶时触发。

### PlayerItemPickupEvent（玩家拾取物品事件）

> `import crafttweaker.event.PlayerItemPickupEvent;`

玩家拾取物品时触发。

### PlayerPickupItemEvent（玩家拾取物品实体事件）

> `import crafttweaker.event.PlayerPickupItemEvent;`

玩家拾取物品实体时触发。

### PlayerPickupXpEvent（玩家拾取经验事件）

> `import crafttweaker.event.PlayerPickupXpEvent;`

玩家拾取经验时触发。

### PlayerOpenContainerEvent（玩家打开容器事件）

> `import crafttweaker.event.PlayerOpenContainerEvent;`

玩家打开容器时触发。

### PlayerCloseContainerEvent（玩家关闭容器事件）

> `import crafttweaker.event.PlayerCloseContainerEvent;`

玩家关闭容器时触发。

### PlayerBonemealEvent（玩家使用骨粉事件）

> `import crafttweaker.event.PlayerBonemealEvent;`

玩家使用骨粉时触发。

### PlayerUseHoeEvent（玩家使用锄头事件）

> `import crafttweaker.event.PlayerUseHoeEvent;`

玩家使用锄头时触发。

### PlayerBreakSpeed（玩家挖掘速度事件）

> `import crafttweaker.event.PlayerBreakSpeed;`

玩家挖掘速度计算时触发。

### PlayerBrewedPotion（玩家酿造药水事件）

> `import crafttweaker.event.PlayerBrewedPotion;`

玩家酿造药水时触发。

### PlayerSleepInBedEvent（玩家睡觉事件）

> `import crafttweaker.event.PlayerSleepInBedEvent;`

玩家尝试睡觉时触发。

### PlayerAdvancementEvent（玩家获得进度事件）

> `import crafttweaker.event.PlayerAdvancementEvent;`

玩家获得进度时触发。

### PlayerAnvilRepairEvent（玩家铁砧修复事件）

> `import crafttweaker.event.PlayerAnvilRepairEvent;`

玩家在铁砧修复物品时触发。

### PlayerAnvilUpdateEvent（玩家铁砧更新事件）

> `import crafttweaker.event.PlayerAnvilUpdateEvent;`

玩家在铁砧更新物品时触发。

### PlayerSetSpawn（玩家设置重生点事件）

> `import crafttweaker.event.PlayerSetSpawn;`

玩家设置重生点时触发。

### PlayerVisibilityEvent（玩家可见性事件）

> `import crafttweaker.event.PlayerVisibilityEvent;`

玩家可见性变化时触发。
