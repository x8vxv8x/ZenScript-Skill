# ContentTweaker 匠魂联动 API 参考

> 前置条件: ContentTweaker + Tinkers' Construct
> 导入: `import mods.contenttweaker.tconstruct.*;`

ContentTweaker 提供与匠魂 (Tinkers' Construct) 的联动 API，可自定义匠魂材料和特性。

**重要**: CoT 脚本第一行必须为 `#loader contenttweaker`。

---

## API 列表

### MaterialBuilder（TiC 材料构建器）

> `import mods.contenttweaker.tconstruct.MaterialBuilder;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.create(string)` | 材料 ID | MaterialBuilder | 创建材料构建器（静态方法） |
| `.color = int` | RGB 颜色 | - | 设置颜色 |
| `.craftable = bool` | 是否可制作 | - | 部件加工台可制作 |
| `.castable = bool` | 是否可铸造 | - | 冶炼炉可制作 |
| `.liquid = ILiquidStack` | 流体 | - | 设置流体 |
| `.representativeItem = IItemStack` | 物品 | - | 宝典显示物品 |
| `.addItem(IIngredient)` | 合成材料 | void | 添加合成材料 |
| `.addHeadMaterialStats(dur, speed, damage, level)` | 耐久, 速度, 伤害, 采掘等级 | void | 镐头属性 |
| `.addHandleMaterialStats(modifier, dur)` | 耐久修正, 耐久 | void | 手柄属性 |
| `.addExtraMaterialStats(dur)` | 耐久 | void | 额外部件属性 |
| `.addBowMaterialStats(draw, range, damage)` | 拉弦时间, 射程, 伤害 | void | 弓属性 |
| `.addBowStringMaterialStats(modifier)` | 耐久修正 | void | 弓弦属性 |
| `.addArrowShaftMaterialStats(modifier, bonus)` | 耐久修正, 箭数修正 | void | 箭杆属性 |
| `.addFletchingMaterialStats(accuracy, modifier)` | 精准度, 耐久修正 | void | 箭羽属性 |
| `.addProjectileMaterialStats()` | 无 | void | 投射物属性 |
| `.addMaterialTrait(string, @Optional string)` | 特性名, 部件类型 | void | 添加特性 |
| `.removeMaterialTrait(string, @Optional string)` | 特性名, 部件类型 | void | 移除特性 |
| `.register()` | 无 | void | 注册材料 |

### TraitBuilder（TiC 特性构建器）

> `import mods.contenttweaker.tconstruct.TraitBuilder;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.create(string)` | 特性 ID | TraitBuilder | 创建特性构建器（静态方法） |
| `.color = int` | RGB 颜色 | - | 设置颜色 |
| `.maxLevel = int` | 最高等级 | - | 最高等级 |
| `.countPerLevel = int` | 计数 | - | 升级所需计数 |
| `.localizedName = string` | 名称 | - | 本地化名称 |
| `.localizedDescription = string` | 描述 | - | 本地化描述 |
| `.addItem(IIngredient)` | 合成材料 | void | 添加合成材料 |
| `.register()` | 无 | void | 注册特性 |

### 可用特性函数

可在 TraitBuilder 上设置的回调函数：

| 函数 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.afterHit` | trait, tool, attacker, target, damage, wasCrit, wasHit | void | 攻击后 |
| `.onHit` | trait, tool, attacker, target, damage, isCritical | void | 攻击时 |
| `.onBlock` | trait, tool, attacker, event | void | 格挡时 |
| `.onPlayerHurt` | trait, tool, player, attacker, event | void | 受伤时 |
| `.onUpdate` | trait, tool, world, entity, slot, isSelected | void | 每 tick |
| `.getMiningSpeed` | trait, tool, event | void | 挖掘速度 |
| `.beforeBlockBreak` | trait, tool, event | void | 破坏方块前 |
| `.afterBlockBreak` | trait, tool, world, blockstate, pos, miner, wasEffective | void | 破坏方块后 |
| `.onBlockHarvestDrops` | trait, tool, event | void | 方块掉落时 |
| `.calcCrit` | trait, tool, attacker, target | bool | 计算暴击 |
| `.calcDamage` | trait, tool, attacker, target, orig, curr, isCrit | float | 计算伤害 |
| `.calcKnockBack` | trait, tool, attacker, target, dmg, kb, newKb, isCrit | float | 计算击退 |
| `.onToolDamage` | trait, tool, damage, newDamage, entity | int | 工具耐久损耗 |
| `.calcToolHeal` | trait, tool, damage, newDamage, entity | int | 工具修复 |
| `.onToolRepair` | trait, tool, amount | void | 修复工具时 |

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

## 注意事项

- 脚本第一行必须为 `#loader contenttweaker`
- 匠魂材料需配合匠魂模组使用
- 特性函数中的 `world.remote` 用于判断是否为客户端
