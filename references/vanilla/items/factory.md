# 自定义物品 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: ContentTweaker（部分需要 ZenUtils）
> 导入: `import mods.contenttweaker.VanillaFactory;`、`import mods.contenttweaker.Item;`、`import mods.contenttweaker.ItemFood;`

ContentTweaker 和 ZenUtils 自定义物品 API。

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
