# 实体特殊类型

## IEntityArrow

> `import crafttweaker.entity.IEntityArrow;`

箭矢。继承 IEntity 和 IProjectile。

### ZenGetters/ZenSetters

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

### ZenGetters

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

### ZenGetters

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

### ZenGetters

| 属性 | 类型 | 说明 |
|------|------|------|
| `caughtEntity` | IEntity | 被钓到的实体 |
| `angler` | IPlayer | 钓鱼者 |

### ZenSetters

| 属性 | 类型 | 说明 |
|------|------|------|
| `lureSpeed` | int | 诱惑速度 |
| `luck` | int | 幸运值 |

---

## IEntityItem

> `import crafttweaker.entity.IEntityItem;`

世界中的物品实体。继承 IEntity。

### ZenGetters/ZenSetters

| 属性 | 类型 | 说明 |
|------|------|------|
| `item` | IItemStack | 物品 |

---

## IEntityThrowable

> `import crafttweaker.entity.IEntityThrowable;`

可投掷实体。继承 IEntity 和 IProjectile。

### ZenGetters

| 属性 | 类型 | 说明 |
|------|------|------|
| `thrower` | IEntityLivingBase | 投掷者 |
| `shake` | int | 抖动值 |

---

## IEntityXp

> `import crafttweaker.entity.IEntityXp;`

经验球。继承 IEntity。

### ZenGetters

| 属性 | 类型 | 说明 |
|------|------|------|
| `xp` | float | 经验值 |

---

## IEntityAttribute（属性）

> `import crafttweaker.entity.Attribute;`

### ZenGetters

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 属性名称 |
| `defaultValue` | double | 默认值 |
| `shouldWatch` | boolean | 是否监控 |
| `parent` | IEntityAttribute | 父属性 |

### ZenMethods

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.clampValue(double)` | 值 | double | 将值限制在属性允许范围内 |

---

## IEntityAttributeInstance（属性实例）

> `import crafttweaker.entity.AttributeInstance;`

### ZenGetters

| 属性 | 类型 | 说明 |
|------|------|------|
| `attribute` | IEntityAttribute | 属性定义 |
| `baseValue` | double | 基础值 |
| `modifiers` | List<IEntityAttributeModifier> | 修饰符列表 |
| `attributeValue` | double | 最终属性值 |

### ZenSetters

| 属性 | 类型 | 说明 |
|------|------|------|
| `baseValue` | double | 设置基础值 |

### 修饰符方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getModifiersByOperation(int)` | 操作类型 | List<IEntityAttributeModifier> | 按操作类型获取修饰符 |
| `.hasModifier(IEntityAttributeModifier)` | 修饰符 | boolean | 检查是否拥有指定修饰符 |
| `.getModifier(String)` | UUID | IEntityAttributeModifier | 按 UUID 获取修饰符 |
| `.applyModifier(IEntityAttributeModifier)` | 修饰符 | void | 应用修饰符 |
| `.removeModifier(IEntityAttributeModifier)` | 修饰符 | void | 移除修饰符 |
| `.removeModifier(String)` | UUID | void | 按 UUID 移除修饰符 |
| `.removeAllModifiers()` | 无 | void | 移除所有修饰符 |

---

## IEntityAttributeModifier（属性修饰符）

> `import crafttweaker.entity.AttributeModifier;`

### ZenGetters

| 属性 | 类型 | 说明 |
|------|------|------|
| `uuid` | string | UUID |
| `name` | string | 名称 |
| `operation` | int | 操作类型（0=加法, 1=乘法基础, 2=乘法） |
| `amount` | double | 数值 |
| `saved` | boolean | 是否已保存 |

### ZenSetters

| 属性 | 类型 | 说明 |
|------|------|------|
| `saved` | boolean | 设置是否保存 |

### 静态方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `AttributeModifier.createModifier(String, double, int, @Optional String)` | 名称, 数值, 操作类型, UUID（可选） | IEntityAttributeModifier | 创建属性修饰符 |

操作类型说明：
- 0 = add：增加 X 由 Amount
- 1 = multiply_base：增加 Y 由 X * Amount
- 2 = multiply：Y = Y * (1 + Amount)

---

## 生物掉落示例

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

#### ZenGetters

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

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `setNBT(IData)` | IData | void | 设置实体 NBT 数据 |
| `sendMessage(String)` | String | void | 向实体发送消息（仅玩家有效） |
| `getRelatedEntities()` | 无 | IEntity[] | 获取相关实体列表 |
| `getEntitiesNear(double)` | double（距离） | IEntity[] | 获取附近实体 |
| `teleport(IWorld, double, double, double)` | IWorld, double, double, double | void | 传送实体到指定坐标 |

### IEntityDefinition 扩展

对 `crafttweaker.entity.IEntityDefinition` 的扩展。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `onTick(IEntityTick, @Optional int)` | IEntityTick, int（可选间隔） | void | 为特定实体类型添加周期性 tick 回调。仅服务端执行，无需检查 `world.remote` |

```zenscript
// 每 50 tick 对所有苦力怕执行一次
<entity:minecraft:creeper>.onTick(function(entity) {
    print("creeper? " ~ entity.world.time);
}, 50);
```
