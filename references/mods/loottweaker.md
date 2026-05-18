# LootTweaker CraftTweaker API 参考

> Mod ID: `loottweaker`
> 前置条件: LootTableTweaker（移除功能需要）
> 导入: `import loottweaker.LootTweaker;`、`import mods.ltt.LootTable;`

用于修改战利品表的 API，支持添加和移除物品。

---

## API 列表

### LootTableTweaker（仅移除）

> `import mods.ltt.LootTable;`

只能移除，不能添加。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeTable(string table)` | 未说明 | 移除整个表 |
| `.removePool(string table, string pool)` | 未说明 | 移除池 |
| `.removeEntry(string table, string pool, string entry)` | 未说明 | 移除条目 |
| `.removeItem(string table, string pool, string itemid)` | 未说明 | 移除物品 |
| `.removeModEntry(string modid)` | 未说明 | 移除某 mod 所有条目 |
| `.removeModItem(string modid)` | 未说明 | 移除某 mod 所有物品 |
| `.removeModTable(string modtable)` | 未说明 | 移除某 mod 所有表 |
| `.removeGlobalItem(string itemid)` | 未说明 | 全局移除某物品 |

### LootTweaker（可添加和移除）

> `import loottweaker.LootTweaker;`

#### 获取/创建表

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getTable(string name)` | 未说明 | 获取已存在的战利品表 |
| `.newTable(string name)` | 未说明 | 创建新的战利品表 |

### LootTable（战利品表）

> 由 `LootTweaker.getTable()` 或 `LootTweaker.newTable()` 获取。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.clear()` | 未说明 | 清空所有物品 |
| `.addPool(string name, int minRolls, int maxRolls, int minBonus, int maxBonus)` | 未说明 | 创建池 |
| `.removePool(string name)` | 未说明 | 移除池 |
| `.getPool(string name)` | 未说明 | 获取池 |

### LootPool（战利品池）

> 由 `LootTable.addPool()` 或 `LootTable.getPool()` 获取。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeEntry(string name)` | 未说明 | 移除条目 |
| `.addItemEntry(IItemStack item, int weight)` | 未说明 | 添加物品条目 |
| `.addItemEntry(IItemStack item, int weight, string name)` | 未说明 | 带自定义名的物品条目 |
| `.addItemEntry(IItemStack item, int weight, int quality, string name)` | 未说明 | 带质量的物品条目 |
| `.addItemEntry(IItemStack item, int weight, int quality, funcs, conditions, string name)` | 未说明 | 完整形式的物品条目 |
| `.addLootTableEntry(string tableName, int weight)` | 未说明 | 嵌套表条目 |
| `.addEmptyEntry(int weight)` | 未说明 | 空条目 |
| `.setRolls(int min, int max)` | 未说明 | 设置抽取次数 |
| `.setBonusRolls(int min, int max)` | 未说明 | 设置奖励次数 |
| `.clearConditions()` | 未说明 | 清空条件 |
| `.clearEntries()` | 未说明 | 清空条目 |
| `.addConditions(conditions)` | 未说明 | 添加条件 |

### Conditions（条件）

> `import loottweaker.vanilla.loot.Conditions;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.randomChance(float chance)` | 未说明 | 随机几率 |
| `.randomChanceWithLooting(float chance, float multiplier)` | 未说明 | 带抢夺的随机几率 |
| `.killedByPlayer()` | 未说明 | 被玩家击杀 |
| `.killedByNonPlayer()` | 未说明 | 非玩家击杀 |
| `.parse(DataMap data)` | 未说明 | 从 JSON 解析条件 |
| `.zenscript(function)` | 未说明 | 自定义条件函数 |

### Functions（函数）

> `import loottweaker.vanilla.loot.Functions;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setCount(int min, int max)` | 未说明 | 设置数量 |
| `.setDamage(float min, float max)` | 未说明 | 设置耐久（max ≤ 1.0） |
| `.setMetadata(int min, int max)` | 未说明 | 设置 Meta |
| `.setNBT(DataMap data)` | 未说明 | 设置 NBT |
| `.enchantRandomly(String[] enchants)` | 未说明 | 随机附魔 |
| `.enchantWithLevels(int min, int max, bool treasure)` | 未说明 | 等级附魔 |
| `.lootingEnchantBonus(int min, int max, int limit)` | 未说明 | 抢夺加成 |
| `.smelt()` | 未说明 | 熔炼 |
| `.parse(DataMap data)` | 未说明 | 从 JSON 解析函数 |

### LootContext（上下文）

> `import loottweaker.LootContext;`

#### @ZenGetter

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
