# 实体战斗事件 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.event.*;`

实体被攻击、受伤、回血、跳跃、击退等战斗事件。

---

## API 列表

### EntityLivingAttackedEvent（实体被攻击事件）

> `import crafttweaker.event.EntityLivingAttackedEvent;`

实体被攻击时触发。可取消以阻止受伤。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `damageSource` | IDamageSource | 伤害来源 |
| `amount` | float | 伤害值 |

继承自 ILivingEvent 的 `entityLivingBase`。

### EntityLivingDamageEvent（实体受伤事件）

> `import crafttweaker.event.EntityLivingDamageEvent;`

实体受伤前触发。此时护甲、药水、吸收等修正已应用，这是**最终伤害值**。注意：护甲耐久和吸收心等资源已被消耗，取消后**不会恢复**。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `damageSource` | IDamageSource | 伤害来源 |
| `amount` | float | 最终伤害值（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

### EntityLivingHurtEvent（实体受伤事件）

> `import crafttweaker.event.EntityLivingHurtEvent;`

实体即将受伤时触发。可取消以阻止受伤。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `amount` | float | 伤害量（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

### EntityLivingHealEvent（实体回血事件）

> `import crafttweaker.event.EntityLivingHealEvent;`

实体即将被治疗时触发。可取消以阻止治疗。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `amount` | float | 治疗量（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

### EntityLivingJumpEvent（实体跳跃事件）

> `import crafttweaker.event.EntityLivingJumpEvent;`

实体跳跃时触发。

实现接口：ILivingEvent

继承自 ILivingEvent 的 `entityLivingBase`。

### LivingKnockBackEvent（生物被击退事件）

> `import crafttweaker.event.LivingKnockBackEvent;`

实体被击退时触发。可取消以阻止击退。可调整击退力度和方向比率。

实现接口：IEventCancelable, ILivingEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `attacker` | IEntity | 攻击者（可设置） |
| `originalAttacker` | IEntity | 原始攻击者 |
| `strength` | float | 击退力度（可设置） |
| `originalStrength` | float | 原始击退力度 |
| `ratioX` | double | X 方向比率（可设置） |
| `ratioZ` | double | Z 方向比率（可设置） |
| `originalRatioX` | double | 原始 X 方向比率 |
| `originalRatioZ` | double | 原始 Z 方向比率 |

继承自 ILivingEvent 的 `entityLivingBase`。

注：事件触发时 `attacker`、`strength`、`ratioX`、`ratioZ` 可能已被其他事件修改，可通过 `original*` 变量获取原始值。
