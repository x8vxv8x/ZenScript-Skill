# 玩家饥饿/食物事件 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: HungerTweaker + AppleCore
> 导入: `import mods.hungertweaker.events.HungerEvents;`

HungerTweaker 暴露的 AppleCore 事件，用于玩家相关的饥饿/疲劳/恢复控制。事件处理器中可访问 `event.player`（IPlayer）。

---

## API 列表

### 食物事件

#### GetFoodValuesEvent（获取食物属性事件）

每次获取食物属性时触发，可根据玩家动态修改食物属性。

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
