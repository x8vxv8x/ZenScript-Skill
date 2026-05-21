# 实体其他事件 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.event.*;`

实体装备变化、摔落、更新、骑乘、雷击、掉落经验等事件。

---

## API 列表

### EntityLivingEquipmentChangeEvent（实体装备变化事件）

> `import crafttweaker.event.EntityLivingEquipmentChangeEvent;`

实体装备变化时触发（包括实体加入世界和被克隆时）。

实现接口：ILivingEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `newItem` | IItemStack | 新装备的物品 |
| `oldItem` | IItemStack | 之前的物品 |
| `slot` | IEntityEquipmentSlot | 变化的装备槽位 |

继承自 ILivingEvent 的 `entityLivingBase`。

### EntityLivingFallEvent（实体摔落事件）

> `import crafttweaker.event.EntityLivingFallEvent;`

实体即将摔落时触发。可取消以阻止摔落。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `distance` | float | 摔落距离（可设置） |
| `damageMultiplier` | float | 伤害倍率（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

### EntityLivingUpdateEvent（实体更新事件）

> `import crafttweaker.event.EntityLivingUpdateEvent;`

实体更新时触发。可取消以阻止实体更新。

实现接口：ILivingEvent, IEventCancelable

继承自 ILivingEvent 的 `entityLivingBase`。

### EntityMountEvent（实体骑乘事件）

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

### EntityStruckByLightningEvent（实体被雷击事件）

> `import crafttweaker.event.EntityStruckByLightningEvent;`

实体即将被闪电击中时触发。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `lightning` | IEntity | 闪电实体 |

继承自 IEntityEvent 的 `entity`。

### LivingExperienceDropEvent（生物死亡掉落经验事件）

> `import crafttweaker.event.LivingExperienceDropEvent;`

实体死亡掉落经验时触发。可修改经验量或取消以阻止掉落。

实现接口：IEventCancelable, ILivingEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 杀死实体的玩家 |
| `droppedExperience` | int | 掉落的经验值（可设置） |
| `originalExperience` | int | 原始经验值 |

继承自 ILivingEvent 的 `entityLivingBase`。
