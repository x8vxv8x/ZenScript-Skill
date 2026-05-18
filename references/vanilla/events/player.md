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
