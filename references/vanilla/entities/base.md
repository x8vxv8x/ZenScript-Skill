# 实体基础类型

## IEntity

> `import crafttweaker.entity.IEntity;`

IEntity 继承 ICommandSender，因此 ICommandSender 的所有方法也可用于 IEntity 对象。

ICommandSender 派生方法：`entity.displayName`、`entity.position`、`entity.world`、`entity.server`、`entity.sendMessage(String text)`

### ZenGetters

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

### ZenSetters

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

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.attackEntityFrom(IDamageSource, float)` | 伤害来源, 伤害值 | boolean | 对实体造成伤害 |
| `.canTrample(IWorld, IBlockDefinition, IBlockPos, float)` | 世界, 方块定义, 位置, 掉落值 | boolean | 检查是否可以踩踏 |
| `.isInsideOfMaterial(IMaterial)` | 材质 | boolean | 检查是否在指定材质内 |
| `.getDistanceSqToEntity(IEntity)` | 实体 | double | 获取到指定实体的距离平方 |
| `.getPickedResult()` | 无 | IItemStack | 获取拾取结果物品 |
| `.addTag(String)` | 标签 | void | 添加标签 |
| `.extinguish()` | 无 | void | 熄灭火焰 |
| `.onEntityUpdate()` | 无 | void | 实体更新回调 |
| `.onKillCommand()` | 无 | void | 执行 kill 命令回调 |
| `.onUpdate()` | 无 | void | 更新回调 |
| `.removeTag(String)` | 标签 | void | 移除标签 |
| `.setDead()` | 无 | void | 杀死实体 |
| `.spawnRunningParticles()` | 无 | void | 生成奔跑粒子效果 |
| `.removePassengers()` | 无 | void | 移除所有乘客 |
| `.dismountRidingEntity()` | 无 | void | 取消骑乘 |
| `.isOnSameTeam(IEntity)` | 实体 | boolean | 检查是否在同一队伍 |
| `.setInWeb()` | 无 | void | 设为被蜘蛛网缠住 |
| `.doWaterSplashEffect()` | 无 | void | 执行水花效果 |
| `.isEntityEqual(IEntity)` | 实体 | boolean | 检查实体是否相等 |
| `.isInvulnerableTo(IDamageSource)` | 伤害来源 | boolean | 检查是否对指定伤害来源无敌 |
| `.shouldRiderDismountInWater(IEntity)` | 骑乘者 | boolean | 检查骑乘者是否应在水中下马 |
| `.isPassenger(IEntity)` | 实体 | boolean | 检查是否为乘客 |
| `.isRidingSameEntity(IEntity)` | 实体 | boolean | 检查是否骑乘同一实体 |
| `.getRayTrace(double, float, @Optional boolean, @Optional boolean, @Optional boolean)` | 方块距离, 部分tick, 停在液体处, 忽略无碰撞箱方块, 返回最后不可碰撞方块 | IRayTraceResult | 射线追踪 |

---

## IEntityLivingBase

> `import crafttweaker.entity.IEntityLivingBase;`

有生命实体，包括怪物、动物和玩家。继承 IEntity。

### ZenGetters

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

### ZenSetters

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

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.attackEntityFrom(IDamageSource, float)` | 伤害来源, 伤害值 | boolean | 对实体造成伤害 |
| `.canEntityBeSeen(IEntity)` | 实体 | boolean | 检查是否能看到指定实体 |
| `.hasItemInSlot(IEntityEquipmentSlot)` | 装备槽 | boolean | 检查指定装备槽是否有物品 |
| `.isPotionActive(IPotion)` | 药水 | boolean | 检查指定药水是否激活 |
| `.isPotionEffectApplicable(IPotionEffect)` | 药水效果 | boolean | 检查药水效果是否适用 |
| `.heal(float)` | 治疗量 | void | 治疗实体 |
| `.getAttribute(String)` | 属性名 | IEntityAttributeInstance | 获取指定属性实例 |
| `.getItemInSlot(IEntityEquipmentSlot)` | 装备槽 | IItemStack | 获取指定槽位的物品 |
| `.getActivePotionEffect(IPotion)` | 药水 | IPotionEffect | 获取指定药水的激活效果 |
| `.addPotionEffect(IPotionEffect)` | 药水效果 | void | 添加药水效果 |
| `.removePotionEffect(IPotion)` | 药水 | void | 移除指定药水效果 |
| `.clearActivePotions()` | 无 | void | 清除所有激活的药水效果 |
| `.knockBack(IEntity, float, double, double)` | 来源实体, 强度, X比率, Z比率 | void | 击退 |
| `.onDeath()` | 无 | void | 死亡回调 |
| `.onLivingUpdate()` | 无 | void | 生物更新回调 |
| `.setItemToSlot(IEntityEquipmentSlot, IItemStack)` | 装备槽, 物品 | void | 设置指定槽位的物品 |
| `.resetActiveHand()` | 无 | void | 重置激活的手 |
| `.stopActiveHand()` | 无 | void | 停止激活的手 |

---

## IEntityLiving

> `import crafttweaker.entity.IEntityLiving;`

有生命实体（不包括玩家）。继承 IEntityLivingBase。

### ZenGetters/ZenSetters

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

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.playLivingSound()` | 无 | void | 播放生物声音 |
| `.spawnExplosionParticle()` | 无 | void | 生成爆炸粒子 |
| `.setDropChance(IEntityEquipmentSlot, float)` | 装备槽, 几率 | void | 设置装备掉落几率 |
| `.enablePersistence()` | 无 | void | 启用持久化（防止消失） |
| `.setLeashedToEntity(IEntity, boolean)` | 实体, 发送附着通知 | void | 设置拴绳连接到指定实体 |
| `.clearLeashed(boolean, boolean)` | 发送数据包, 掉落拴绳 | void | 解除拴绳 |
| `.canBeLeashedTo(IPlayer)` | 玩家 | boolean | 检查是否可被指定玩家拴住 |

---

## IEntityCreature

> `import crafttweaker.entity.IEntityCreature;`

生物（Creature）。继承 IEntityLiving。

### ZenGetters/ZenSetters

| 属性 | 类型 | 说明 |
|------|------|------|
| `hasPath` | bool | 是否有寻路路径 |
| `isWithinHomeDistance` | bool | 是否在家园范围内 |
| `homePosition` | IBlockPos | 家园位置 |
| `maximumHomeDistance` | float | 最大家园距离 |
| `hasHome` | bool | 是否设置家园 |

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.playLivingSound()` | 无 | void | 播放生物声音 |
| `.setHomePositionAndDistance(IBlockPos, int)` | 位置, 距离 | void | 设置家园位置和距离 |
| `.detachHome()` | 无 | void | 取消家园设置 |
| `.isPositionWithinHomeDistance(IBlockPos)` | 位置 | boolean | 检查位置是否在家园范围内 |

---

## IEntityAgeable

> `import crafttweaker.entity.IEntityAgeable;`

可成长实体（如牛）。继承 IEntityCreature。

### ZenGetters/ZenSetters

| 属性 | 可写 | 类型 | 说明 |
|------|------|------|------|
| `growingAge` | 是 | int | 成长年龄 |
| `scaleForAge` | 是 | bool | 是否按年龄缩放 |

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.ageUp(int, @Optional boolean)` | 秒数, 强制 | void | 增加年龄 |
| `.addGrowth(int)` | 秒数 | void | 增加成长值 |

---

## IEntityAnimal

> `import crafttweaker.entity.IEntityAnimal;`

动物。继承 IEntityAgeable。

### ZenGetters/ZenSetters

| 属性 | 类型 | 说明 |
|------|------|------|
| `loveCause` | IPlayer | 导致繁殖的玩家（可能为 null） |
| `isInLove` | bool | 是否处于繁殖状态 |

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.isBreedingItem(IItemStack)` | 物品 | boolean | 检查物品是否可用于繁殖 |
| `.setInLove(@Optional IPlayer)` | 玩家（可选） | void | 设置为繁殖状态 |
| `.resetInLove()` | 无 | void | 重置繁殖状态 |
| `.canMateWith(IEntityAnimal)` | 另一个动物 | boolean | 检查是否可与指定动物交配 |

---

## IEntityMob

> `import crafttweaker.entity.IEntityMob;`

敌对生物。继承 IEntityCreature。

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.isPreventingPlayerRest(IPlayer)` | 玩家 | boolean | 检查此生物是否阻止玩家睡觉 |
