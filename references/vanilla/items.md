# Items CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.item.IItemStack;`、`import crafttweaker.item.IIngredient;`、`import crafttweaker.item.IMutableItemStack;`、`import crafttweaker.item.IItemDefinition;`、`import crafttweaker.item.IWeightedIngredient;`、`import crafttweaker.item.WeightedItemStack;`

物品系统 API，用于操作物品堆叠、配方原料和物品定义。

---

## API 列表

### IItemStack（物品堆叠）

> `import crafttweaker.item.IItemStack;`

#### 获取 IItemStack

```zenscript
<minecraft:apple>                           // 尖括号（最常用）
<minecraft:stone>.definition.makeStack(0)   // 通过 IItemDefinition
<ore:ingotGold>.items                       // 从矿辞获取列表
<ore:ingotGold>.firstItem                   // 从矿辞获取第一个
loadedMods["minecraft"].items               // 从 mod 获取所有物品
```

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `definition` | IItemDefinition | 物品定义 |
| `name` | string | 物品内部名 |
| `displayName` | string | 显示名称 |
| `hardness` | float | 方块硬度（破坏所需时间，仅方块有效） |
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

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `displayName` | string | 修改显示名称（全局生效） |
| `maxStackSize` | int | 修改最大堆叠数 |
| `hardness` | float | 修改方块硬度（仅方块有效） |
| `maxDamage` | int | 修改最大耐久 |
| `repairCost` | int | 修改修复花费 |

#### 数量方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.anyAmount()` | IItemStack | 任意数量（配方输入用） |
| `.amount(int)` | IItemStack | 设置数量 |
| `.withAmount(int)` | IItemStack | 设置数量（同上） |
| `stack * n` | IItemStack | 设置数量 |
| `.splitStack(int)` | IItemStack | 分割堆叠（原堆叠减少） |

#### 耐久方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.anyDamage()` | IItemStack | 任意耐久（配方输入用） |
| `.withDamage(int)` | IItemStack | 设置耐久值 |
| `.damageItem(int, IEntity)` | void | 消耗耐久 |

#### NBT 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.withEmptyTag()` | IItemStack | 设置空 NBT |
| `.withTag(IData)` | IItemStack | 设置 NBT（覆盖） |
| `.withTag(IData, bool)` | IItemStack | bool 为 true 时合并而非覆盖 |
| `.removeTag(String)` | IItemStack | 移除指定 NBT 键 |
| `.updateTag(IData)` | IItemStack | 合并 NBT（不覆盖已有键） |
| `.updateTag(IData, bool)` | IItemStack | 同上，bool 控制行为 |

#### 显示方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.withDisplayName(String)` | IItemStack | 设置显示名（仅单物品，支持 `§` 颜色代码） |
| `.withLore(String[])` | IItemStack | 设置 Lore（支持 `§` 颜色代码） |
| `.clearCustomName()` | void | 清除自定义名称 |
| `.addTooltip(String)` | void | 添加提示（全局生效） |
| `.addShiftTooltip(String)` | void | 添加 Shift 提示 |
| `.addShiftTooltip(String, String)` | void | Shift 提示 + 非 Shift 时的提示文字 |
| `.addAdvancedTooltip(ITooltipFunction fn)` | void | 添加动态提示（函数接收 IItemStack 返回 string） |
| `.addShiftTooltip(ITooltipFunction fn, @Optional ITooltipFunction infoFn)` | void | 添加动态 Shift 提示（两个参数要么都是函数，要么都是文本） |
| `.clearTooltip()` | void | 清除所有提示 |
| `.clearTooltip(bool leaveName)` | void | 清除所有提示，为 true 时保留物品名称 |
| `.removeTooltip(String regex)` | void | 移除匹配正则表达式的提示 |
| `.removeTooltipLine(int line)` | void | 移除指定行的提示 |

#### 附魔方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.canApplyAtCraftingTable(IEnchantmentDefinition)` | bool | 是否可在工作台附魔 |
| `.addEnchantment(IEnchantment)` | void | 添加附魔 |

#### 方块方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.asBlock()` | IBlock | 转为方块 |
| `stack as IBlock` | IBlock | 转为方块 |
| `.canPlaceOn(IBlockDefinition)` | bool | 是否可放置在 |
| `.canDestroy(IBlockDefinition)` | bool | 是否可破坏 |
| `.canHarvestBlock(IBlockState)` | bool | 是否可挖掘 |
| `.getStrengthAgainstBlock(IBlockState)` | float | 对方块的破坏速度 |

#### 权重方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.percent(float)` | WeightedItemStack | 百分比权重（100 = 100%） |
| `.weight(float)` | WeightedItemStack | 权重（1 = 100%） |
| `stack % 50` | WeightedItemStack | 50% 权重 |

#### 实体方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createEntityItem(IWorld, float, float, float)` | IEntityItem | 创建掉落物实体 |
| `.createEntityItem(IWorld, IBlockPos)` | IEntityItem | 创建掉落物实体 |

#### 其他方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.mutable()` | IMutableItemStack | 转为可变堆叠（原地修改） |
| `.getCapNBT()` | IData | 获取能力 NBT |
| `.withCapNBT(IData)` | IItemStack | 设置能力 NBT |
| `.liquid` | ILiquidStack | 获取关联流体（如桶） |
| `.isFood` | bool | 是否为食物 |
| `.healAmount` | int | 恢复饥饿值 |
| `.saturation` | float | 饱和度 |

### IIngredient（配方原料接口）

> `import crafttweaker.item.IIngredient;`

IItemStack、IOreDictEntry、ILiquidStack 都实现了此接口。

#### 方法

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
| `.applyTransform(IItemStack, IPlayer)` | IItemStack | 应用物品转换器，返回转换后的物品堆叠 |
| `.hasTransformers()` | bool | 是否绑定了物品转换器 |

### IMutableItemStack（可变物品堆叠）

> `import crafttweaker.item.IMutableItemStack;`

可变物品堆叠。`withTag`、`withAmount` 等方法会直接修改并返回原堆叠，而非创建新堆叠。

通过 `IItemStack.mutable()` 获取，继承 IItemStack 的所有方法。

#### 数量方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.grow(int count)` | IMutableItemStack | 增加指定数量 |
| `.shrink(int count)` | IMutableItemStack | 减少指定数量 |

#### 耐久方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.attemptDamageItem(int amount, @Optional IPlayer player)` | bool | 尝试损耗耐久，返回是否成功 |

#### 其他方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.copy()` | IItemStack | 复制为新的不可变堆叠（避免意外修改时使用） |

### IItemDefinition（物品定义）

> `import crafttweaker.item.IItemDefinition;`

通过 `<minecraft:wool>.definition` 获取。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `id` | string | 物品 ID |
| `name` | string | 内部名 |
| `maxStackSize` | int | 最大堆叠数 |
| `maxDamage` | int | 最大耐久 |
| `hasSubtypes` | bool | 是否有子类型 |
| `ores` | List\<IOreDictEntry\> | 所属矿辞列表（包含引用子物品的矿辞） |
| `owner` | string | 所属 mod 名称 |
| `defaultInstance` | IItemStack | 默认物品实例 |
| `creativeTab` | string | 创造模式标签页 |
| `creativeTabs` | List\<string\> | 所有标签页 |
| `canItemEditBlocks` | bool | 是否可编辑方块 |
| `itemEnchantability` | int | 附魔能力 |
| `subItems` | List\<IItemStack\> | 所有子物品列表（服务端 mod 不保证正确） |

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `creativeTab` | ICreativeTab | 设置创造模式标签页 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.makeStack(int meta)` | IItemStack | 按 Meta 值创建物品（meta 可选） |
| `.setHarvestLevel(String type, int level)` | void | 设置挖掘等级 |
| `.setNoRepair()` | void | 设置物品不可修复 |
| `.setContainerItem(IItemDefinition item)` | void | 设置容器物品 |
| `.getSubItems(ICreativeTab creativeTab)` | List\<IItemStack\> | 获取指定创造标签页下的子物品（服务端 mod 不保证正确） |
| `.getItemBurntime(IItemStack item)` | int | 获取燃烧时间：-1 为默认逻辑，0 为不可燃烧，其他为实际燃烧时间 |

### IWeightedIngredient / WeightedItemStack（带权重的物品）

> `import crafttweaker.item.IWeightedIngredient;`
> `import crafttweaker.item.WeightedItemStack;`

带百分比权重的物品，用于概率性掉落或副产物输出。WeightedItemStack 实现了 IWeightedIngredient 接口。

通过 `%` 运算符或 `.weight()` 方法从 IItemStack 创建：

```zenscript
val wItem = <minecraft:diamond> % 20;      // 20% 概率
val wItem2 = <minecraft:diamond>.weight(0.2); // 同上（0.2 = 20%）
```

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `stack` | IItemStack | 关联的物品堆叠 |
| `ingredient` | IIngredient | 关联的配方原料 |
| `chance` | float | 小数形式概率（如 0.2） |
| `percent` | float | 百分比形式概率（如 20.0） |

---

## 物品条件（Item Conditions）

附加到物品上，用于配方的特殊需求。

> **注意：** 使用耐久相关条件时，先加 meta 通配符禁用默认精确耐久匹配：
> `<minecraft:iron_pickaxe:*>.onlyDamaged()`

| 条件 | 说明 |
|------|------|
| `.anyDamage()` | 耐久值不影响合成 |
| `.onlyDamaged()` | 只有有损耗的物品才能参与 |
| `.onlyDamageAtLeast(int)` | 耐久不小于指定值 |
| `.onlyDamageAtMost(int)` | 耐久不大于指定值 |
| `.onlyDamageBetween(int, int)` | 耐久在两者之间 |
| `.withTag(IData)` | 需要带有指定 NBT |
| `.onlyWithTag(IData)` | 需要**只**带有指定 NBT |
| `.withDamage(int)` | 输出带有指定耐久 |
| `.only(function)` | 自定义条件函数 |

```zenscript
// 有损耗的铁镐才能参与合成
<minecraft:iron_pickaxe:*>.onlyDamaged().withTag({display: {Lore: ["损坏的铁镐"]}});

// 自定义条件：只在下界生效
recipes.addShapeless("nether_recipe", <minecraft:netherrack>,
    [<ore:cobblestone>, <ore:cobblestone>, <ore:cobblestone>],
    function(output, ins, info) {
        return info.player.world.dimension == -1 ? output : null;
    },
null);
```

---

## 物品转换器（Item Transformers）

用于合成后物品不消耗、转换为其他物品等场景。

| 转换器 | 说明 |
|--------|------|
| `.reuse()` | 物品不消耗，留在工作台 |
| `.giveBack()` | 物品不消耗，整组回到物品栏 |
| `.giveBack(IItemStack)` | 物品被消耗，但返回指定物品到物品栏 |
| `.transformReplace(IItemStack)` | 合成后变为指定物品放入工作台槽位 |
| `.transformDamage()` | 合成后掉 1 点耐久 |
| `.transformDamage(int)` | 合成后掉指定点耐久 |
| `.noReturn()` | 强制消耗（即使有容器物品） |
| `.transformConsume(int)` | 消耗指定个数 |
| `.transform(function(IItemStack, IPlayer))` | 自定义转换函数（返回物品替换槽位内容，null 清空槽位，可能在 1.13 移除） |
| `.transformNew(function(IItemStack))` | 新版自定义转换函数（不需要 player 参数时优先使用） |

```zenscript
// 石斧 + 木板 = 3 木棍，石斧掉 1 耐久
recipes.addShapeless(<minecraft:stick> * 3, [
    <minecraft:stone_axe>.transformDamage(), <ore:plankWood>
]);

// 牛奶桶合成蛋糕后变空桶（自动，无需手动转换）
// 如需阻止返回空桶：用 .noReturn()

// giveBack(IItemStack)：物品被消耗但返回指定物品
<minecraft:bucket>.giveBack(<minecraft:stick>)

// transform：自定义转换（旧版，接收 item 和 player）
item.transform(function(item, player) { return item; });

// transformNew：自定义转换（新版，只接收 item）
item.transformNew(function(item) { return item; });
```

---

## ContentTweaker 扩展（需安装 ContentTweaker）

> `import mods.contenttweaker.VanillaFactory;`
> `import mods.contenttweaker.Item;`
> `import mods.contenttweaker.ItemFood;`

CoT 脚本第一行必须为 `#loader contenttweaker`。

### VanillaFactory 物品方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createItem(string id)` | Item | 创建自定义物品（ID 全小写，字母开头） |
| `.createItemFood(string id, int healAmount)` | ItemFood | 创建自定义食物 |

### Item（自定义物品）

> `import mods.contenttweaker.Item;`

| ZenProperty | 类型 | 默认值 | 说明 |
|-------------|------|--------|------|
| `maxStackSize` | int | 64 | 最大堆叠数 |
| `maxDamage` | int | -1 | 耐久（<0 为普通物品，>0 为工具） |
| `rarity` | string | "COMMON" | 稀有度: "COMMON"/"UNCOMMON"/"RARE"/"EPIC" |
| `creativeTab` | ICreativeTab | 杂项 | 所在创造标签 |
| `glowing` | bool | false | 是否有附魔光芒 |
| `beaconPayment` | bool | false | 是否可作为信标消耗品 |
| `toolClass` | string | null | 工具类型（"pickaxe"/"axe" 等） |
| `toolLevel` | int | -1 | 工具挖掘等级 |

| 方法 | 返回 | 说明 |
|------|------|------|
| `.register()` | void | 注册物品进游戏（注册后不可修改） |

### ItemFood（自定义食物）

> `import mods.contenttweaker.ItemFood;`

继承 Item 的所有属性，另有：

| ZenProperty | 类型 | 默认值 | 说明 |
|-------------|------|--------|------|
| `healAmount` | int | - | 恢复饥饿值 |
| `saturation` | float | 0.6 | 相对饱和度 |
| `alwaysEdible` | bool | false | 饥饿值满时是否可吃 |
| `wolfFood` | bool | false | 是否可喂给狼 |
| `onItemFoodEaten` | function | null | 吃下后执行的函数 |

### ContentTweaker 物品示例

```zenscript
#loader contenttweaker
import mods.contenttweaker.VanillaFactory;
import mods.contenttweaker.ItemFood;

var soup as ItemFood = VanillaFactory.createItemFood("sweet_soup", 4);
soup.saturation = 0.8;
soup.alwaysEdible = true;
soup.onItemFoodEaten = function(stack, world, player) {
    if (!world.remote) {
        player.addPotionEffect(<potion:minecraft:speed>.makePotionEffect(100, 1));
    }
};
soup.register();
```

---

## ZenUtils 扩展（需安装 ZenUtils + ContentTweaker）

> `import mods.zenutils.cotx.*;`

该部分是对 ContentTweaker 物品系统的扩展(见上方ContentTweaker 扩展)。

### VanillaFactory 物品扩展方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `VanillaFactory.createEnergyItem(String, int, int, int)` | EnergyItem | 创建能量物品 |
| `VanillaFactory.createExpandItem(String)` | ExpandItem | 创建扩展物品 |

### ExpandItem（扩展物品）

> `import mods.zenutils.cotx.Item;`

继承 ContentTweaker 的 `ItemRepresentation`。

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `onEntityItemUpdate` | IEntityItemUpdate | null | 物品实体更新回调。返回 true 跳过后续更新 |
| `noRepair` | bool | false | 是否不可修复 |
| `getEntityLifeSpan` | IGetEntityLifeSpan | null | 掉落物存活时间回调。返回 tick 数（默认 6000） |

#### IEntityItemUpdate（函数式接口）

> `import mods.zenutils.cotx.IEntityItemUpdate;`

参数：`IEntityItem`。返回 `bool`（true=跳过后续更新）。

#### IGetEntityLifeSpan（函数式接口）

> `import mods.zenutils.cotx.IGetEntityLifeSpan;`

参数：`IItemStack`, `IWorld`。返回 `int`（tick 数，默认 6000）。

### EnergyItem（能量物品）

> `import mods.zenutils.cotx.EnergyItem;`

继承 `ExpandItem`，无额外 ZenProperties。通过 `VanillaFactory.createEnergyItem` 创建。

### LateSetCoTFunction 物品部分

| Bracket | 返回 | 说明 |
|------|------|------|
| `<cotItem:name>` | IItemRepresentation | 获取 ContentTweaker 物品 |

| 属性 | 回调签名 | 说明 |
|------|------|------|
| `IItemRepresentation.onItemUse` | (player, world, pos, hand, facing, blockHit) → ActionResult | 物品使用回调 |

```zenscript
#loader crafttweaker reloadable
import mods.zenutils.cotx.LateSetCoTFunction;

<cotItem:test_item>.onItemUse = function(player, world, pos, hand, facing, blockHit) {
    // 自定义物品使用逻辑
    return ActionResult.success();
};
```

---

## RandomTweaker 扩展（需安装 RandomTweaker）

> `import mods.randomtweaker.vanilla.IItemStack;`

IItemStack 的扩展类，IItemStack 实例可直接使用这些方法。由于类名与 CrT 自带的 IItemStack 重合，如需用类名调用需使用 `as` 重定向：`import mods.randomtweaker.vanilla.IItemStack as IItemStackExpansion;`

### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getTagSize()` | int | 返回物品 NBT 中有多少个 key（空 NBT `{}` 返回 0）
