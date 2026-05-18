# HungerTweaker CraftTweaker API 参考

> Mod ID: `hungertweaker`
> 前置条件: AppleCore
> 导入: `import mods.hungertweaker.*;`

HungerTweaker 是 AppleCore 与 CraftTweaker 的桥梁，允许通过脚本修改食物和饥饿相关属性。所有参数均支持数字或 Expression 表达式。

---

## API 列表

### FoodValues（食物属性）

> 通过 `IIngredient.foodValues` 获取

修改匹配物品的食物属性。当多个 IIngredient 匹配同一物品时，后获取的 FoodValues 实例生效。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `hunger` | number / Expression | 食物恢复的饥饿值 |
| `saturationModifier` | number / Expression | 饱和度修正值。实际饱和度 = 饥饿值 × 饱和度修正 × 2，且总饱和度不超过总饥饿值 |

#### @ZenGetter（只读）

| 属性 | 类型 | 说明 |
|------|------|------|
| `unmodifiedHunger` | number | 未修改的原始饥饿值 |
| `unmodifiedSaturationModifier` | number | 未修改的原始饱和度修正值 |

注：Getter 仅对单物品 IItemStack 有效。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setHunger(IData)` | 未说明 | 设置饥饿值（同 hunger setter） |
| `.setSaturationModifier(IData)` | 未说明 | 设置饱和度修正值（同 saturationModifier setter） |

---

### Hunger（饥饿值）

> `import mods.hungertweaker.Hunger;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `Hunger.setMaxHunger(IData)` | 未说明 | 设置饥饿值上限。注意：UI 不受影响，饥饿阈值不变（如冲刺仍需 6 饥饿值） |

---

### Exhaustion（疲劳值）

> `import mods.hungertweaker.Exhaustion;`

修改疲劳效果、最大疲劳值，以及启用/禁用疲劳。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `Exhaustion.setMaxExhaustionLevel(IData)` | 未说明 | 设置疲劳导致饥饿损失的阈值 |
| `Exhaustion.setDeltaExhaustion(IData)` | 未说明 | 设置疲劳时增加的疲劳值（默认等于最大疲劳值） |
| `Exhaustion.setDeltaHunger(IData)` | 未说明 | 设置疲劳时减少的饥饿值（受难度等因素影响） |
| `Exhaustion.setDeltaSaturation(IData)` | 未说明 | 设置疲劳时减少的饱和度（受难度等因素影响） |
| `Exhaustion.setStatus(int)` | 未说明 | 疲劳状态：0 = 禁用，1 = 原版条件，2 = 强制启用 |

---

### ExhaustingAction（疲劳行为）

> `import mods.hungertweaker.ExhaustingAction;`

修改特定行为的疲劳值获取量。

#### 常量

| 常量 | 说明 |
|------|------|
| `HARVEST_BLOCK` | 采集方块 |
| `NORMAL_JUMP` | 普通跳跃 |
| `SPRINTING_JUMP` | 冲刺跳跃 |
| `ATTACK_ENTITY` | 攻击实体 |
| `DAMAGE_TAKEN` | 受到伤害 |
| `HUNGER_POTION` | 饥饿药水 |
| `MOVEMENT_DIVE` | 潜水移动 |
| `MOVEMENT_SWIM` | 游泳移动 |
| `MOVEMENT_SPRINT` | 冲刺移动 |
| `MOVEMENT_CROUCH` | 潜行移动 |
| `MOVEMENT_WALK` | 行走移动 |
| `ALL` | 包含以上所有行为的数组 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setDeltaExhaustion(IData)` | 未说明 | 设置该行为产生的疲劳值。注意：会覆盖之前的值，如需先全局修改再单独修改，应先设全局再设单独 |

---

### Starvation（饥饿伤害）

> `import mods.hungertweaker.Starvation;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `Starvation.setInterval(IData)` | 未说明 | 设置饥饿伤害间隔（tick） |
| `Starvation.setDamage(IData)` | 未说明 | 设置饥饿伤害量 |
| `Starvation.setStatus(int)` | 未说明 | 饥饿状态：0 = 禁用，1 = 原版条件，2 = 强制启用 |

---

### Regen（生命恢复）

> `import mods.hungertweaker.Regen;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `Regen.setInterval(IData)` | 未说明 | 设置恢复间隔（tick） |
| `Regen.setDeltaExhaustion(IData)` | 未说明 | 设置恢复时增加的疲劳值 |
| `Regen.setDeltaHealth(IData)` | 未说明 | 设置恢复的生命值 |
| `Regen.setStatus(int)` | 未说明 | 恢复状态：0 = 禁用，1 = 原版条件，2 = 强制启用 |

---

### SaturatedRegen（饱和恢复）

> `import mods.hungertweaker.SaturatedRegen;`

饥饿值和饱和度均满时的生命恢复。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `SaturatedRegen.setInterval(IData)` | 未说明 | 设置恢复间隔（tick） |
| `SaturatedRegen.setDeltaExhaustion(IData)` | 未说明 | 设置恢复时增加的疲劳值 |
| `SaturatedRegen.setDeltaHealth(IData)` | 未说明 | 设置恢复的生命值 |
| `SaturatedRegen.setStatus(int)` | 未说明 | 恢复状态：0 = 禁用，1 = 原版条件，2 = 强制启用 |

---

### PeacefulRegen（和平模式恢复）

> `import mods.hungertweaker.PeacefulRegen;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `PeacefulRegen.setDeltaHealth(IData)` | 未说明 | 设置和平模式下恢复的生命值 |
| `PeacefulRegen.setStatus(int)` | 未说明 | 恢复状态：0 = 禁用，1 = 原版条件，2 = 强制启用 |

---

### HUD（界面显示）

> `import mods.hungertweaker.HUD;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `HUD.setStatus(IData)` | 未说明 | 食物条显示状态：0 / "DENY" = 禁用，1 / "DEFAULT" = 原版条件，2 / "ALLOW" = 强制显示 |

---

## Expression 表达式

HungerTweaker 支持表达式字符串作为参数，使用变量 `x`（当前值）。

### 运算符

`+`、`-`、`*`、`/`、`^`（幂）

### 函数

| 函数 | 说明 |
|------|------|
| `sqrt(x)` | 平方根 |
| `sin(x)` / `cos(x)` / `tan(x)` | 三角函数 |
| `ceil(x)` | 向上取整 |
| `round(x)` | 四舍五入 |
| `nextUp(x)` / `nextDown(x)` | 上/下一个可表示值 |
| `max(a, b)` / `min(a, b)` | 最大/最小值 |
| `clamp(v, min, max)` | 将 v 限制在 [min, max] 范围内 |
| `random()` | 0（含）到 1（不含）的随机数 |
| `random(n)` | 0（含）到 n（不含）的随机整数 |

### 用法区别

- **带引号**（HungerTweaker 表达式）：每次检查值时动态求值，可用变量 `x`
- **不带引号**（CraftTweaker 表达式）：脚本加载时求值一次，不可用 `x`

```zenscript
// 正确：动态表达式
mods.hungertweaker.Hunger.setMaxHunger("x*2");
// 正确：静态值
mods.hungertweaker.Hunger.setMaxHunger(20);
// 错误：x 未定义
mods.hungertweaker.Hunger.setMaxHunger(x*2);
```

---

## 使用示例

### 修改食物属性

```zenscript
import mods.hungertweaker.FoodValues;

// 苹果恢复 10 饥饿值
<minecraft:apple>.foodValues.hunger = 10;

// 所有水果类食物饥饿值翻倍
<ore:fruit>.foodValues.hunger = "x*2";
```

### 修改疲劳行为

```zenscript
import mods.hungertweaker.ExhaustingAction;

// 冲刺疲劳翻倍
ExhaustingAction.MOVEMENT_SPRINT.setDeltaExhaustion("x*2");

// 所有行为疲劳减半，游泳除外
for action in ExhaustingAction.ALL {
    action.setDeltaExhaustion("x/2");
}
ExhaustingAction.MOVEMENT_SWIM.setDeltaExhaustion("x*20");
```

### 禁用特定玩家的疲劳

```zenscript
mods.hungertweaker.events.HungerEvents.onAllowExhaustion(function(event as mods.hungertweaker.events.AllowExhaustionEvent) {
    if (event.player.name == "me") {
        event.deny();
    }
});
```
