# LootTweaker 战利品表 API

需要安装 LootTweaker 和 LootTableTweaker 附加模组。

## LootTableTweaker（只能移除）

> `import mods.ltt.LootTable;`

```zenscript
LootTable.removeTable("table");           // 移除整个表
LootTable.removePool("table", "pool");    // 移除池
LootTable.removeEntry("table", "pool", "entry");  // 移除条目
LootTable.removeItem("table", "pool", "itemid");  // 移除物品
LootTable.removeModEntry("modid");        // 移除某 mod 所有条目
LootTable.removeModItem("modid");         // 移除某 mod 所有物品
LootTable.removeModTable("modtable");     // 移除某 mod 所有表
LootTable.removeGlobalItem("itemid");     // 全局移除某物品
```

## LootTweaker（可添加和移除）

> `import loottweaker.LootTweaker;`

### 获取/创建表

```zenscript
val table = LootTweaker.getTable("minecraft:entities/pig");
val newTable = LootTweaker.newTable("mypack:custom_table");
```

### LootTable 方法

| 方法 | 说明 |
|------|------|
| `.clear()` | 清空所有物品 |
| `.addPool(name, minRolls, maxRolls, minBonus, maxBonus)` | 创建池 |
| `.removePool(name)` | 移除池 |
| `.getPool(name)` | 获取池 |

### LootPool 方法

| 方法 | 说明 |
|------|------|
| `.removeEntry(name)` | 移除条目 |
| `.addItemEntry(IItemStack, weight)` | 添加物品条目 |
| `.addItemEntry(IItemStack, weight, name)` | 带自定义名 |
| `.addItemEntry(IItemStack, weight, quality, name)` | 带质量 |
| `.addItemEntry(IItemStack, weight, quality, funcs, conditions, name)` | 完整形式 |
| `.addLootTableEntry(tableName, weight)` | 嵌套表 |
| `.addEmptyEntry(weight)` | 空条目 |
| `.setRolls(min, max)` | 设置抽取次数 |
| `.setBonusRolls(min, max)` | 设置奖励次数 |
| `.clearConditions()` | 清空条件 |
| `.clearEntries()` | 清空条目 |
| `.addConditions(conditions)` | 添加条件 |

### Conditions（条件）

> `import loottweaker.vanilla.loot.Conditions;`

| 方法 | 说明 |
|------|------|
| `Conditions.randomChance(float)` | 随机几率 |
| `Conditions.randomChanceWithLooting(float, float)` | 带抢夺的随机几率 |
| `Conditions.killedByPlayer()` | 被玩家击杀 |
| `Conditions.killedByNonPlayer()` | 非玩家击杀 |
| `Conditions.parse(DataMap)` | 从 JSON 解析 |
| `Conditions.zenscript(function)` | 自定义条件函数 |

### Functions（函数）

> `import loottweaker.vanilla.loot.Functions;`

| 方法 | 说明 |
|------|------|
| `Functions.setCount(min, max)` | 设置数量 |
| `Functions.setDamage(min, max)` | 设置耐久（max ≤ 1.0） |
| `Functions.setMetadata(min, max)` | 设置 Meta |
| `Functions.setNBT(DataMap)` | 设置 NBT |
| `Functions.enchantRandomly(String[])` | 随机附魔 |
| `Functions.enchantWithLevels(min, max, treasure)` | 等级附魔 |
| `Functions.lootingEnchantBonus(min, max, limit)` | 抢夺加成 |
| `Functions.smelt()` | 熔炼 |
| `Functions.parse(DataMap)` | 从 JSON 解析 |

### LootContext（上下文）

> `import loottweaker.LootContext;`

| 属性 | 类型 | 说明 |
|------|------|------|
| `.lootedEntity()` | IEntity | 被击杀实体 |
| `.killerPlayer()` | IPlayer | 击杀玩家 |
| `.killer()` | IEntity | 击杀者 |
| `.luck()` | float | 幸运值 |
| `.world()` | IWorld | 世界 |
| `.lootingModifier()` | int | 抢夺等级 |

---

## 使用示例

### 移除物品

```zenscript
import loottweaker.LootTweaker;

LootTweaker.getTable("minecraft:entities/pig")
    .getPool("main")
    .removeEntry("minecraft:porkchop");
```

### 添加物品

```zenscript
import loottweaker.LootTweaker;

val cow = LootTweaker.getTable("minecraft:entities/cow");
cow.addPool("extra", 1, 1, 0, 0)
   .addItemEntry(<minecraft:apple>, 5);
```

### 带条件和函数

```zenscript
import loottweaker.LootTweaker;
import loottweaker.vanilla.loot.Conditions;
import loottweaker.vanilla.loot.Functions;

val pool = LootTweaker.getTable("minecraft:entities/zombie")
    .addPool("diamond_drop", 1, 1, 0, 0);
pool.addItemEntry(<minecraft:diamond>, 10);
pool.addConditions([Conditions.randomChance(0.01)]);
```

---

## 原版战利品表 ID

### 箱子

```
minecraft:chests/abandoned_mineshaft
minecraft:chests/desert_pyramid
minecraft:chests/end_city_treasure
minecraft:chests/igloo_chest
minecraft:chests/jungle_temple
minecraft:chests/jungle_temple_dispenser
minecraft:chests/nether_bridge
minecraft:chests/simple_dungeon
minecraft:chests/spawn_bonus_chest
minecraft:chests/stronghold_corridor
minecraft:chests/stronghold_crossing
minecraft:chests/stronghold_library
minecraft:chests/village_blacksmith
minecraft:chests/woodland_mansion
```

### 实体

```
minecraft:entities/cow
minecraft:entities/pig
minecraft:entities/sheep
minecraft:entities/zombie
minecraft:entities/skeleton
minecraft:entities/creeper
minecraft:entities/spider
minecraft:entities/enderman
// ... 大部分实体都有对应表
```

### 命令查询

```
/ct loottables all      // 列出所有表
/ct loottables list     // 列出表名
/ct loottables target   // 查看目标实体的表
/ct loottables byName <name>  // 按名称查看
```

> 注意：箱子战利品表在打开后会被删除，查询前不要打开箱子。
