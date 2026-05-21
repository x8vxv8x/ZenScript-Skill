# 实体生命周期事件 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.event.*;`

实体加入世界、生成、死亡、死亡掉落、跨维度传送、末影传送等事件。

---

## API 列表

### EntityJoinWorldEvent（实体加入世界事件）

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

### EntityLivingSpawnEvent / EntityLivingExtendedSpawnEvent（实体生成事件）

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

### EntityLivingDeathEvent（实体死亡事件）

> `import crafttweaker.event.EntityLivingDeathEvent;`

实体即将死亡时触发。可取消以让实体存活。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `damageSource` | IDamageSource | 伤害来源 |

继承自 ILivingEvent 的 `entityLivingBase`。

### EntityLivingDeathDropsEvent（实体死亡掉落事件）

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

### EntityTravelToDimensionEvent（实体跨维度传送事件）

> `import crafttweaker.event.EntityTravelToDimensionEvent;`

实体即将前往另一个维度时触发。可取消以阻止传送。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `dimension` | int | 目标维度 ID |

继承自 IEntityEvent 的 `entity`。

注：`event.entity.dimension` 可获取传送前的维度。

### EnderTeleportEvent（末影人传送事件）

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
