# Baubles CraftTweaker API 参考

> Mod ID: `baubles`
> 前置条件: Roids-Tweaker（部分功能需要 Bubbles）
> 导入: 见各章节

## API 列表

### IPlayer 扩展

可在任何 IPlayer 上调用。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getBaublesInventory()` | 无 | IBaublesInventory | 获取饰品栏 |
| `.getBubblesInventory()` | 无 | IBubbleInventory | 获取 Bubbles 饰品栏（**需要 Bubbles**） |
| `.isBaubleEquipped(IItemStack bauble)` | bauble | int | 检查饰品是否装备，返回槽位号，未找到返回 -1 |

### IBauble

> `import mods.ctintegration.baubles.IBauble;`

静态工具类。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getBaubleType(IItemStack item)` | item | string | 获取饰品类型 |
| `.getValidSlots(String type)` | type | int[] | 获取该类型的有效槽位索引（**不兼容 Bubbles**） |
| `.createBauble(String type)` | type | InjectableBauble | 创建可注入饰品（见下方） |

### IBaublesInventory

> `import mods.ctintegration.baubles.IBaubleInventory;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.isItemValidForSlot(int slot, IItemStack item, IEntityLivingBase entity)` | slot, item, entity | bool | 检查物品是否可放入槽位 |
| `.isItemValid(int slot, IItemStack item)` | slot, item | bool | 检查物品是否有效 |
| `.getSlotCount()` | 无 | int | 获取槽位数量（Baubles 默认 7，其他模组可能更多） |
| `.getStackInSlot(int slot)` | slot | IItemStack | 获取槽位物品 |
| `.setStackInSlot(int slot, IItemStack item)` | slot, item | void | 设置槽位物品 |

支持迭代：`for item in IBaublesInventory { doStuff(item); }`

### IBubbleInventory

> `import mods.ctintegration.bubbles.IBubbleInventory;`

继承 IBaublesInventory，所有 IBaublesInventory 方法均可使用。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.growBaubleSlot(String type, int amount)` | type, amount | void | 增加指定类型的槽位 |
| `.shrinkBaubleSlot(String type, int amount)` | type, amount | void | 减少指定类型的槽位 |
| `.setBaubleSlot(String type, int amount)` | type, amount | void | 设置指定类型的槽位数量 |
| `.resetBaubleSlots()` | 无 | void | 重置所有饰品槽位 |

---

## 饰品物品创建

### 方式一：ContentTweaker 创建自定义饰品

**需要 ContentTweaker**

通过 `VanillaFactory.createBaubleItem(string unlocalizedName)` 获取 BaubleItemRepresentation。继承 ItemRepresentation，所有 ContentTweaker 物品构建器方法均可使用。

#### ZenProperty

| 属性 | 类型 | 说明 |
|------|------|------|
| `baubleType` | String | 必须为 'AMULET'、'RING'、'BELT'、'TRINKET'、'HEAD'、'BODY'、'CHARM' 之一，默认 TRINKET |
| `canEquip` | function(IItemStack, IEntityLivingBase) | 决定是否可装备 |
| `canUnequip` | function(IItemStack, IEntityLivingBase) | 决定是否可卸下 |
| `onWornTick` | function(IItemStack, IEntityLivingBase) | 每 tick 调用 |
| `onEquipped` | function(IItemStack, IEntityLivingBase) | 装备时调用 |
| `onUnequipped` | function(IItemStack, IEntityLivingBase) | 卸下时调用 |
| `willAutoSync` | function(IItemStack, IEntityLivingBase) | 自动同步 |
| `getBaubleType` | function(IItemStack) | 优先级高于 baubleType 属性 |

### 方式二：将现有物品转为饰品（需要 Bubbles）

**需要 Bubbles 和配置：`event category.allowCustomBaubles=true`**

> `mods.ctintegration.baubles.InjectableBauble;`

通过 `IBauble.createBauble(type)` 获取实例。仅支持原版饰品类型。

| 方法 | 参数 | 说明 |
|------|------|------|
| `.setOnWornTick(function)` | function(stack, entity) | 穿戴时每 tick 调用。默认：盔甲调用 onArmorTick，其他调用 onUpdate |
| `.setMainHand(bool)` | bool | 默认 onWornTick 是否视为主手持握，默认 true |
| `.setOnEquipped(function)` | function(stack, entity) | 装备时调用 |
| `.setOnUnequipped(function)` | function(stack, entity) | 卸下时调用 |
| `.setCanEquip(function)` | function(stack, entity): bool | 决定是否可装备 |
| `.setCanUnequip(function)` | function(stack, entity): bool | 决定是否可卸下 |
| `.setWillAutoSync(function)` | function(stack, entity): bool | 服务器是否每 10 tick 同步 NBT/伤害变化 |
| `.setOnDeath(function)` | function(slot, stack, entity): string | 死亡时调用，返回 "DEFAULT"、"ALWAYS_KEEP"、"ALWAYS_DROP"、"DESTROY"、"CUSTOM" |
| `.register(IItemDefinition item)` | item | 注入饰品到物品定义 |
