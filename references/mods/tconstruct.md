# 匠魂联动 CraftTweaker API 参考

> Mod ID: `contenttweaker`
> 前置条件: ContentTweaker + Tinkers' Construct
> 导入: `import mods.contenttweaker.tconstruct.*;`

ContentTweaker 提供与匠魂 (Tinkers' Construct) 的联动 API，可自定义匠魂材料和特性。

**重要**: CoT 脚本第一行必须为 `#loader contenttweaker`。

---

## API 列表

### MaterialBuilder（TiC 材料构建器）

> `import mods.contenttweaker.tconstruct.MaterialBuilder;`

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `.color` | int | RGB 颜色 |
| `.craftable` | bool | 部件加工台可制作 |
| `.castable` | bool | 冶炼炉可制作 |
| `.liquid` | ILiquidStack | 设置流体 |
| `.representativeItem` | IItemStack | 宝典显示物品 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(string name)` | 未说明 | 创建材料构建器（静态方法） |
| `.addItem(IIngredient ingredient)` | void | 添加合成材料 |
| `.addHeadMaterialStats(int dur, float speed, float damage, int level)` | void | 镐头属性（耐久, 速度, 伤害, 采掘等级） |
| `.addHandleMaterialStats(float modifier, int dur)` | void | 手柄属性（耐久修正, 耐久） |
| `.addExtraMaterialStats(int dur)` | void | 额外部件属性（耐久） |
| `.addBowMaterialStats(float draw, float range, float damage)` | void | 弓属性（拉弦时间, 射程, 伤害） |
| `.addBowStringMaterialStats(float modifier)` | void | 弓弦属性（耐久修正） |
| `.addArrowShaftMaterialStats(float modifier, int bonus)` | void | 箭杆属性（耐久修正, 箭数修正） |
| `.addFletchingMaterialStats(float accuracy, float modifier)` | void | 箭羽属性（精准度, 耐久修正） |
| `.addProjectileMaterialStats()` | void | 投射物属性 |
| `.addMaterialTrait(string trait, @Optional string partType)` | void | 添加特性 |
| `.removeMaterialTrait(string trait, @Optional string partType)` | void | 移除特性 |
| `.register()` | void | 注册材料 |

### TraitBuilder（TiC 特性构建器）

> `import mods.contenttweaker.tconstruct.TraitBuilder;`

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `.color` | int | RGB 颜色 |
| `.maxLevel` | int | 最高等级 |
| `.countPerLevel` | int | 升级所需计数 |
| `.localizedName` | string | 本地化名称 |
| `.localizedDescription` | string | 本地化描述 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(string name)` | 未说明 | 创建特性构建器（静态方法） |
| `.addItem(IIngredient ingredient)` | void | 添加合成材料 |
| `.register()` | void | 注册特性 |

### 可用特性函数

可在 TraitBuilder 上设置的回调函数：

| 函数 | 返回 | 说明 |
|------|------|------|
| `.afterHit` | void | 攻击后（参数: trait, tool, attacker, target, damage, wasCrit, wasHit） |
| `.onHit` | void | 攻击时（参数: trait, tool, attacker, target, damage, isCritical） |
| `.onBlock` | void | 格挡时（参数: trait, tool, attacker, event） |
| `.onPlayerHurt` | void | 受伤时（参数: trait, tool, player, attacker, event） |
| `.onUpdate` | void | 每 tick（参数: trait, tool, world, entity, slot, isSelected） |
| `.getMiningSpeed` | void | 挖掘速度（参数: trait, tool, event） |
| `.beforeBlockBreak` | void | 破坏方块前（参数: trait, tool, event） |
| `.afterBlockBreak` | void | 破坏方块后（参数: trait, tool, world, blockstate, pos, miner, wasEffective） |
| `.onBlockHarvestDrops` | void | 方块掉落时（参数: trait, tool, event） |
| `.calcCrit` | bool | 计算暴击（参数: trait, tool, attacker, target） |
| `.calcDamage` | float | 计算伤害（参数: trait, tool, attacker, target, orig, curr, isCrit） |
| `.calcKnockBack` | float | 计算击退（参数: trait, tool, attacker, target, dmg, kb, newKb, isCrit） |
| `.onToolDamage` | int | 工具耐久损耗（参数: trait, tool, damage, newDamage, entity） |
| `.calcToolHeal` | int | 工具修复（参数: trait, tool, damage, newDamage, entity） |
| `.onToolRepair` | void | 修复工具时（参数: trait, tool, amount） |

---

## 使用示例

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

---

## 注意事项

- CoT 脚本必须以 `#loader contenttweaker` 开头
- 材料 ID 必须全小写，字母开头，可含数字和下划线
- 注册后不可再修改属性
- 材质文件需放在 resources/contenttweaker/textures/ 对应目录

---

## ZenTraits 扩展（需安装 ZenTraits）

> `import zentraits.TraitManager;`

ZenTraits 允许通过脚本动态附加/移除已有匠魂材料的特性。

### TraitManager（特性管理器）

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `TraitManager.attachTrait(string materialID, string traitID, @Optional string partType)` | 未说明 | 为材料附加特性。`partType` 可选，留空则作为默认特性。注意：为原本没有部件特性的材料添加部件特性会替换默认特性 |
| `TraitManager.detachTrait(string materialID, string traitID, @Optional string partType)` | 未说明 | 从材料移除特性 |
| `TraitManager.detachAllTraits(string materialID, @Optional string partType)` | 未说明 | 移除材料的所有特性 |

### 命令

| 命令 | 说明 |
|------|------|
| `/ct ztdumpmats` | 将材料信息输出到 CraftTweaker 日志 |
| `/ct ztdumptraits` | 将特性信息输出到 CraftTweaker 日志 |

### 默认部件类型

**匠魂（TiC）**：`head`、`handle`、`extra`、`bow`、`bowstring`、`projectile`、`shaft`、`fletching`

**匠魂护甲（Conarm）**：`core`、`trim`、`plate`

### 默认特性 ID

#### 通用特性

| 特性 ID | 特性 ID | 特性 ID |
|---------|---------|---------|
| `alien` | `aquadynamic` | `aridiculous` |
| `autosmelt` | `baconlicious` | `cheap` |
| `cheapskate` | `coldblooded` | `crude` |
| `crude2` | `crumbling` | `dense` |
| `depthdigger` | `duritos` | `ecological` |
| `enderference` | `established` | `flammable` |
| `fractured` | `heavy` | `hellish` |
| `holy` | `insatiable` | `jagged` |
| `lightweight` | `magnetic` | `magnetic2` |
| `momentum` | `petramor` | `poisonous` |
| `prickly` | `sharp` | `shocking` |
| `slimeyGreen` | `slimeyBlue` | `spiky` |
| `splintering` | `splinters` | `squeaky` |
| `superheat` | `stiff` | `stonebound` |
| `tasty` | `unnatural` | `writable` |
| `writable2` | | |

#### 箭杆特性

`breakable`、`endspeed`、`freezing`、`hovering`、`splitting`

### 使用示例

```zenscript
import zentraits.TraitManager;

// 为石头添加默认特性 "sharp"
TraitManager.attachTrait("stone", "sharp");

// 为铁的头部部件添加特性 "magnetic"
TraitManager.attachTrait("iron", "magnetic", "head");

// 从石头移除 "cheap" 默认特性
TraitManager.detachTrait("stone", "cheap");

// 移除木头的所有特性
TraitManager.detachAllTraits("wood");
```

---

## Modtweaker 配方处理器（需安装 Modtweaker）

> `import mods.tconstruct.*;`

### Alloying（合金）

> `import mods.tconstruct.Alloy;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, ILiquidStack[] inputs)` | void | 添加合金配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(ILiquidStack output)` | void | 按输出移除配方 |
| `.removeRecipe(ILiquidStack output, ILiquidStack[] inputs)` | void | 按输入输出移除配方 |

### Casting（浇铸）

> `import mods.tconstruct.Casting;`

#### 浇铸台配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addTableRecipe(IItemStack output, IIngredient cast, ILiquidStack fluid, int amount, @Optional boolean consumeCast, @Optional int time)` | void | 添加浇铸台配方。`cast` 模具。`amount` 流体量(mB)。`consumeCast` 是否消耗模具 |
| `.removeTableRecipe(IItemStack output)` | void | 按输出移除浇铸台配方 |
| `.removeTableRecipe(IItemStack output, ILiquidStack input)` | void | 按输入输出移除 |

#### 铸造盆配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addBasinRecipe(IItemStack output, IIngredient cast, ILiquidStack fluid, int amount, @Optional boolean consumeCast, @Optional int time)` | void | 添加铸造盆配方 |
| `.removeBasinRecipe(IItemStack output)` | void | 按输出移除铸造盆配方 |
| `.removeBasinRecipe(IItemStack output, ILiquidStack input)` | void | 按输入输出移除 |

### Melting（熔炼）

> `import mods.tconstruct.Melting;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, IIngredient input, @Optional int temp)` | void | 添加熔炼配方。`temp` 可选温度 |
| `.addEntityMelting(IEntityDefinition entity, ILiquidStack stack)` | void | 添加实体熔炼配方（可直接覆盖已有配方） |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(ILiquidStack output)` | void | 按输出移除配方 |
| `.removeRecipe(ILiquidStack output, IItemStack input)` | void | 按输入输出移除配方 |
| `.removeEntityMelting(IEntityDefinition entity)` | void | 移除实体熔炼配方 |

### Drying（晾干架）

> `import mods.tconstruct.Drying;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input, int time)` | void | 添加晾干配方。`time` 为时间(tick) |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 按输出移除配方 |
| `.removeRecipe(IItemStack output, IItemStack input)` | void | 按输入输出移除配方 |

### Fuel（冶炼炉燃料）

> `import mods.tconstruct.Fuel;`

#### 燃料注册方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerFuel(ILiquidStack fuel, int duration)` | void | 注册冶炼炉燃料。`fuel` 的 amount 为最小消耗增量。`duration` 为消耗一次持续的 tick 数 |

**注意**: 无法通过此 API 设置流体温度，需使用 `ILiquidDefinition` 的 ZenSetter 预先修改流体温度。

### Modtweaker 使用示例

```zenscript
import mods.tconstruct.Alloy;
import mods.tconstruct.Casting;
import mods.tconstruct.Melting;
import mods.tconstruct.Drying;
import mods.tconstruct.Fuel;

// 合金配方
Alloy.addRecipe(<liquid:water> * 10, [<liquid:lava> * 10, <liquid:molten_iron> * 5]);

// 浇铸台配方
Casting.addTableRecipe(<minecraft:gold_ingot>, <minecraft:gold_ingot>, <liquid:molten_gold>, 140);

// 熔炼配方
Melting.addRecipe(<liquid:molten_gold> * 144, <minecraft:gold_ingot>);

// 晾干架配方
Drying.addRecipe(<minecraft:leather>, <minecraft:rotten_flesh>, 100);

// 冶炼炉燃料
Fuel.registerFuel(<liquid:water> * 2, 300);
```
