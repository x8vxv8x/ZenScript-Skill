# 实体特殊类型

## IEntityArrow

> `import crafttweaker.entity.IEntityArrow;`

箭矢。继承 IEntity 和 IProjectile。

### ZenGetter/ZenSetter

| 属性 | 可写 | 类型 | 说明 |
|------|------|------|------|
| `shooter` | 是 | IEntity | 射出者 |
| `damage` | 是 | double | 伤害值 |
| `knockbackStrength` | 是 | int | 击退强度 |
| `isCritical` | 是 | boolean | 是否暴击 |
| `pickupStatus` | 是 | String | 拾取状态 |
| `shake` | 否 | int | 抖动值 |

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.shoot(IEntity, float, float, float, float, float)` | 射出者, 俯仰角, 偏航角, 翻滚角, 速度, 偏差 | void | 发射箭矢 |
| `.setPickupDisallowed()` | 无 | void | 设置不允许拾取 |
| `.setPickupAllowed()` | 无 | void | 设置允许拾取 |
| `.setPickupCreative()` | 无 | void | 设置仅创造模式可拾取 |

---

## IEntityArrowTipped

> `import crafttweaker.entity.IEntityArrowTipped;`

药箭。继承 IEntityArrow。

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.setPotionEffect(IItemStack)` | 药水物品 | void | 设置药水效果 |
| `.addPotionEffect(IPotionEffect)` | 药水效果 | void | 添加药水效果 |

---

---

## IEntityCreature

> `import crafttweaker.entity.IEntityCreature;`

生物（Creature）。继承 IEntityLiving。

### ZenGetter/ZenSetter

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

### ZenGetter/ZenSetter

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

### ZenGetter/ZenSetter

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

---

## IEntityDefinition

> `import crafttweaker.entity.IEntityDefinition;`

实体定义，引用游戏中注册的实体类型。

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `id` | string | 实体 ID（如 "net.minecraft.entity.passive.EntitySheep"） |
| `name` | string | 实体名称（如 "Sheep"） |
| `commandString` | string | 命令字符串 |
| `width` | float | 宽度 |
| `height` | float | 高度 |
| `immuneToFire` | bool | 是否免疫火焰 |
| `boss` | bool | 是否为 Boss |
| `creatureType` | string | 生物类型 |
| `drops` | List<IEntityDrop> | 通过 CT 添加的掉落物列表 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.createEntity(IWorld)` | 世界 | IEntity | 在指定世界创建实体（不生成） |
| `.spawnEntity(IWorld, IBlockPos)` | 世界, 位置 | IEntity | 在指定世界和位置生成实体 |
| `.addDrop(IItemStack)` | IItemStack | void | 添加掉落物 |
| `.addDrop(WeightedItemStack, @Optional int, @Optional int)` | 权重物品, 最小数量（可选）, 最大数量（可选） | void | 添加权重掉落物 |
| `.addDrop(IItemStack, @Optional int, @Optional int, @Optional float)` | IItemStack, 最小数量（可选）, 最大数量（可选）, 几率（可选） | void | 添加掉落物（带数量范围和几率） |
| `.addPlayerOnlyDrop(IItemStack)` | IItemStack | void | 添加仅玩家击杀掉落 |
| `.addPlayerOnlyDrop(IItemStack, int, int)` | IItemStack, int, int | void | 添加仅玩家击杀掉落（数量范围） |
| `.addPlayerOnlyDrop(WeightedItemStack, @Optional int, @Optional int)` | 权重物品, 最小数量（可选）, 最大数量（可选） | void | 添加权重仅玩家击杀掉落 |
| `.addDropFunction(IEntityDropFunction)` | 掉落函数 | void | 添加掉落函数，实体被击杀时调用 |
| `.removeDrop(IItemStack)` | IItemStack | void | 移除掉落物 |
| `.clearDrops()` | 无 | void | 清除所有掉落 |

---

## IEntityDrop

> `import crafttweaker.entity.IEntityDrop;`

实体掉落物，引用实体定义中的掉落物。

### ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `chance` | float | 掉落几率 |
| `max` | int | 最大掉落数量 |
| `min` | int | 最小掉落数量 |
| `playerOnly` | boolean | 是否仅玩家击杀掉落 |
| `range` | IntegerRange | 数量范围 |
| `stack` | IItemStack | 掉落物品 |

---

## IEntityDropFunction

> `import crafttweaker.entity.IEntityDropFunction;`

实体掉落函数，在关联实体被击杀时调用。

### 参数

函数接收以下参数：
- `entity` (IEntity) - 被击杀的实体
- `dmgSource` (IDamageSource) - 伤害来源

函数需要返回 IItemStack 或 `null`。

```zenscript
<entity:minecraft:sheep>.addDropFunction(function(entity, dmgSource) {
    return <minecraft:iron_ingot> * 10;
});
```

---

## IEntityEquipmentSlot

> `import crafttweaker.entity.IEntityEquipmentSlot;`

装备槽位，如主手、副手或盔甲槽。

### ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `index` | int | 索引 |
| `slotIndex` | int | 槽位索引 |
| `name` | string | 槽位名称 |

### 静态方法（枚举）

| 方法 | 返回 | 说明 |
|------|------|------|
| `IEntityEquipmentSlot.mainHand()` | IEntityEquipmentSlot | 主手 |
| `IEntityEquipmentSlot.offhand()` | IEntityEquipmentSlot | 副手 |
| `IEntityEquipmentSlot.feet()` | IEntityEquipmentSlot | 脚部 |
| `IEntityEquipmentSlot.legs()` | IEntityEquipmentSlot | 腿部 |
| `IEntityEquipmentSlot.chest()` | IEntityEquipmentSlot | 胸部 |
| `IEntityEquipmentSlot.head()` | IEntityEquipmentSlot | 头部 |

可使用 `==` 比较两个 IEntityEquipmentSlot 是否相等。

---

## IEntityFishHook

> `import crafttweaker.entity.IEntityFishHook;`

钓鱼钩。继承 IEntity。

### ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `caughtEntity` | IEntity | 被钓到的实体 |
| `angler` | IPlayer | 钓鱼者 |

### ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `lureSpeed` | int | 诱惑速度 |
| `luck` | int | 幸运值 |

---

## IEntityItem

> `import crafttweaker.entity.IEntityItem;`

世界中的物品实体。继承 IEntity。

### ZenGetter/ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IItemStack | 物品 |

---

## IEntityThrowable

> `import crafttweaker.entity.IEntityThrowable;`

可投掷实体。继承 IEntity 和 IProjectile。

### ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `thrower` | IEntityLivingBase | 投掷者 |
| `shake` | int | 抖动值 |

---

## IEntityXp

> `import crafttweaker.entity.IEntityXp;`

经验球。继承 IEntity。

### ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `xp` | float | 经验值 |
