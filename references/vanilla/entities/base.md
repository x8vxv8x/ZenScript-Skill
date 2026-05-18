# 实体基础类型 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.entity.IEntity;`、`import crafttweaker.entity.IEntityLivingBase;`、`import crafttweaker.entity.IEntityLiving;`、`import crafttweaker.entity.Attribute;`、`import crafttweaker.entity.AttributeInstance;`、`import crafttweaker.entity.AttributeModifier;`

实体基础类型 API，包括 IEntity、IEntityLivingBase、IEntityLiving 及属性系统。

---

## API 列表

### IEntity（实体）

> `import crafttweaker.entity.IEntity;`

IEntity 继承 ICommandSender，因此 ICommandSender 的所有方法也可用于 IEntity 对象。

ICommandSender 派生方法：`entity.displayName`、`entity.position`、`entity.world`、`entity.server`、`entity.sendMessage(String text)`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `air` | int | 剩余空气值 |
| `alive` | boolean | 是否存活 |
| `alwaysRenderNameTag` | boolean | 是否始终渲染名称标签 |
| `armorInventory` | List<IItemStack> | 盔甲物品列表 |
| `canBeAttackedWithItem` | boolean | 是否可被物品攻击 |
| `canBeCollidedWith` | boolean | 是否可被碰撞 |
| `canPassengerSteer` | boolean | 乘客是否可操控 |
| `canRiderInteract` | boolean | 骑乘者是否可交互 |
| `controllingPassenger` | IEntity | 控制乘客 |
| `customName` | string | 自定义名称 |
| `definition` | IEntityDefinition | 实体定义 |
| `dimension` | int | 维度 ID |
| `doesTriggerPressurePlate` | boolean | 是否触发压力板 |
| `equipmentAndArmor` | List<IItemStack> | 装备和盔甲物品列表 |
| `eyeHeight` | float | 眼睛高度 |
| `hasCustomName` | boolean | 是否有自定义名称 |
| `hasNoGravity` | boolean | 是否无重力 |
| `heldEquipment` | List<IItemStack> | 手持物品列表 |
| `id` | int | 实体 ID |
| `immuneToFire` | boolean | 是否免疫火焰 |
| `isBeingRidden` | boolean | 是否被骑乘 |
| `isBoss` | boolean | 是否为 Boss |
| `isBurning` | boolean | 是否着火 |
| `isGlowing` | boolean | 是否发光 |
| `isImmuneToExplosions` | boolean | 是否免疫爆炸 |
| `isInLava` | boolean | 是否在岩浆中 |
| `isInsideOpaqueBlock` | boolean | 是否在不透明方块内 |
| `isInvisible` | boolean | 是否隐身 |
| `isInvulnerable` | boolean | 是否无敌 |
| `isInWater` | boolean | 是否在水中 |
| `isLightningbolt` | boolean | 是否为闪电 |
| `isOutsideBorder` | boolean | 是否在世界边界外 |
| `isOverWater` | boolean | 是否在水面上方 |
| `isPushedByWater` | boolean | 是否被水推动 |
| `isRiding` | boolean | 是否骑乘 |
| `isSilent` | boolean | 是否静音 |
| `isSneaking` | boolean | 是否潜行 |
| `isSprinting` | boolean | 是否冲刺 |
| `lowestRidingEntity` | IEntity | 最底层骑乘实体 |
| `maxFallHeight` | int | 最大掉落高度 |
| `maxInPortalTime` | int | 最大传送门停留时间 |
| `nbt` | IData | NBT 数据 |
| `onGround` | boolean | 是否在地面上 |
| `parts` | IEntity[] | 实体部件数组 |
| `passengers` | List<IEntity> | 乘客列表 |
| `passengersRecursive` | List<IEntity> | 递归乘客列表 |
| `portalCooldown` | int | 传送门冷却时间 |
| `position3f` | Position3f | 精确位置 |
| `ridingEntity` | IEntity | 骑乘的实体 |
| `shouldRiderSit` | boolean | 骑乘者是否坐下 |
| `tags` | List<string> | 标签列表 |
| `team` | ITeam | 所属队伍 |
| `wet` | boolean | 是否潮湿 |
| `world` | IWorld | 所在世界 |
| `x` / `y` / `z` | double | 坐标 |
| `motionX` / `motionY` / `motionZ` | double | 速度 |
| `posX` / `posY` / `posZ` | double | 精确坐标 |
| `rotationYaw` | float | 偏航角 |
| `rotationPitch` | float | 俯仰角 |
| `lookingDirection` | IVector3d | 视线方向 |
| `horizontalFacing` | IFacing | 水平朝向 |
| `updateBlocked` | boolean | 是否阻止更新 |
| `inPortal` | boolean | 是否在传送门中 |
| `portalCounter` | int | 传送门计数器 |
| `lastPortalVec` | IVector3d | 上次传送门向量 |
| `lastPortalPos` | IBlockPos | 上次传送门位置 |
| `lastPortalDirection` | IFacing | 上次传送门方向 |

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `air` | int | 设置剩余空气值 |
| `alwaysRenderNameTag` | boolean | 设置是否始终渲染名称标签 |
| `customName` | string | 设置自定义名称 |
| `dimension` | int | 设置维度 ID |
| `fire` | int | 设置着火时间 |
| `hasNoGravity` | boolean | 设置无重力 |
| `id` | int | 设置实体 ID |
| `isGlowing` | boolean | 设置发光 |
| `isInvisible` | boolean | 设置隐身 |
| `isOutsideBorder` | boolean | 设置是否在世界边界外 |
| `isSilent` | boolean | 设置静音 |
| `isSneaking` | boolean | 设置潜行 |
| `isSprinting` | boolean | 设置冲刺 |
| `position` | IBlockPos | 设置位置 |
| `rotationYaw` | float | 设置偏航角 |
| `rotationPitch` | float | 设置俯仰角 |
| `motionX` / `motionY` / `motionZ` | double | 设置速度 |
| `posX` / `posY` / `posZ` | double | 设置精确坐标 |
| `nbt` | IData | 设置 NBT 数据 |
| `team` | ITeam | 设置所属队伍 |
| `updateBlocked` | boolean | 设置是否阻止更新 |
| `inPortal` | boolean | 设置是否在传送门中 |
| `portalCounter` | int | 设置传送门计数器 |
| `lastPortalVec` | IVector3d | 设置上次传送门向量 |
| `lastPortalPos` | IBlockPos | 设置上次传送门位置 |
| `lastPortalDirection` | IFacing | 设置上次传送门方向 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.attackEntityFrom(IDamageSource, float)` | boolean | 对实体造成伤害 |
| `.canTrample(IWorld, IBlockDefinition, IBlockPos, float)` | boolean | 检查是否可以踩踏 |
| `.isInsideOfMaterial(IMaterial)` | boolean | 检查是否在指定材质内 |
| `.getDistanceSqToEntity(IEntity)` | double | 获取到指定实体的距离平方 |
| `.getPickedResult()` | IItemStack | 获取拾取结果物品 |
| `.addTag(String)` | void | 添加标签 |
| `.extinguish()` | void | 熄灭火焰 |
| `.onEntityUpdate()` | void | 实体更新回调 |
| `.onKillCommand()` | void | 执行 kill 命令回调 |
| `.onUpdate()` | void | 更新回调 |
| `.removeTag(String)` | void | 移除标签 |
| `.setDead()` | void | 杀死实体 |
| `.spawnRunningParticles()` | void | 生成奔跑粒子效果 |
| `.removePassengers()` | void | 移除所有乘客 |
| `.dismountRidingEntity()` | void | 取消骑乘 |
| `.isOnSameTeam(IEntity)` | boolean | 检查是否在同一队伍 |
| `.setInWeb()` | void | 设为被蜘蛛网缠住 |
| `.doWaterSplashEffect()` | void | 执行水花效果 |
| `.isEntityEqual(IEntity)` | boolean | 检查实体是否相等 |
| `.isInvulnerableTo(IDamageSource)` | boolean | 检查是否对指定伤害来源无敌 |
| `.shouldRiderDismountInWater(IEntity)` | boolean | 检查骑乘者是否应在水中下马 |
| `.isPassenger(IEntity)` | boolean | 检查是否为乘客 |
| `.isRidingSameEntity(IEntity)` | boolean | 检查是否骑乘同一实体 |
| `.getRayTrace(double, float, @Optional boolean, @Optional boolean, @Optional boolean)` | IRayTraceResult | 射线追踪 |

### IEntityLivingBase（有生命实体）

> `import crafttweaker.entity.IEntityLivingBase;`

有生命实体，包括怪物、动物和玩家。继承 IEntity。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `activeHand` | IEntityEquipmentSlot | 当前激活的手部装备槽 |
| `activeItemStack` | IItemStack | 当前激活的物品 |
| `activePotionEffects` | List<IPotionEffect> | 当前激活的药水效果列表 |
| `AIMovementSpeed` | float | AI 移动速度 |
| `arrowsInEntity` | int | 插在实体上的箭数量 |
| `attackingEntity` | IEntityLivingBase | 正在攻击此实体的实体 |
| `canBreatheUnderwater` | boolean | 是否能在水下呼吸 |
| `health` | float | 当前生命值 |
| `isActiveItemStackBlocking` | boolean | 当前激活物品是否在格挡 |
| `isChild` | boolean | 是否为幼年 |
| `isElytraFlying` | boolean | 是否在使用鞘翅飞行 |
| `isOnLadder` | boolean | 是否在梯子上 |
| `isUndead` | boolean | 是否为亡灵 |
| `lastAttackedEntity` | IEntityLivingBase | 上次攻击的实体 |
| `lastAttackedEntityTime` | int | 上次攻击实体的时间 |
| `lastDamageSource` | IDamageSource | 上次伤害来源 |
| `mainHandHeldItem` | IItemStack | 主手物品 |
| `maxHealth` | float | 最大生命值 |
| `offHandHeldItem` | IItemStack | 副手物品 |
| `revengeTarget` | IEntityLivingBase | 复仇目标 |
| `swingInProgress` | boolean | 是否正在挥动 |
| `totalArmorValue` | int | 总护甲值 |
| `moveForward` | float | 前进移动量 |
| `moveStrafing` | float | 横向移动量 |
| `moveVertical` | float | 垂直移动量 |

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `AIMovementSpeed` | float | 设置 AI 移动速度 |
| `arrowsInEntity` | int | 设置插在实体上的箭数量 |
| `health` | float | 设置当前生命值 |
| `lastAttackedEntity` | IEntityLivingBase | 设置上次攻击的实体 |
| `revengeTarget` | IEntityLivingBase | 设置复仇目标 |
| `swingProgress` | int | 设置挥动进度 |
| `moveForward` | float | 设置前进移动量 |
| `moveStrafing` | float | 设置横向移动量 |
| `moveVertical` | float | 设置垂直移动量 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.attackEntityFrom(IDamageSource, float)` | boolean | 对实体造成伤害 |
| `.canEntityBeSeen(IEntity)` | boolean | 检查是否能看到指定实体 |
| `.hasItemInSlot(IEntityEquipmentSlot)` | boolean | 检查指定装备槽是否有物品 |
| `.isPotionActive(IPotion)` | boolean | 检查指定药水是否激活 |
| `.isPotionEffectApplicable(IPotionEffect)` | boolean | 检查药水效果是否适用 |
| `.heal(float)` | void | 治疗实体 |
| `.getAttribute(String)` | IEntityAttributeInstance | 获取指定属性实例 |
| `.getItemInSlot(IEntityEquipmentSlot)` | IItemStack | 获取指定槽位的物品 |
| `.getActivePotionEffect(IPotion)` | IPotionEffect | 获取指定药水的激活效果 |
| `.addPotionEffect(IPotionEffect)` | void | 添加药水效果 |
| `.removePotionEffect(IPotion)` | void | 移除指定药水效果 |
| `.clearActivePotions()` | void | 清除所有激活的药水效果 |
| `.knockBack(IEntity, float, double, double)` | void | 击退 |
| `.onDeath()` | void | 死亡回调 |
| `.onLivingUpdate()` | void | 生物更新回调 |
| `.setItemToSlot(IEntityEquipmentSlot, IItemStack)` | void | 设置指定槽位的物品 |
| `.resetActiveHand()` | void | 重置激活的手 |
| `.stopActiveHand()` | void | 停止激活的手 |

### IEntityLiving（有生命实体，不包括玩家）

> `import crafttweaker.entity.IEntityLiving;`

有生命实体（不包括玩家）。继承 IEntityLivingBase。

#### @ZenGetter / @ZenSetter

| 属性 | 可写 | 类型 | 说明 |
|------|------|------|------|
| `attackInterval` | 否 | int | 攻击间隔 |
| `attackTarget` | 是 | IEntityLivingBase | 攻击目标 |
| `canBeSteered` | 否 | bool | 是否可被驾驭 |
| `canPickUpLoot` | 是 | bool | 是否可拾取战利品 |
| `canSpawnHere` | 否 | bool | 是否可在此生成 |
| `getLeashedToEntity` | 否 | IEntity | 被拴绳连接的实体 |
| `isAIDisabled` | 是 | bool | AI 是否禁用 |
| `isColliding` | 否 | bool | 是否正在碰撞 |
| `isLeashed` | 否 | bool | 是否被拴住 |
| `isLeftHanded` | 是 | bool | 是否为左撇子 |
| `isNoDespawnRequired` | 否 | bool | 是否设置为不消失 |
| `maxSpawnedInChunk` | 否 | int | 区块内最大生成数量 |
| `moveForward` | 是 | float | 前进移动量 |
| `moveStrafing` | 是 | float | 横向移动量 |
| `moveVertical` | 是 | float | 垂直移动量 |
| `renderSizeModifier` | 否 | float | 渲染大小修正值 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.playLivingSound()` | void | 播放生物声音 |
| `.spawnExplosionParticle()` | void | 生成爆炸粒子 |
| `.setDropChance(IEntityEquipmentSlot, float)` | void | 设置装备掉落几率 |
| `.enablePersistence()` | void | 启用持久化（防止消失） |
| `.setLeashedToEntity(IEntity, boolean)` | void | 设置拴绳连接到指定实体 |
| `.clearLeashed(boolean, boolean)` | void | 解除拴绳 |
| `.canBeLeashedTo(IPlayer)` | boolean | 检查是否可被指定玩家拴住 |

### IEntityAttribute（属性）

> `import crafttweaker.entity.Attribute;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 属性名称 |
| `defaultValue` | double | 默认值 |
| `shouldWatch` | boolean | 是否监控 |
| `parent` | IEntityAttribute | 父属性 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.clampValue(double)` | double | 将值限制在属性允许范围内 |

### IEntityAttributeInstance（属性实例）

> `import crafttweaker.entity.AttributeInstance;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `attribute` | IEntityAttribute | 属性定义 |
| `baseValue` | double | 基础值 |
| `modifiers` | List<IEntityAttributeModifier> | 修饰符列表 |
| `attributeValue` | double | 最终属性值 |

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `baseValue` | double | 设置基础值 |

#### 修饰符方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getModifiersByOperation(int)` | List<IEntityAttributeModifier> | 按操作类型获取修饰符 |
| `.hasModifier(IEntityAttributeModifier)` | boolean | 检查是否拥有指定修饰符 |
| `.getModifier(String)` | IEntityAttributeModifier | 按 UUID 获取修饰符 |
| `.applyModifier(IEntityAttributeModifier)` | void | 应用修饰符 |
| `.removeModifier(IEntityAttributeModifier)` | void | 移除修饰符 |
| `.removeModifier(String)` | void | 按 UUID 移除修饰符 |
| `.removeAllModifiers()` | void | 移除所有修饰符 |

### IEntityAttributeModifier（属性修饰符）

> `import crafttweaker.entity.AttributeModifier;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `uuid` | string | UUID |
| `name` | string | 名称 |
| `operation` | int | 操作类型（0=加法, 1=乘法基础, 2=乘法） |
| `amount` | double | 数值 |
| `saved` | boolean | 是否已保存 |

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `saved` | boolean | 设置是否保存 |

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `AttributeModifier.createModifier(String, double, int, @Optional String)` | IEntityAttributeModifier | 创建属性修饰符 |

操作类型说明：
- 0 = add：增加 X 由 Amount
- 1 = multiply_base：增加 Y 由 X * Amount
- 2 = multiply：Y = Y * (1 + Amount)

---

## 使用示例

### 生物掉落示例

```zenscript
val sheep = <entity:minecraft:sheep>;

// 添加掉落：物品, 最小数量, 最大数量, 几率
sheep.addDrop(<minecraft:apple>);
sheep.addDrop(<minecraft:stone> % 20);  // 权重 20

// 仅玩家击杀掉落
sheep.addPlayerOnlyDrop(<minecraft:gold_ingot>, 10, 64);
sheep.addPlayerOnlyDrop(<minecraft:iron_ingot> % 20, 1, 3);

// 移除掉落
sheep.removeDrop(<minecraft:wool>);

// 清除所有掉落
sheep.clearDrops();

// 创建和生成实体
val world = crafttweaker.world.IWorld.getFromString("overworld"); // 示例
<entity:minecraft:sheep>.spawnEntity(world, blockPos);
```

---

## ZenUtils 扩展（需安装 ZenUtils）

> `import mods.zenutils.*;`

### IEntity 扩展

对 `crafttweaker.entity.IEntity` 的扩展，所有实体对象自动可用。

#### ZenGetter

| 属性 | 返回 | 说明 |
|------|------|------|
| `nbt` | IData | 获取实体的完整 NBT 数据 |
| `position` | IBlockPos | 获取实体位置（方块坐标） |
| `world` | IWorld | 获取实体所在世界 |
| `id` | int | 获取实体的实体 ID |
| `uuid` | String | 获取实体 UUID 字符串 |
| `name` | String | 获取实体名称 |
| `eyeHeight` | float | 获取实体眼睛高度 |
| `width` | float | 获取实体宽度 |
| `height` | float | 获取实体高度 |
| `isCreatureType(CreatureType, bool)` | bool | 检查实体是否属于指定生物类型 |

#### ZenMethods

| 方法 | 返回 | 说明 |
|------|------|------|
| `setNBT(IData)` | void | 设置实体 NBT 数据 |
| `sendMessage(String)` | void | 向实体发送消息（仅玩家有效） |
| `getRelatedEntities()` | IEntity[] | 获取相关实体列表 |
| `getEntitiesNear(double)` | IEntity[] | 获取附近实体 |
| `teleport(IWorld, double, double, double)` | void | 传送实体到指定坐标 |

### IEntityDefinition 扩展

对 `crafttweaker.entity.IEntityDefinition` 的扩展。

| 方法 | 返回 | 说明 |
|------|------|------|
| `onTick(IEntityTick, @Optional int)` | void | 为特定实体类型添加周期性 tick 回调。仅服务端执行，无需检查 `world.remote` |

```zenscript
// 每 50 tick 对所有苦力怕执行一次
<entity:minecraft:creeper>.onTick(function(entity) {
    print("creeper? " ~ entity.world.time);
}, 50);
```
