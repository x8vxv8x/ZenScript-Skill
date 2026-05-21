# 有生命实体 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.entity.IEntityLivingBase;`、`import crafttweaker.entity.IEntityLiving;`

IEntityLivingBase、IEntityLiving 有生命实体 API。

---

## API 列表

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
