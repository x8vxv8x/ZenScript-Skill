# Events API

## 概述

事件系统允许在游戏特定时间点执行自定义行为。通过全局 `events` 字段访问事件管理器。

```zenscript
events.onPlayerCrafted(function(event as crafttweaker.event.PlayerCraftedEvent){
    // 玩家合成时执行
});
```

**导入事件管理器**：`import crafttweaker.events.IEventManager;`

**清除所有事件处理器**：`events.clear();`

---

## 事件监听基础

```zenscript
events.on<EventName>(function(event as <EventType>) {
    // 事件处理代码
});
```

**重要**：必须将 event 强制转换为正确的事件类型，否则无法访问其 ZenGetter/ZenSetter。

---

## 重要提示

### `!world.remote` 保证服务端执行

MC 分为服务端和客户端。与存档相关的操作（召唤实体、修改方块等）必须在服务端执行。

```zenscript
events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if (!event.player.world.remote) {
        // 只在服务端执行
    }
});
```

**原因**: 单人游戏也有内置的服务端和客户端。不加 `!world.remote` 会导致事件执行两次（客户端一次，服务端一次），出现重复实体等问题。

---

## 事件接口

事件类通过实现接口来共享方法和属性。以下是所有事件接口。

### IBlockEvent

所有与方块相关的事件都实现此接口。

> `import crafttweaker.event.IBlockEvent;`

继承自 [IEventPositionable](#ieventpositionable)。

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |
| `blockState` | IBlockState | 方块状态 |
| `block` | IBlock | 方块对象 |
| `position` | IBlockPos | 方块位置 |
| `x` | int | X 坐标 |
| `y` | int | Y 坐标 |
| `z` | int | Z 坐标 |

### IEntityEvent

所有与实体相关的事件的基础接口。

| 属性 | 类型 | 说明 |
|------|------|------|
| `entity` | IEntity | 实体对象 |

### ILivingEvent

所有与生物相关的事件的基础接口。

| 属性 | 类型 | 说明 |
|------|------|------|
| `entityLivingBase` | IEntityLivingBase | 生物实体对象 |

### IPlayerEvent

所有与玩家相关的事件的基础接口。

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 玩家对象 |

### ITickEvent

所有 Tick 事件的基础接口。

| 属性 | 类型 | 说明 |
|------|------|------|
| `phase` | string | Tick 阶段，值为 `START` 或 `END` |
| `side` | string | 执行端，值为 `CLIENT` 或 `SERVER` |

### IEventCancelable

可取消事件的基础接口。

| 属性 | 类型 | 说明 |
|------|------|------|
| `canceled` | bool | 事件是否已取消（可设置） |

方法：`event.cancel()` 取消事件。

### IEventHasResult

拥有结果的事件的基础接口。

| 属性 | 类型 | 说明 |
|------|------|------|
| `result` | string | 事件结果，值为 `default`、`deny` 或 `allow` |

方法：
- `event.deny()` 设置结果为 `deny`
- `event.allow()` 设置结果为 `allow`
- `event.default()` 设置结果为 `default`

### IEventPositionable

拥有位置信息的事件的基础接口。

| 属性 | 类型 | 说明 |
|------|------|------|
| `position` | IBlockPos | 位置 |
| `x` | int | X 坐标 |
| `y` | int | Y 坐标 |
| `z` | int | Z 坐标 |

### IExplosionEvent

爆炸事件的基础接口。

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |
| `explosion` | IExplosion | 爆炸对象 |
| `position` | IBlockPos | 爆炸位置 |
| `x` | double | X 坐标 |
| `y` | double | Y 坐标 |
| `z` | double | Z 坐标 |

### IProjectileImpactEvent

投射物命中事件的基础接口。

### IMinecartEvent

矿车事件的基础接口。

### IPotionBrewEvent

药水酿造事件的基础接口。

### IProcessableEvent

可处理事件的基础接口。

---

## 完整事件列表

下表列出所有可用的 ZenMethod 和对应的事件类。

| ZenMethod | 事件类 | 说明 |
|-----------|--------|------|
| `onAllowDespawn` | EntityLivingSpawnEvent | 允许实体消失 |
| `onAnimalTame` | AnimalTameEvent | 动物驯服 |
| `onArrowLoose` | ArrowLooseEvent | 射箭（松开弓弦） |
| `onArrowNock` | ArrowNockEvent | 搭箭（开始拉弓） |
| `onBlockBreak` | BlockBreakEvent | 方块被破坏 |
| `onBlockHarvestDrops` | BlockHarvestDrops | 方块破坏掉落 |
| `onBlockNeighborNotify` | BlockNeighborNotifyEvent | 方块邻居通知（物理更新） |
| `onBlockPlace` | BlockPlaceEvent | 方块放置 |
| `onCheckSpawn` | EntityLivingExtendedSpawnEvent | 检查实体生成 |
| `onClientTick` | ClientTickEvent | 客户端 Tick |
| `onCommand` | CommandEvent | 命令执行 |
| `onCriticalHit` | CriticalHitEvent | 暴击判定 |
| `onCropGrowPost` | CropGrowPostEvent | 作物生长后 |
| `onCropGrowPre` | CropGrowPreEvent | 作物生长前 |
| `onEnchantmentLevelSet` | EnchantmentLevelSetEvent | 附魔台等级生成 |
| `onEnderTeleport` | EnderTeleportEvent | 末影人传送/末影珍珠传送 |
| `onEntityJoinWorld` | EntityJoinWorldEvent | 实体加入世界 |
| `onEntityLivingAttacked` | EntityLivingAttackedEvent | 实体被攻击 |
| `onEntityLivingDamage` | EntityLivingDamageEvent | 实体受伤（最终伤害） |
| `onEntityLivingDeath` | EntityLivingDeathEvent | 实体死亡 |
| `onEntityLivingDeathDrops` | EntityLivingDeathDropsEvent | 实体死亡掉落 |
| `onEntityLivingEquipmentChange` | EntityLivingEquipmentChangeEvent | 实体装备变化 |
| `onEntityLivingFall` | EntityLivingFallEvent | 实体摔落 |
| `onEntityLivingHeal` | EntityLivingHealEvent | 实体回血 |
| `onEntityLivingHurt` | EntityLivingHurtEvent | 实体受伤 |
| `onEntityLivingJump` | EntityLivingJumpEvent | 实体跳跃 |
| `onEntityLivingUpdate` | EntityLivingUpdateEvent | 实体更新 |
| `onEntityLivingUseItem` | EntityLivingUseItemEvent.All | 实体使用物品（全部阶段） |
| `onEntityLivingUseItemFinish` | EntityLivingUseItemEvent.Finish | 实体完成使用物品 |
| `onEntityLivingUseItemStart` | EntityLivingUseItemEvent.Start | 实体开始使用物品 |
| `onEntityLivingUseItemStop` | EntityLivingUseItemEvent.Stop | 实体停止使用物品 |
| `onEntityLivingUseItemTick` | EntityLivingUseItemEvent.Tick | 实体使用物品 Tick |
| `onEntityMount` | EntityMountEvent | 实体骑乘/下骑 |
| `onEntityStruckByLightning` | EntityStruckByLightningEvent | 实体被雷击 |
| `onEntityTravelToDimension` | EntityTravelToDimensionEvent | 实体跨维度传送 |
| `onExplosionDetonate` | ExplosionDetonateEvent | 爆炸引爆 |
| `onExplosionStart` | ExplosionStartEvent | 爆炸开始 |
| `onFarmlandTrample` | FarmlandTrampleEvent | 农田被踩踏 |
| `onItemExpire` | ItemExpireEvent | 物品实体过期 |
| `onItemFished` | ItemFishedEvent | 钓鱼获得物品 |
| `onItemToss` | ItemTossEvent | 丢弃物品 |
| `onLivingDestroyBlock` | LivingDestroyBlockEvent | 生物破坏方块（凋灵/末影龙/僵尸） |
| `onLivingExperienceDrop` | LivingExperienceDropEvent | 生物死亡掉落经验 |
| `onLivingKnockBack` | LivingKnockBackEvent | 生物被击退 |
| `onLootingLevel` | LootingLevelEvent | 抢夺等级判定 |
| `onMinecartCollision` | MinecartCollisionEvent | 矿车碰撞 |
| `onMinecartInteract` | MinecartInteractEvent | 矿车交互 |
| `onMobGriefing` | MobGriefingEvent | 生物破坏（苦力怕爆炸等） |
| `onPlayerAdvancement` | PlayerAdvancementEvent | 玩家获得进度 |
| `onPlayerAnvilRepair` | PlayerAnvilRepairEvent | 玩家铁砧修复 |
| `onPlayerAnvilUpdate` | PlayerAnvilUpdateEvent | 玩家铁砧更新 |
| `onPlayerAttackEntity` | PlayerAttackEntityEvent | 玩家攻击实体 |
| `onPlayerBonemeal` | PlayerBonemealEvent | 玩家使用骨粉 |
| `onPlayerBreakSpeed` | PlayerBreakSpeed | 玩家挖掘速度 |
| `onPlayerBrewedPotion` | PlayerBrewedPotion | 玩家酿造药水 |
| `onPlayerChangedDimension` | PlayerChangedDimensionEvent | 玩家切换维度 |
| `onPlayerClone` | PlayerCloneEvent | 玩家克隆（重生时） |
| `onPlayerCloseContainer` | PlayerCloseContainerEvent | 玩家关闭容器 |
| `onPlayerCrafted` | PlayerCraftedEvent | 玩家合成物品 |
| `onPlayerDeathDrops` | PlayerDeathDropsEvent | 玩家死亡掉落 |
| `onPlayerDestroyItem` | PlayerDestroyItem | 玩家物品损坏 |
| `onPlayerFillBucket` | PlayerFillBucketEvent | 玩家填充桶 |
| `onPlayerInteract` | PlayerInteractEvent | 玩家交互 |
| `onPlayerInteractBlock` | PlayerInteractBlockEvent | 玩家右键方块 |
| `onPlayerInteractEntity` | PlayerInteractEntityEvent | 玩家右键实体 |
| `onPlayerItemPickup` | PlayerItemPickupEvent | 玩家拾取物品 |
| `onPlayerLeftClickBlock` | PlayerLeftClickBlockEvent | 玩家左键方块 |
| `onPlayerLoggedIn` | PlayerLoggedInEvent | 玩家登录 |
| `onPlayerLoggedOut` | PlayerLoggedOutEvent | 玩家登出 |
| `onPlayerOpenContainer` | PlayerOpenContainerEvent | 玩家打开容器 |
| `onPlayerPickupItem` | PlayerPickupItemEvent | 玩家拾取物品实体 |
| `onPlayerPickupXp` | PlayerPickupXpEvent | 玩家拾取经验 |
| `onPlayerRespawn` | PlayerRespawnEvent | 玩家重生 |
| `onPlayerRightClickItem` | PlayerRightClickItemEvent | 玩家右键物品 |
| `onPlayerSetSpawn` | PlayerSetSpawn | 玩家设置重生点 |
| `onPlayerSleepInBed` | PlayerSleepInBedEvent | 玩家睡觉 |
| `onPlayerSmelted` | PlayerSmeltedEvent | 玩家熔炼物品 |
| `onPlayerTick` | PlayerTickEvent | 玩家 Tick |
| `onPlayerUseHoe` | PlayerUseHoeEvent | 玩家使用锄 |
| `onPlayerVisibility` | PlayerVisibilityEvent | 玩家可见性 |
| `onPortalSpawn` | PortalSpawnEvent | 传送门生成 |
| `onPotionBrewPost` | PotionBrewPostEvent | 药水酿造后 |
| `onPotionBrewPre` | PotionBrewPreEvent | 药水酿造前 |
| `onProjectileImpactArrow` | ProjectileImpactArrowEvent | 箭矢命中 |
| `onProjectileImpactFireball` | ProjectileImpactFireballEvent | 火球命中 |
| `onProjectileImpactThrowable` | ProjectileImpactThrowableEvent | 投掷物命中 |
| `onRenderTick` | RenderTickEvent | 渲染 Tick |
| `onServerTick` | ServerTickEvent | 服务端 Tick |
| `onSleepingLocationCheck` | SleepingLocationCheckEvent | 睡觉位置检查 |
| `onSleepingTimeCheck` | SleepingTimeCheckEvent | 睡觉时间检查 |
| `onSpecialSpawn` | EntityLivingExtendedSpawnEvent | 特殊生成（刷怪笼等） |
| `onWorldTick` | WorldTickEvent | 世界 Tick |

---

## 事件详细说明

### 方块事件

#### BlockBreakEvent

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

#### BlockHarvestDropsEvent

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

#### BlockNeighborNotifyEvent

> `import crafttweaker.event.BlockNeighborNotifyEvent;`

方块发生物理更新时触发（类似 BUD 开关）。仅在服务端调用。

实现接口：IEventCancelable, IBlockEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `forceRedstoneUpdate` | bool | 是否在 setBlock 调用时强制红石更新 |
| `notifiedSides` | IFacing[] | 接收更新的方向列表 |

继承自 IBlockEvent 的 `world`、`blockState`、`block`、`position`、`x`、`y`、`z`。

#### BlockPlaceEvent

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

#### FarmlandTrampleEvent

> `import crafttweaker.event.FarmlandTrampleEvent;`

农田被踩踏时触发。可取消以阻止踩踏。

实现接口：IEventCancelable, IBlockEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `entity` | IEntity | 踩踏农田的实体 |
| `fallDistance` | float | 踩踏前的摔落距离 |

继承自 IBlockEvent 的 `world`、`blockState`、`block`、`position`、`x`、`y`、`z`。

#### CropGrowPostEvent

> `import crafttweaker.event.CropGrowPostEvent;`

作物成功生长后触发。不可取消，仅作为通知。

实现接口：IBlockEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `originalBlockState` | IBlockState | 生长前的方块状态 |
| `originalBlock` | IBlock | 生长前的方块 |

继承自 IBlockEvent 的 `world`、`blockState`、`block`、`position`、`x`、`y`、`z`。

#### CropGrowPreEvent

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

#### LivingDestroyBlockEvent

> `import crafttweaker.event.LivingDestroyBlockEvent;`

凋灵、末影龙尝试破坏方块或僵尸尝试破门时触发。可取消以阻止破坏。

实现接口：IEventPositionable, IEventCancelable, ILivingEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `state` | IBlockState | 被破坏的方块状态 |

继承自 ILivingEvent 的 `entityLivingBase`；继承自 IEventPositionable 的 `position`、`x`、`y`、`z`。

#### PortalSpawnEvent

> `import crafttweaker.event.PortalSpawnEvent;`

传送门生成时触发。

---

### 实体事件

#### EntityJoinWorldEvent

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

#### EntityLivingSpawnEvent / EntityLivingExtendedSpawnEvent

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

#### EntityLivingAttackedEvent

> `import crafttweaker.event.EntityLivingAttackedEvent;`

实体被攻击时触发。可取消以阻止受伤。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `damageSource` | IDamageSource | 伤害来源 |
| `amount` | float | 伤害值 |

继承自 ILivingEvent 的 `entityLivingBase`。

#### EntityLivingDamageEvent

> `import crafttweaker.event.EntityLivingDamageEvent;`

实体受伤前触发。此时护甲、药水、吸收等修正已应用，这是**最终伤害值**。注意：护甲耐久和吸收心等资源已被消耗，取消后**不会恢复**。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `damageSource` | IDamageSource | 伤害来源 |
| `amount` | float | 最终伤害值（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

#### EntityLivingDeathEvent

> `import crafttweaker.event.EntityLivingDeathEvent;`

实体即将死亡时触发。可取消以让实体存活。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `damageSource` | IDamageSource | 伤害来源 |

继承自 ILivingEvent 的 `entityLivingBase`。

#### EntityLivingDeathDropsEvent

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

#### EntityLivingEquipmentChangeEvent

> `import crafttweaker.event.EntityLivingEquipmentChangeEvent;`

实体装备变化时触发（包括实体加入世界和被克隆时）。

实现接口：ILivingEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `newItem` | IItemStack | 新装备的物品 |
| `oldItem` | IItemStack | 之前的物品 |
| `slot` | IEntityEquipmentSlot | 变化的装备槽位 |

继承自 ILivingEvent 的 `entityLivingBase`。

#### EntityLivingFallEvent

> `import crafttweaker.event.EntityLivingFallEvent;`

实体即将摔落时触发。可取消以阻止摔落。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `distance` | float | 摔落距离（可设置） |
| `damageMultiplier` | float | 伤害倍率（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

#### EntityLivingHealEvent

> `import crafttweaker.event.EntityLivingHealEvent;`

实体即将被治疗时触发。可取消以阻止治疗。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `amount` | float | 治疗量（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

#### EntityLivingHurtEvent

> `import crafttweaker.event.EntityLivingHurtEvent;`

实体即将受伤时触发。可取消以阻止受伤。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `amount` | float | 伤害量（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

#### EntityLivingJumpEvent

> `import crafttweaker.event.EntityLivingJumpEvent;`

实体跳跃时触发。

实现接口：ILivingEvent

继承自 ILivingEvent 的 `entityLivingBase`。

#### EntityLivingUpdateEvent

> `import crafttweaker.event.EntityLivingUpdateEvent;`

实体更新时触发。可取消以阻止实体更新。

实现接口：ILivingEvent, IEventCancelable

继承自 ILivingEvent 的 `entityLivingBase`。

#### EntityMountEvent

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

#### EntityStruckByLightningEvent

> `import crafttweaker.event.EntityStruckByLightningEvent;`

实体即将被闪电击中时触发。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `lightning` | IEntity | 闪电实体 |

继承自 IEntityEvent 的 `entity`。

#### EntityTravelToDimensionEvent

> `import crafttweaker.event.EntityTravelToDimensionEvent;`

实体即将前往另一个维度时触发。可取消以阻止传送。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `dimension` | int | 目标维度 ID |

继承自 IEntityEvent 的 `entity`。

注：`event.entity.dimension` 可获取传送前的维度。

#### EnderTeleportEvent

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

#### LivingExperienceDropEvent

> `import crafttweaker.event.LivingExperienceDropEvent;`

实体死亡掉落经验时触发。可修改经验量或取消以阻止掉落。

实现接口：IEventCancelable, ILivingEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 杀死实体的玩家 |
| `droppedExperience` | int | 掉落的经验值（可设置） |
| `originalExperience` | int | 原始经验值 |

继承自 ILivingEvent 的 `entityLivingBase`。

#### LivingKnockBackEvent

> `import crafttweaker.event.LivingKnockBackEvent;`

实体被击退时触发。

---

### 玩家事件

#### PlayerCraftedEvent

> `import crafttweaker.event.PlayerCraftedEvent;`

玩家合成物品时触发。

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 合成的玩家 |
| `output` | IItemStack | 合成结果 |
| `inventory` | ICraftingInventory | 合成网格 |

#### PlayerSmeltedEvent

> `import crafttweaker.event.PlayerSmeltedEvent;`

玩家从熔炉取出物品时触发。

#### PlayerLoggedInEvent

> `import crafttweaker.event.PlayerLoggedInEvent;`

玩家登录时触发。

#### PlayerLoggedOutEvent

> `import crafttweaker.event.PlayerLoggedOutEvent;`

玩家登出时触发。

#### PlayerRespawnEvent

> `import crafttweaker.event.PlayerRespawnEvent;`

玩家重生时触发。

#### PlayerChangedDimensionEvent

> `import crafttweaker.event.PlayerChangedDimensionEvent;`

玩家切换维度时触发。

#### PlayerCloneEvent

> `import crafttweaker.event.PlayerCloneEvent;`

玩家被克隆时触发（如从末地返回）。

#### PlayerTickEvent

> `import crafttweaker.event.PlayerTickEvent;`

玩家 Tick 时触发。

#### PlayerAttackEntityEvent

> `import crafttweaker.event.PlayerAttackEntityEvent;`

玩家攻击实体时触发。

#### PlayerInteractEvent

> `import crafttweaker.event.PlayerInteractEvent;`

玩家交互时触发。

#### PlayerInteractBlockEvent

> `import crafttweaker.event.PlayerInteractBlockEvent;`

玩家右键方块时触发。

#### PlayerInteractEntityEvent

> `import crafttweaker.event.PlayerInteractEntityEvent;`

玩家右键实体时触发。

#### PlayerRightClickItemEvent

> `import crafttweaker.event.PlayerRightClickItemEvent;`

玩家右键物品时触发。

#### PlayerLeftClickBlockEvent

> `import crafttweaker.event.PlayerLeftClickBlockEvent;`

玩家左键方块时触发。

#### PlayerDeathDropsEvent

> `import crafttweaker.event.PlayerDeathDropsEvent;`

玩家死亡掉落时触发。

#### PlayerDestroyItem

> `import crafttweaker.event.PlayerDestroyItem;`

玩家物品损坏时触发。

#### PlayerFillBucketEvent

> `import crafttweaker.event.PlayerFillBucketEvent;`

玩家填充桶时触发。

#### PlayerItemPickupEvent

> `import crafttweaker.event.PlayerItemPickupEvent;`

玩家拾取物品时触发。

#### PlayerPickupItemEvent

> `import crafttweaker.event.PlayerPickupItemEvent;`

玩家拾取物品实体时触发。

#### PlayerPickupXpEvent

> `import crafttweaker.event.PlayerPickupXpEvent;`

玩家拾取经验时触发。

#### PlayerOpenContainerEvent

> `import crafttweaker.event.PlayerOpenContainerEvent;`

玩家打开容器时触发。

#### PlayerCloseContainerEvent

> `import crafttweaker.event.PlayerCloseContainerEvent;`

玩家关闭容器时触发。

#### PlayerBonemealEvent

> `import crafttweaker.event.PlayerBonemealEvent;`

玩家使用骨粉时触发。

#### PlayerUseHoeEvent

> `import crafttweaker.event.PlayerUseHoeEvent;`

玩家使用锄头时触发。

#### PlayerBreakSpeed

> `import crafttweaker.event.PlayerBreakSpeed;`

玩家挖掘速度计算时触发。

#### PlayerBrewedPotion

> `import crafttweaker.event.PlayerBrewedPotion;`

玩家酿造药水时触发。

#### PlayerSleepInBedEvent

> `import crafttweaker.event.PlayerSleepInBedEvent;`

玩家尝试睡觉时触发。

#### PlayerAdvancementEvent

> `import crafttweaker.event.PlayerAdvancementEvent;`

玩家获得进度时触发。

#### PlayerAnvilRepairEvent

> `import crafttweaker.event.PlayerAnvilRepairEvent;`

玩家在铁砧修复物品时触发。

#### PlayerAnvilUpdateEvent

> `import crafttweaker.event.PlayerAnvilUpdateEvent;`

玩家在铁砧更新物品时触发。

#### PlayerSetSpawn

> `import crafttweaker.event.PlayerSetSpawn;`

玩家设置重生点时触发。

#### PlayerVisibilityEvent

> `import crafttweaker.event.PlayerVisibilityEvent;`

玩家可见性变化时触发。

---

### 箭矢事件

#### ArrowLooseEvent

> `import crafttweaker.event.ArrowLooseEvent;`

玩家松开弓弦（射箭）时触发。可取消。

实现接口：IPlayerEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `bow` | IItemStack | 弓 |
| `charge` | int | 蓄力值（可设置） |
| `world` | IWorld | 世界对象 |
| `player` | IPlayer | 射箭的玩家 |

#### ArrowNockEvent

> `import crafttweaker.event.ArrowNockEvent;`

玩家开始拉弓（搭箭）时触发。

实现接口：IPlayerEvent, IEventHasResult

| 属性 | 类型 | 说明 |
|------|------|------|
| `bow` | IItemStack | 弓 |
| `hand` | string | 使用的手 |
| `player` | IPlayer | 玩家 |
| `result` | string | 事件结果 |

方法：
- `event.deny()` / `event.allow()` / `event.default()`

---

### 附魔事件

#### EnchantmentLevelSetEvent

> `import crafttweaker.event.EnchantmentLevelSetEvent;`

附魔台生成三个附魔等级时触发。

实现接口：IEventPositionable

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |
| `enchantRow` | int | 附魔台行号（1-3） |
| `power` | int | 书架总能量 |
| `item` | IItemStack | 被附魔的物品 |
| `originalLevel` | int | 原始附魔等级 |
| `level` | int | 附魔等级（可设置，0-30） |

继承自 IEventPositionable 的 `position`、`x`、`y`、`z`。

---

### 命令事件

#### CommandEvent

> `import crafttweaker.event.CommandEvent;`

命令执行时触发。可取消。

实现接口：IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `commandSender` | ICommandSender | 命令发送者 |
| `command` | ICommand | 命令对象 |
| `parameters` | string[] | 命令参数（可设置） |

```zenscript
events.onCommand(function(event as CommandEvent) {
    if (event.command.name == "gamemode" && (event.parameters in "creative")) {
        event.cancel();
    }
});
```

---

### 暴击事件

#### CriticalHitEvent

> `import crafttweaker.event.CriticalHitEvent;`

玩家攻击时暴击判定触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `target` | IEntity | 攻击目标 |
| `oldDamageModifier` | float | 原始伤害倍率 |
| `damageModifier` | float | 伤害倍率（可设置） |
| `isVanillaCrit` | boolean | 是否原版暴击 |
| `player` | IPlayer | 攻击的玩家 |

方法：
- `event.deny()` 阻止暴击
- `event.allow()` 强制暴击
- `event.default()` 使用原版行为

---

### 爆炸事件

#### ExplosionStartEvent

> `import crafttweaker.event.ExplosionStartEvent;`

爆炸即将开始时触发。可取消以阻止爆炸。

实现接口：IExplosionEvent, IEventCancelable

继承自 IExplosionEvent 的 `world`、`explosion`、`position`、`x`、`y`、`z`。

#### ExplosionDetonateEvent

> `import crafttweaker.event.ExplosionDetonateEvent;`

爆炸引爆时触发。不可取消。

实现接口：IExplosionEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `affectedEntities` | IEntity[] | 受影响的实体列表 |
| `affectedPositions` | IBlockPos[] | 受影响的位置列表 |

继承自 IExplosionEvent 的 `world`、`explosion`、`position`、`x`、`y`、`z`。

---

### Tick 事件

#### WorldTickEvent

> `import crafttweaker.event.WorldTickEvent;`

每个世界每 Tick 触发（客户端和服务端都会触发）。

实现接口：ITickEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 世界对象 |
| `phase` | string | Tick 阶段，值为 `START` 或 `END` |
| `side` | string | 执行端，值为 `CLIENT` 或 `SERVER` |

#### ClientTickEvent

> `import crafttweaker.event.ClientTickEvent;`

客户端每 Tick 触发。

实现接口：ITickEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `phase` | string | Tick 阶段，值为 `START` 或 `END` |
| `side` | string | 执行端，值为 `CLIENT` 或 `SERVER` |

#### ServerTickEvent

> `import crafttweaker.event.ServerTickEvent;`

服务端每 Tick 触发。

实现接口：ITickEvent

#### RenderTickEvent

> `import crafttweaker.event.RenderTickEvent;`

渲染 Tick 时触发。

实现接口：ITickEvent

---

### 物品事件

#### ItemExpireEvent

> `import crafttweaker.event.ItemExpireEvent;`

物品实体达到最大寿命时触发。可取消以阻止物品消失，取消后会将 `extraLife` 添加到物品寿命中。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IEntityItem | 物品实体 |
| `extraLife` | int | 额外寿命（可设置） |

继承自 IEntityEvent 的 `entity`。

#### ItemFishedEvent

> `import crafttweaker.event.ItemFishedEvent;`

玩家即将钓到物品时触发。取消后玩家不会收到物品，但鱼竿仍会消耗耐久。

实现接口：IPlayerEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `damage` | int | 鱼竿伤害 |
| `additionalDamage` | int | 额外鱼竿伤害（可设置） |
| `drops` | IItemStack[] | 将钓到的物品列表（不可修改） |
| `fishHook` | IEntityFishHook | 鱼钩实体 |
| `player` | IPlayer | 钓鱼的玩家 |

#### ItemTossEvent

> `import crafttweaker.event.ItemTossEvent;`

玩家从背包丢弃物品时触发。取消后物品不会进入世界（物品会被删除）。

实现接口：IEntityEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IEntityItem | 物品实体 |
| `player` | IPlayer | 丢弃物品的玩家 |

继承自 IEntityEvent 的 `entity`。

---

### 使用物品事件

#### EntityLivingUseItemEvent（系列事件）

> `import crafttweaker.event.EntityLivingUseItemEvent.All;`
> `import crafttweaker.event.EntityLivingUseItemEvent.Start;`
> `import crafttweaker.event.EntityLivingUseItemEvent.Tick;`
> `import crafttweaker.event.EntityLivingUseItemEvent.Stop;`
> `import crafttweaker.event.EntityLivingUseItemEvent.Finish;`

实体使用物品时触发。分为 5 个子事件（All 包含所有阶段，其他 4 个为特定阶段）。

实现接口：ILivingEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 使用物品的玩家（如果玩家） |
| `isPlayer` | bool | 是否为玩家 |
| `item` | IItemStack | 被使用的物品 |
| `duration` | int | 使用持续时间（可设置） |

继承自 ILivingEvent 的 `entityLivingBase`。

---

### 药水酿造事件

#### PotionBrewPreEvent

> `import crafttweaker.event.PotionBrewPreEvent;`

药水酿造前触发。

#### PotionBrewPostEvent

> `import crafttweaker.event.PotionBrewPostEvent;`

药水酿造后触发。

---

### 投射物命中事件

#### ProjectileImpactArrowEvent

> `import crafttweaker.event.ProjectileImpactArrowEvent;`

箭矢命中时触发。

#### ProjectileImpactFireballEvent

> `import crafttweaker.event.ProjectileImpactFireballEvent;`

火球命中时触发。

#### ProjectileImpactThrowableEvent

> `import crafttweaker.event.ProjectileImpactThrowableEvent;`

投掷物（如雪球、末影珍珠）命中时触发。

---

### 矿车事件

#### MinecartCollisionEvent

> `import crafttweaker.event.MinecartCollisionEvent;`

矿车碰撞时触发。

#### MinecartInteractEvent

> `import crafttweaker.event.MinecartInteractEvent;`

玩家与矿车交互时触发。

---

### 睡觉事件

#### SleepingTimeCheckEvent

> `import crafttweaker.event.SleepingTimeCheckEvent;`

睡觉时间检查时触发。

#### SleepingLocationCheckEvent

> `import crafttweaker.event.SleepingLocationCheckEvent;`

睡觉位置检查时触发。

---

### 其他事件

#### AnimalTameEvent

> `import crafttweaker.event.AnimalTameEvent;`

动物即将被驯服时触发。可取消以阻止驯服。

实现接口：IPlayerEvent, IEventCancelable

| 属性 | 类型 | 说明 |
|------|------|------|
| `animal` | IEntityAnimal | 被驯服的动物 |
| `player` | IPlayer | 驯服的玩家 |

#### MobGriefingEvent

> `import crafttweaker.event.MobGriefingEvent;`

生物破坏方块（如苦力怕爆炸、末影人搬方块等）时触发。

#### LootingLevelEvent

> `import crafttweaker.event.LootingLevelEvent;`

抢夺等级判定时触发。

---

## ZenUtils 扩展（需安装 ZenUtils）

> `import mods.zenutils.event.*;`

### EntityRemoveEvent

> `import mods.zenutils.event.EntityRemoveEvent;`

当实体从世界中移除时触发。

### EntityItemDeathEvent

> `import mods.zenutils.event.EntityItemDeathEvent;`
> 版本要求: 1.13.9+

当物品实体被岩浆、火焰、虚空等销毁时触发（不包括漏斗等传输设备）。

| 属性 | 返回 | 说明 |
|------|------|------|
| `item` | IEntityItem | 被销毁的物品实体 |
| `damageSource` | IDamageSource | 销毁原因 |

```zenscript
events.onEntityItemDeath(function(event as EntityItemDeathEvent) {
    print("物品 " ~ event.item.name ~ " 被销毁了");
});
```

### EntityItemFallEvent

当物品实体掉落时触发。具体属性参见 wiki。

### WorldEvents

世界相关事件。具体事件列表参见 wiki。

### GenericEventManager

通用事件管理器，支持注册自定义事件。具体用法参见 wiki。
