# ContentTweaker CraftTweaker API 参考

> Mod ID: `contenttweaker`
> 前置条件: CraftTweaker
> 导入: `import mods.contenttweaker.*;`

ContentTweaker (CoT) 允许用 ZenScript 为游戏添加自定义物品、方块、流体、创造标签等。

**重要**: CoT 脚本第一行必须为 `#loader contenttweaker`。

---

## 指令

| 指令 | 用途 |
|------|------|
| `/ct blockmaterial` | 打印所有 Block Material 至日志 |
| `/ct creativetab` | 打印所有创造标签至日志 |
| `/ct soundevent` | 打印所有 SoundEvent 至日志 |
| `/ct soundtype` | 打印所有 SoundType 至日志 |
| `/ct parts` | 打印所有已注册的材料部件至日志 |

---

## API 列表

### VanillaFactory（原版加工厂）

> `import mods.contenttweaker.VanillaFactory;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.createItem(string id)` | 物品 ID（全小写，字母开头） | Item | 创建物品 |
| `.createBlock(string id, BlockMaterial)` | 方块 ID, 方块材质 | Block | 创建方块 |
| `.createFluid(string id, int color)` | 流体 ID, RGB 颜色 | Fluid | 创建流体 |
| `.createItemFood(string id, int healAmount)` | 食物 ID, 恢复饥饿值 | ItemFood | 创建食物 |
| `.createCreativeTab(string id, IItemStack/Item/Block icon)` | 标签 ID, 图标 | CreativeTab | 创建创造标签 |

### Item（物品）

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

| 方法 | 说明 |
|------|------|
| `.register()` | 注册物品进游戏（注册后不可修改） |

### Block（方块）

> `import mods.contenttweaker.Block;`

| ZenProperty | 类型 | 默认值 | 说明 |
|-------------|------|--------|------|
| `blockHardness` | float | 5.0 | 方块硬度 |
| `blockResistance` | float | 5.0 | 防爆等级 |
| `blockSoundType` | SoundType | `<soundtype:metal>` | 方块声音 |
| `creativeTab` | ICreativeTab | 杂项 | 所在创造标签 |
| `lightValue` | int | 0 | 光照等级（最大 15） |
| `lightOpacity` | bool | 255/0 | 不透明度 |
| `fullBlock` | bool | true | 是否完整方块 |
| `translucent` | bool | false | 是否半透明 |
| `blockLayer` | string | "SOLID" | 渲染层: "SOLID"/"CUTOUT_MIPPED"/"CUTOUT"/"TRANSLUCENT" |
| `gravity` | bool | false | 是否受重力影响 |
| `slipperiness` | float | 0.6 | 滑度（冰为 0.98） |
| `toolClass` | string | "pickaxe" | 需要的挖掘工具 |
| `toolLevel` | int | 2 | 需要的挖掘等级 |
| `entitySpawnable` | bool | true | 生物是否可在此方块上生成 |
| `witherProof` | bool | false | 是否抵御凋灵爆炸 |
| `beaconBase` | bool | false | 是否可作为信标基座 |
| `replaceable` | bool | 取决于材质 | 是否可直接替换 |
| `passable` | bool | 取决于材质 | 玩家是否可通过 |
| `dropHandler` | IBlockDropHandler | null | 自定义掉落物函数 |

| 方法 | 说明 |
|------|------|
| `.register()` | 注册方块进游戏 |

### Fluid（流体）

> `import mods.contenttweaker.Fluid;`

| ZenProperty | 类型 | 默认值 | 说明 |
|-------------|------|--------|------|
| `density` | int | 1000 | 密度（水=1000，熔岩=3000） |
| `viscosity` | int | 1000 | 黏度（水=1000，熔岩=3000） |
| `temperature` | int | 300 | 温度（水=300，熔岩=1300） |
| `luminosity` | int | 0 | 亮度 |
| `vaporize` | bool | false | 在下界是否蒸发 |
| `colorize` | bool | true | 材质是否受颜色参数影响 |
| `stillLocation` | string | "contenttweaker:fluids/fluid" | 源头材质路径 |
| `flowingLocation` | string | "contenttweaker:fluids/fluid_flow" | 流动材质路径 |
| `material` | IMaterialDefinition | `<blockmaterial:water>` | 方块材质 |
| `gaseous` | bool | false | 是否反重力流动 |

| 方法 | 说明 |
|------|------|
| `.register()` | 注册流体进游戏 |

### ItemFood（食物）

> `import mods.contenttweaker.ItemFood;`

继承 Item 的所有属性，另有：

| ZenProperty | 类型 | 默认值 | 说明 |
|-------------|------|--------|------|
| `healAmount` | int | - | 恢复饥饿值 |
| `saturation` | float | 0.6 | 相对饱和度 |
| `alwaysEdible` | bool | false | 饥饿值满时是否可吃 |
| `wolfFood` | bool | false | 是否可喂给狼 |
| `onItemFoodEaten` | function | null | 吃下后执行的函数 |

### CreativeTab（创造标签）

> `import mods.contenttweaker.CreativeTab;`

| 方法 | 说明 |
|------|------|
| `.register()` | 注册创造标签 |

---

## 材料系统

> `import mods.contenttweaker.MaterialSystem;`

允许批量添加金属的不同部件（齿轮、板、锭等）。

### MaterialBuilder（材料构建器）

> `import mods.contenttweaker.MaterialBuilder;`

| 方法 | 参数 | 说明 |
|------|------|------|
| `MaterialSystem.getMaterialBuilder()` | 无 | 获取构建器 |
| `.setName(string)` | 材料 ID | 设置名称 |
| `.setColor(int)` | RGB 颜色 | 设置颜色 |
| `.setHasEffect(bool)` | 是否有附魔光芒 | 设置效果 |
| `.build()` | 无 | 构建 Material 对象 |

### PartBuilder（部件构建器）

> `import mods.contenttweaker.PartBuilder;`

| 方法 | 参数 | 说明 |
|------|------|------|
| `MaterialSystem.getPartBuilder()` | 无 | 获取构建器 |
| `.setName(string)` | 部件 ID | 设置名称 |
| `.setPartType(PartType)` | 部件类型 | 设置类型 |
| `.setOreDictName(string)` | 矿辞前缀 | 设置矿辞名 |
| `.setHasOverlay(bool)` | 是否有 overlay | 设置覆盖层 |
| `.build()` | 无 | 构建 Part 对象 |

### 预设部件类型

**物品**: beam, bolt, casing, clump, crystal, crushed_ore, dense_plate, dirty_dust, dust, gear, ingot, nugget, plate, rod, shard

**方块**: block

**矿石**: ore, dense_ore, poor_ore

**流体**: molten

**护甲**: armor (head, chest, legs, feet)

### Material 方法

| 方法 | 说明 |
|------|------|
| `.registerParts(string[])` | 注册多个部件 |
| `.registerPart(string)` | 注册单个部件 |

### MaterialPartData（材料部件数据）

> `import mods.contenttweaker.MaterialPartData;`

| 方法 | 说明 |
|------|------|
| `.getData()` | 获取数据对象 |
| `.addDataValue(string name, string value)` | 添加数据字段 |

**物品字段**: burn (燃烧时间)

**盔甲字段**: durability, enchantability, reduction, toughness

**流体字段**: temperature, density, luminosity, viscosity, vaporize

**矿石字段**: drops, variants, hardness, resistance, harvestLevel, harvestTool

---

## 匠魂联动

### TiC 材料构建

> `import mods.contenttweaker.tconstruct.MaterialBuilder;`

| 方法 | 说明 |
|------|------|
| `MaterialBuilder.create(string)` | 创建材料构建器 |
| `.color = int` | 设置颜色 |
| `.craftable = bool` | 部件加工台可制作 |
| `.castable = bool` | 冶炼炉可制作 |
| `.liquid = ILiquidStack` | 设置流体 |
| `.representativeItem = IItemStack` | 宝典显示物品 |
| `.addItem(IIngredient)` | 添加合成材料 |
| `.addHeadMaterialStats(dur, speed, damage, level)` | 镐头属性 |
| `.addHandleMaterialStats(modifier, dur)` | 手柄属性 |
| `.addExtraMaterialStats(dur)` | 额外部件属性 |
| `.addBowMaterialStats(draw, range, damage)` | 弓属性 |
| `.addBowStringMaterialStats(modifier)` | 弓弦属性 |
| `.addArrowShaftMaterialStats(modifier, bonus)` | 箭杆属性 |
| `.addFletchingMaterialStats(accuracy, modifier)` | 箭羽属性 |
| `.addProjectileMaterialStats()` | 投射物属性 |
| `.addMaterialTrait(string, @Optional string)` | 添加特性 |
| `.removeMaterialTrait(string, @Optional string)` | 移除特性 |
| `.register()` | 注册材料 |

### TiC 特性构建

> `import mods.contenttweaker.tconstruct.TraitBuilder;`

| 方法 | 说明 |
|------|------|
| `TraitBuilder.create(string)` | 创建特性构建器 |
| `.color = int` | 设置颜色 |
| `.maxLevel = int` | 最高等级 |
| `.countPerLevel = int` | 升级所需计数 |
| `.localizedName = string` | 本地化名称 |
| `.localizedDescription = string` | 本地化描述 |
| `.addItem(IIngredient)` | 添加合成材料 |
| `.register()` | 注册特性 |

**可用特性函数**:

| 函数 | 参数 | 说明 |
|------|------|------|
| `.afterHit` | trait, tool, attacker, target, damage, wasCrit, wasHit | 攻击后 |
| `.onHit` | trait, tool, attacker, target, damage, isCritical | 攻击时 |
| `.onBlock` | trait, tool, attacker, event | 格挡时 |
| `.onPlayerHurt` | trait, tool, player, attacker, event | 受伤时 |
| `.onUpdate` | trait, tool, world, entity, slot, isSelected | 每 tick |
| `.getMiningSpeed` | trait, tool, event | 挖掘速度 |
| `.beforeBlockBreak` | trait, tool, event | 破坏方块前 |
| `.afterBlockBreak` | trait, tool, world, blockstate, pos, miner, wasEffective | 破坏方块后 |
| `.onBlockHarvestDrops` | trait, tool, event | 方块掉落时 |
| `.calcCrit` | trait, tool, attacker, target → bool | 计算暴击 |
| `.calcDamage` | trait, tool, attacker, target, orig, curr, isCrit → float | 计算伤害 |
| `.calcKnockBack` | trait, tool, attacker, target, dmg, kb, newKb, isCrit → float | 计算击退 |
| `.onToolDamage` | trait, tool, damage, newDamage, entity → int | 工具耐久损耗 |
| `.calcToolHeal` | trait, tool, damage, newDamage, entity → int | 工具修复 |
| `.onToolRepair` | trait, tool, amount | 修复工具时 |

---

## 使用示例

### 创建自定义物品

```zenscript
#loader contenttweaker
import mods.contenttweaker.VanillaFactory;
import mods.contenttweaker.Item;

val zsItem as Item = VanillaFactory.createItem("zs_item");
zsItem.maxDamage = 8848;
zsItem.rarity = "rare";
zsItem.creativeTab = <creativetab:tools>;
zsItem.toolClass = "pickaxe";
zsItem.toolLevel = 5;
zsItem.register();
```

### 创建自定义方块

```zenscript
#loader contenttweaker
import mods.contenttweaker.VanillaFactory;
import mods.contenttweaker.Block;

var antiIceBlock as Block = VanillaFactory.createBlock("anti_ice", <blockmaterial:ice>);
antiIceBlock.lightOpacity = 3;
antiIceBlock.blockHardness = 1.0;
antiIceBlock.blockResistance = 5.0;
antiIceBlock.toolClass = "pickaxe";
antiIceBlock.toolLevel = 0;
antiIceBlock.blockSoundType = <soundtype:snow>;
antiIceBlock.slipperiness = 0.75;
antiIceBlock.register();
```

### 创建自定义流体

```zenscript
#loader contenttweaker
import mods.contenttweaker.VanillaFactory;
import mods.contenttweaker.Fluid;

var zsFluid as Fluid = VanillaFactory.createFluid("zs_fluid", 0xFF69B4);
zsFluid.temperature = 500;
zsFluid.viscosity = 1500;
zsFluid.density = 1500;
zsFluid.luminosity = 4;
zsFluid.stillLocation = "base:fluids/liquid";
zsFluid.flowingLocation = "base:fluids/liquid_flow";
zsFluid.register();
```

### 创建食物（带药水效果）

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
        player.addPotionEffect(<potion:minecraft:strength>.makePotionEffect(200, 2));
    }
};
soup.register();
```

### 批量创建材料部件

```zenscript
#loader contenttweaker
import mods.contenttweaker.MaterialSystem;

val copper as Material = MaterialSystem.getMaterialBuilder().setName("Copper").setColor(0xFF9933).build();
copper.registerParts(["gear", "casing", "rod"]); // 同时注册铜齿轮、铜外壳、铜杆

// 自定义部件
val denseIngotPart = MaterialSystem.getPartBuilder()
    .setName("dense_ingot")
    .setPartType(MaterialSystem.getPartType("item"))
    .setOreDictName("denseIngot")
    .build();
copper.registerPart(denseIngotPart); // 注册致密铜锭
```

### 创建匠魂材料

```zenscript
#loader contenttweaker
import mods.contenttweaker.tconstruct.MaterialBuilder;

var testMat as MaterialBuilder = MaterialBuilder.create("kindlich_mat");
testMat.color = 0x8e661b;
testMat.craftable = true;
testMat.castable = true;
testMat.liquid = <liquid:lava>;
testMat.localizedName = "Wicked";
testMat.representativeItem = <item:minecraft:red_flower:4>;
testMat.addItem(<item:minecraft:red_flower:4>);
testMat.addHeadMaterialStats(100, 1.5f, 5.5f, 5);
testMat.addHandleMaterialStats(0.3, 500);
testMat.addBowStringMaterialStats(0.5f);
testMat.addMaterialTrait("blasting", "bowstring");
testMat.addMaterialTrait("blasting", "head");
testMat.addMaterialTrait("dense");
testMat.register();
```

### 创建匠魂特性

```zenscript
#loader contenttweaker
import mods.contenttweaker.tconstruct.TraitBuilder;

var testTrait = TraitBuilder.create("kindlich_test");
testTrait.color = 0xffaadd;
testTrait.maxLevel = 100;
testTrait.countPerLevel = 20;
testTrait.addItem(<item:minecraft:iron_pickaxe>);
testTrait.addItem(<item:minecraft:iron_block>, 4, 2);
testTrait.localizedName = "实例特性";
testTrait.localizedDescription = "独创的特性!";
testTrait.afterHit = function(thisTrait, tool, attacker, target, damageDealt, wasCrit, wasHit) {
    if(!attacker.world.remote) {
        attacker.heal(damageDealt);
    }
};
testTrait.register();
```

---

## ZenUtils 扩展（需安装 ZenUtils）

> `import mods.zenutils.cotx.*;`

### ExpandVanillaFactory（工厂方法扩展）

对 `VanillaFactory` 的扩展。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `VanillaFactory.createEnergyItem(String, int, int, int)` | unlocalizedName, capacity, maxReceive, maxExtract | EnergyItem | 创建能量物品 |
| `VanillaFactory.createExpandBlock(String, IBlockMaterialDefinition)` | unlocalizedName, blockMaterial | ExpandBlock | 创建扩展方块 |
| `VanillaFactory.createExpandItem(String)` | unlocalizedName | ExpandItem | 创建扩展物品 |
| `VanillaFactory.createActualTileEntity(int)` | id | TileEntity | 创建自定义方块实体 |

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

### ExpandBlock（扩展方块）

> `import mods.zenutils.cotx.Block;`

继承 ContentTweaker 的 `BlockRepresentation`。

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `onBlockActivated` | IBlockActivated | null | 方块右键交互回调 |
| `onEntityWalk` | IEntityWalk | null | 实体踩踏回调 |
| `onEntityCollidedWithBlock` | IEntityCollided | null | 实体碰撞回调 |
| `tileEntity` | TileEntity | null | 关联的方块实体 |

#### IBlockActivated（函数式接口）

> `import mods.zenutils.cotx.IBlockActivated;`

| 参数 | 类型 |
|------|------|
| world | IWorld |
| pos | IBlockPos |
| state | ICTBlockState |
| player | ICTPlayer |
| hand | Hand |
| facing | Facing |
| blockHit | Position3f |

返回 `bool`。

#### IEntityWalk（函数式接口）

> `import mods.zenutils.cotx.IEntityWalk;`

参数：`IWorld`, `IBlockPos`, `IEntity`。返回 void。

#### IEntityCollided（函数式接口）

> `import mods.zenutils.cotx.IEntityCollided;`

参数：`IWorld`, `IBlockPos`, `ICTBlockState`, `IEntity`。返回 void。

### EnergyItem（能量物品）

> `import mods.zenutils.cotx.EnergyItem;`

继承 `ExpandItem`，无额外 ZenProperties。通过 `VanillaFactory.createEnergyItem` 创建。

### TileEntity（方块实体定义）

> `import mods.zenutils.cotx.TileEntity;`

用于定义自定义方块实体的行为。通过 `VanillaFactory.createActualTileEntity` 创建。

### TileEntityInGame（方块实体实例）

> `import mods.zenutils.cotx.TileEntityInGame;`
> 版本要求: 1.4.0+

表示游戏中的自定义方块实体实例。通过 `world.getCustomTileEntity(IBlockPos)` 获取。

| 属性 | 类型 | 读/写 | 说明 |
|------|------|------|------|
| `id` | int | 读 | 方块实体 ID |
| `data` | IData | 读/写 | 自定义数据 |

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `updateCustomData(IData)` | IData | void | 更新自定义数据 |

### LateSetCoTFunction（延迟设置函数）

> 版本要求: 1.8.0+

允许在 CraftTweaker 脚本中设置 ContentTweaker 物品/方块的函数（支持脚本重载）。

#### Bracket Handlers

| Bracket | 返回 | 说明 |
|------|------|------|
| `<cotItem:name>` | IItemRepresentation | 获取 ContentTweaker 物品 |
| `<cotBlock:name>` | IBlockRepresentation | 获取 ContentTweaker 方块 |

#### 可设置属性

| 属性 | 回调签名 | 说明 |
|------|------|------|
| `IItemRepresentation.onItemUse` | (player, world, pos, hand, facing, blockHit) → ActionResult | 物品使用回调 |

#### 静态方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `VanillaFactory.putTileEntityTickFunction(int, ITileEntityTick)` | id, tickFunction | void | 注册方块实体 tick 函数（可重载） |

```zenscript
#loader crafttweaker reloadable
import mods.zenutils.cotx.LateSetCoTFunction;

<cotItem:test_item>.onItemUse = function(player, world, pos, hand, facing, blockHit) {
    // 自定义物品使用逻辑
    return ActionResult.success();
};
```

---

## 常见错误

| 错误 | 原因 | 修复 |
|------|------|------|
| 脚本无效果 | 未添加 `#loader contenttweaker` | 在脚本第一行添加 |
| 物品/方块不显示 | 缺少材质文件 | 在 resources/contenttweaker/textures/ 下添加对应 png |
| 本地化名称不显示 | 缺少语言文件 | 添加 lang 文件或使用 displayName 赋值 |
| 材料部件不出现 | 未调用 addHeadMaterialStats 等方法 | 确保调用了对应的 add 方法 |

## 注意事项

- CoT 脚本必须以 `#loader contenttweaker` 开头
- 物品/方块 ID 必须全小写，字母开头，可含数字和下划线
- 注册后不可再修改属性
- 材质文件需放在 resources/contenttweaker/textures/ 对应目录
- 使用 `!world.remote` 确保事件只在服务端执行
