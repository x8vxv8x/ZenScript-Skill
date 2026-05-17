# IItemStack 完整 API 参考

> `import crafttweaker.item.IItemStack;`

## 获取 IItemStack

```zenscript
<minecraft:apple>                           // 尖括号（最常用）
<minecraft:stone>.definition.makeStack(0)   // 通过 IItemDefinition
<ore:ingotGold>.items                       // 从矿辞获取列表
<ore:ingotGold>.firstItem                   // 从矿辞获取第一个
loadedMods["minecraft"].items               // 从 mod 获取所有物品
```

## ZenGetter 属性（只读）

| 属性 | 类型 | 说明 |
|------|------|------|
| `definition` | IItemDefinition | 物品定义 |
| `name` | string | 物品内部名 |
| `displayName` | string | 显示名称 |
| `damage` | int | 耐久损耗值 |
| `maxDamage` | int | 最大耐久 |
| `metadata` | int | Meta 值 |
| `hasTag` | bool | 是否有 NBT |
| `tag` | IData | NBT 数据（无 NBT 返回 `{}`） |
| `ores` | List\<IOreDictEntry\> | 所属矿辞列表 |
| `toolClasses` | List\<string\> | 工具类型 |
| `itemEnchantability` | int | 附魔能力 |
| `containerItem` | IItemStack | 容器物品（如空桶） |
| `hasContainerItem` | bool | 是否有容器物品 |
| `canEditBlocks` | bool | 是否可编辑方块 |
| `isOnItemFrame` | bool | 是否在物品展示框 |
| `isEnchantable` | bool | 是否可附魔 |
| `isEnchanted` | bool | 是否已附魔 |
| `isDamaged` | bool | 是否有耐久损耗 |
| `isDamageable` | bool | 是否可损耗 |
| `isItemBlock` | bool | 是否为方块物品 |
| `isStackable` | bool | 是否可堆叠 |
| `isBeaconPayment` | bool | 是否可作为信标消耗品 |
| `hasEffect` | bool | 是否有效果粒子 |
| `hasDisplayName` | bool | 是否有自定义显示名 |
| `hasSubtypes` | bool | 是否有子类型 |
| `isEmpty` | bool | 是否为空 |
| `burnTime` | int | 熔炉燃烧时间 |
| `showsDurabilityBar` | bool | 是否显示耐久条 |
| `hasCustomEntity` | bool | 是否有自定义实体 |
| `enchantments` | List\<IEnchantment\> | 附魔列表 |
| `matchTagExact` | bool | 精确匹配 NBT |
| `maxItemUseDuration` | int | 最大使用时长 |
| `capNBT` | IData | 能力 NBT |

## ZenSetter 属性（可读写）

| 属性 | 类型 | 说明 |
|------|------|------|
| `displayName` | string | 修改显示名称（全局生效） |
| `maxStackSize` | int | 修改最大堆叠数 |
| `maxDamage` | int | 修改最大耐久 |
| `repairCost` | int | 修改修复花费 |

## 数量方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.anyAmount()` | IItemStack | 任意数量（配方输入用） |
| `.amount(int)` | IItemStack | 设置数量 |
| `.withAmount(int)` | IItemStack | 设置数量（同上） |
| `stack * n` | IItemStack | 设置数量 |
| `.splitStack(int)` | IItemStack | 分割堆叠（原堆叠减少） |

## 耐久方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.anyDamage()` | IItemStack | 任意耐久（配方输入用） |
| `.withDamage(int)` | IItemStack | 设置耐久值 |
| `.damageItem(int, IEntity)` | void | 消耗耐久 |

## NBT 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.withEmptyTag()` | IItemStack | 设置空 NBT |
| `.withTag(IData)` | IItemStack | 设置 NBT（覆盖） |
| `.withTag(IData, bool)` | IItemStack | bool 为 true 时合并而非覆盖 |
| `.removeTag(String)` | IItemStack | 移除指定 NBT 键 |
| `.updateTag(IData)` | IItemStack | 合并 NBT（不覆盖已有键） |
| `.updateTag(IData, bool)` | IItemStack | 同上，bool 控制行为 |

## 显示方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.withDisplayName(String)` | IItemStack | 设置显示名（仅单物品） |
| `.withLore(String[])` | IItemStack | 设置 Lore |
| `.clearCustomName()` | void | 清除自定义名称 |
| `.addTooltip(String)` | void | 添加提示（全局生效） |
| `.addShiftTooltip(String)` | void | 添加 Shift 提示 |
| `.addShiftTooltip(String, String)` | void | Shift 提示 + 提示文字 |

## 附魔方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.canApplyAtCraftingTable(IEnchantmentDefinition)` | bool | 是否可在工作台附魔 |
| `.addEnchantment(IEnchantment)` | void | 添加附魔 |

## 方块方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.asBlock()` | IBlock | 转为方块 |
| `stack as IBlock` | IBlock | 转为方块 |
| `.canPlaceOn(IBlockDefinition)` | bool | 是否可放置在 |
| `.canDestroy(IBlockDefinition)` | bool | 是否可破坏 |
| `.canHarvestBlock(IBlockState)` | bool | 是否可挖掘 |
| `.getStrengthAgainstBlock(IBlockState)` | float | 对方块的破坏速度 |

## 权重方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.percent(float)` | WeightedItemStack | 百分比权重（100 = 100%） |
| `.weight(float)` | WeightedItemStack | 权重（1 = 100%） |
| `stack % 50` | WeightedItemStack | 50% 权重 |

## 实体方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createEntityItem(IWorld, float, float, float)` | IEntityItem | 创建掉落物实体 |
| `.createEntityItem(IWorld, IBlockPos)` | IEntityItem | 创建掉落物实体 |

## 其他

| 方法 | 返回 | 说明 |
|------|------|------|
| `.mutable()` | IMutableItemStack | 转为可变堆叠（原地修改） |
| `.getCapNBT()` | IData | 获取能力 NBT |
| `.withCapNBT(IData)` | IItemStack | 设置能力 NBT |
| `.liquid` | ILiquidStack | 获取关联流体（如桶） |
| `.isFood` | bool | 是否为食物 |
| `.healAmount` | int | 恢复饥饿值 |
| `.saturation` | float | 饱和度 |

---

# IIngredient 接口

> `import crafttweaker.item.IIngredient;`

IItemStack、IOreDictEntry、ILiquidStack 都实现了此接口。

## 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.mark(string)` | IIngredient | 标记（用于配方函数） |
| `.marked(string)` | IIngredient | 标记（同上） |
| `.amount` | int | 获取数量 |
| `.items` | List\<IItemStack\> | 匹配的物品列表 |
| `.itemArray` | IItemStack[] | 匹配的物品数组 |
| `.liquids` | List\<ILiquidStack\> | 匹配的流体列表 |
| `.commandString` | string | 命令字符串 |
| `.transform(IItemStack function(IItemStack, IPlayer))` | IIngredient | 自定义转换 |
| `.transformNew(IItemStack function(IItemStack, IPlayer))` | IIngredient | 自定义转换（新物品） |
| `.only(IItemStack function(IItemStack, IPlayer))` | IIngredient | 自定义条件 |
| `.matches(IItemStack)` | bool | 是否匹配 |
| `.matchesExact(IItemStack)` | bool | 是否精确匹配 |
| `.matches(ILiquidStack)` | bool | 是否匹配流体 |
| `ingredient has item` | bool | 是否包含 |
| `ingredient | other` | IIngredient | 或运算 |
| `.or(IIngredient)` | IIngredient | 或运算 |

---

# IItemDefinition

> `import crafttweaker.item.IItemDefinition;`

通过 `<minecraft:wool>.definition` 获取。

## 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `id` | string | 物品 ID |
| `name` | string | 内部名 |
| `maxStackSize` | int | 最大堆叠数 |
| `maxDamage` | int | 最大耐久 |
| `hasSubtypes` | bool | 是否有子类型 |
| `creativeTab` | string | 创造模式标签页 |
| `creativeTabs` | List\<string\> | 所有标签页 |

## 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.makeStack(int meta)` | IItemStack | 按 Meta 值创建物品 |
| `.setHarvestLevel(String toolClass, int level)` | void | 设置挖掘等级 |

---

# IOreDictEntry

> `import crafttweaker.oredict.IOreDictEntry;`

通过 `<ore:ingotIron>` 获取。

## 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 矿辞名称 |
| `items` | List\<IItemStack\> | 包含的物品列表 |
| `itemArray` | IItemStack[] | 包含的物品数组 |
| `firstItem` | IItemStack | 第一个物品 |
| `empty` | bool | 是否为空 |

## 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack)` | void | 添加物品到矿辞 |
| `.remove(IItemStack)` | void | 从矿辞移除物品 |
| `.addAll(IOreDictEntry)` | void | 将另一个矿辞的所有物品加入 |
| `.mirror(IOreDictEntry)` | void | 映射（A 的物品加入 B，但不反向） |
| `.matches(IItemStack)` | bool | 是否匹配 |
| `.has(IItemStack)` | bool | 是否包含 |
