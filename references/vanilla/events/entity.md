# 实体事件

## EntityJoinWorldEvent

> `import crafttweaker.event.EntityJoinWorldEvent;`

实体加入世界时触发。可取消以阻止实体加入。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |

继承自 IEntityEvent 的 `entity`。

```zenscript
events.onEntityJoinWorld(function(event as EntityJoinWorldEvent) {
    if (!isNull(event.entity.definition) && event.entity.definition.id == "minecraft:creeper") {
        event.cancel();
    }
});
```

---

## EntityLivingSpawnEvent / EntityLivingExtendedSpawnEvent

> `import crafttweaker.event.EntityLivingSpawnEvent;`
> `import crafttweaker.event.EntityLivingExtendedSpawnEvent;`

实体尝试加入或离开世界时触发。`EntityLivingExtendedSpawnEvent` 包含刷怪笼引用。

实现接口：ILivingEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |
| `x` | float | X 坐标 |
| `y` | float | Y 坐标 |
| `z` | float | Z 坐标 |
| `spawner` | IMobSpawnerBaseLogic | 刷怪笼逻辑（仅 Extended） |

方法：
- `event.allow()` 强制实体生成/消失
- `event.deny()` 阻止实体生成/消失
- `event.pass()` 设置为默认状态

继承自 ILivingEvent 的 `entityLivingBase`。

---

## EntityLivingAttackedEvent

> `import crafttweaker.event.EntityLivingAttackedEvent;`

实体被攻击时触发。可取消以阻止受伤。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `damageSource` | IDamageSource | 伤害来源 |
| `amount` | float | 伤害值 |

继承自 ILivingEvent 的 `entityLivingBase`。

---

## EntityLivingDamageEvent

> `import crafttweaker.event.EntityLivingDamageEvent;`

实体受伤前触发。此时护甲、药水、吸收等修正已应用，这是**最终伤害值**。注意：护甲耐久和吸收心等资源已被消耗，取消后**不会恢复**。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `damageSource` | IDamageSource | 伤害来源 |
| `amount` | float | 最终伤害值（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

---

## EntityLivingDeathEvent

> `import crafttweaker.event.EntityLivingDeathEvent;`

实体即将死亡时触发。可取消以让实体存活。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `damageSource` | IDamageSource | 伤害来源 |

继承自 ILivingEvent 的 `entityLivingBase`。

---

## EntityLivingDeathDropsEvent

> `import crafttweaker.event.EntityLivingDeathDropsEvent;`

实体死亡导致掉落物出现时触发。可取消以阻止掉落。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `drops` | IEntityItem[] | 掉落物列表 |
| `damageSource` | IDamageSource | 伤害来源 |
| `isRecentlyHit` | bool | 是否最近被攻击 |
| `lootingLevel` | int | 抢夺等级 |

方法：
- `event.addItem(IItemStack)` 添加物品到掉落列表
- `event.addItem(IEntityItem)` 添加物品实体到掉落列表

继承自 ILivingEvent 的 `entityLivingBase`。

```zenscript
event.drops = []; // 清空掉落
event.addItem(<minecraft:iron_ingot>); // 添加物品
```

---

## EntityLivingEquipmentChangeEvent

> `import crafttweaker.event.EntityLivingEquipmentChangeEvent;`

实体装备变化时触发（包括实体加入世界和被克隆时）。

实现接口：ILivingEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `newItem` | IItemStack | 新装备的物品 |
| `oldItem` | IItemStack | 之前的物品 |
| `slot` | IEntityEquipmentSlot | 变化的装备槽位 |

继承自 ILivingEvent 的 `entityLivingBase`。

---

## EntityLivingFallEvent

> `import crafttweaker.event.EntityLivingFallEvent;`

实体即将摔落时触发。可取消以阻止摔落。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `distance` | float | 摔落距离（可设置） |
| `damageMultiplier` | float | 伤害倍率（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

---

## EntityLivingHealEvent

> `import crafttweaker.event.EntityLivingHealEvent;`

实体即将被治疗时触发。可取消以阻止治疗。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `amount` | float | 治疗量（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

---

## EntityLivingHurtEvent

> `import crafttweaker.event.EntityLivingHurtEvent;`

实体即将受伤时触发。可取消以阻止受伤。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `amount` | float | 伤害量（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

---

## EntityLivingJumpEvent

> `import crafttweaker.event.EntityLivingJumpEvent;`

实体跳跃时触发。

实现接口：ILivingEvent

继承自 ILivingEvent 的 `entityLivingBase`。

---

## EntityLivingUpdateEvent

> `import crafttweaker.event.EntityLivingUpdateEvent;`

实体更新时触发。可取消以阻止实体更新。

实现接口：ILivingEvent, IEventCancelable

继承自 ILivingEvent 的 `entityLivingBase`。

---

## EntityMountEvent

> `import crafttweaker.event.EntityMountEvent;`

实体被骑乘或下骑时触发。可取消以阻止骑乘/下骑。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |
| `mountingEntity` | IEntity | 骑乘的实体 |
| `mountedEntity` | IEntity | 被骑乘的实体 |
| `isMounting` | boolean | 是否正在骑乘 |
| `isDismounting` | boolean | 是否正在下骑 |

继承自 ILivingEvent 的 `entityLivingBase`。

---

## EntityStruckByLightningEvent

> `import crafttweaker.event.EntityStruckByLightningEvent;`

实体即将被闪电击中时触发。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `lightning` | IEntity | 闪电实体 |

继承自 IEntityEvent 的 `entity`。

---

## EntityTravelToDimensionEvent

> `import crafttweaker.event.EntityTravelToDimensionEvent;`

实体即将前往另一个维度时触发。可取消以阻止传送。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `dimension` | int | 目标维度 ID |

继承自 IEntityEvent 的 `entity`。

注：`event.entity.dimension` 可获取传送前的维度。

---

## EnderTeleportEvent

> `import crafttweaker.event.EnderTeleportEvent;`

末影人/潜影贝传送或玩家使用末影珍珠传送时触发。可取消。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `targetX` | double | 目标 X 坐标（可设置） |
| `targetY` | double | 目标 Y 坐标（可设置） |
| `targetZ` | double | 目标 Z 坐标（可设置） |
| `attackDamage` | float | 传送伤害（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

---

## LivingExperienceDropEvent

> `import crafttweaker.event.LivingExperienceDropEvent;`

实体死亡掉落经验时触发。可修改经验量或取消以阻止掉落。

实现接口：IEventCancelable, ILivingEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 杀死实体的玩家 |
| `droppedExperience` | int | 掉落的经验值（可设置） |
| `originalExperience` | int | 原始经验值 |

继承自 ILivingEvent 的 `entityLivingBase`。

---

## LivingKnockBackEvent

> `import crafttweaker.event.LivingKnockBackEvent;`

实体被击退时触发。
