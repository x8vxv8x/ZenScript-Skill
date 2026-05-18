# ContentTweaker 匠魂联动 CraftTweaker API 参考

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
