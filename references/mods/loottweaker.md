# LootTweaker CraftTweaker API 参考

> Mod ID: `loottweaker`
> 前置条件: 无
> 导入: `import loottweaker.LootTweaker;`

用于修改 Minecraft 战利品表（Loot Table）的 CraftTweaker 附加模组。支持获取、创建、修改战利品表及其池和条目。

---

## API 列表

### LootTweaker（入口类）

> `import loottweaker.LootTweaker;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getTable(String tableName)` | LootTable | 获取指定名称的战利品表。若表不存在则报错 |
| `.newTable(String tableName)` | LootTable | 创建新的空战利品表。表名不应使用 `minecraft` 或 `loottweaker` 作为命名空间，若使用 `minecraft` 命名空间会产生警告 |
| `.createLootGenerator(IWorld world)` | LootGenerator | 创建战利品生成器，必须传入服务端世界（`world.remote` 为 false） |

**表名格式**: `namespace:path`，如 `minecraft:entities/cow`、`examplepack:chests/my_chest`

---

### LootTable（战利品表）

> 由 `LootTweaker.getTable()` 或 `LootTweaker.newTable()` 获取。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.clear()` | void | 清空表中所有池（包括脚本新增的池） |
| `.addPool(String poolName, float minRolls, float maxRolls, float minBonusRolls, float maxBonusRolls)` | LootPool | 添加新池并返回。池名在表内必须唯一，若已存在同名池则报错 |
| `.removePool(String poolName)` | void | 移除指定池。若不存在则报错 |
| `.getPool(String poolName)` | LootPool | 获取指定池。若不存在则报错 |

**默认池名**: 第一个未命名池为 `main`，后续为 `pool1`、`pool2`……依此类推。

---

### LootPool（战利品池）

> 由 `LootTable.addPool()` 添加或 `LootTable.getPool()` 获取。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeEntry(String entryName)` | void | 移除指定条目。若不存在则报错 |
| `.addItemEntry(IItemStack stack, int weight, int quality, LootFunction[] functions, LootCondition[] conditions, @Optional String name)` | void | 添加物品条目（完整形式）。weight 越高生成概率越大；quality 影响幸运值对概率的加成；LootTweaker 会根据 stack 自动生成 set_nbt、set_damage/set_data、set_count 函数（除非 functions 中已有同类函数）；name 可选，需在池内唯一 |
| `.addItemEntry(IItemStack stack, int weight, int quality, @Optional String name)` | void | 添加物品条目（无条件和函数） |
| `.addItemEntry(IItemStack stack, int weight, @Optional String name)` | void | 添加物品条目（无条件、无函数、quality 为 0） |
| `.addLootTableEntry(String tableName, int weight, int quality, LootCondition[] conditions, @Optional String name)` | void | 添加嵌套战利品表条目，生成时从另一张表抽取物品 |
| `.addLootTableEntry(String tableName, int weight, int quality, @Optional String name)` | void | 添加嵌套战利品表条目（无条件） |
| `.addLootTableEntry(String tableName, int weight, @Optional String name)` | void | 添加嵌套战利品表条目（无条件、quality 为 0） |
| `.addEmptyEntry(int weight, int quality, LootCondition[] conditions, @Optional String name)` | void | 添加空条目（不生成物品，用于降低实际生成概率） |
| `.addEmptyEntry(int weight, int quality, @Optional String name)` | void | 添加空条目（无条件） |
| `.addEmptyEntry(int weight, @Optional String name)` | void | 添加空条目（无条件、quality 为 0） |
| `.setRolls(float min, float max)` | void | 设置池的抽取次数范围 |
| `.setBonusRolls(float min, float max)` | void | 设置池的奖励抽取次数范围（受幸运值影响） |
| `.addConditions(LootCondition[] conditions)` | void | 为池添加条件。JSON 格式 Map 会自动转换为 LootCondition |
| `.clearConditions()` | void | 清空池的所有条件（不影响子条目上的条件） |
| `.clearEntries()` | void | 清空池的所有条目 |

**权重与概率**: 条目生成概率 = 该条目有效权重 / 池内所有条目有效权重之和。有效权重 = `floor(weight + quality * luck)`。luck 默认为 0。

---

### Conditions（条件工厂）

> `import loottweaker.Conditions;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.randomChance(float chance)` | LootCondition | 随机几率，chance 为 0.0~1.0 |
| `.randomChanceWithLooting(float chance, float lootingMult)` | LootCondition | 带抢夺附魔加成的随机几率。实际几率 = chance + 抢夺等级 × lootingMult |
| `.killedByPlayer()` | LootCondition | 被玩家击杀时触发 |
| `.killedByNonPlayer()` | LootCondition | 非玩家击杀时触发（反向的 killed_by_player） |
| `.zenscript(CustomLootCondition zenFunction)` | LootCondition | 自定义 ZenScript 条件。函数签名：`(IRandom rng, LootContext context) → boolean` |
| `.parse(DataMap json)` | LootCondition | **已废弃 (0.3.0)**，JSON Map 现在会自动转换，直接传递即可 |

---

### Functions（函数工厂）

> `import loottweaker.Functions;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setCount(int min, int max)` | LootFunction | 设置物品数量范围 |
| `.setDamage(float min, float max)` | LootFunction | 设置物品损坏值范围（0.0~1.0，max 不可超过 1.0） |
| `.setMetadata(int min, int max)` | LootFunction | 设置物品元数据范围 |
| `.setNBT(DataMap nbtData)` | LootFunction | 设置 NBT 数据，必须为复合标签 |
| `.enchantRandomly(String[] enchantIDList)` | LootFunction | 随机附魔。enchantIDList 为附魔 ID 数组，如 `["minecraft:looting"]` |
| `.enchantWithLevels(int min, int max, boolean isTreasure)` | LootFunction | 按等级附魔。isTreasure 为 true 时允许宝藏附魔 |
| `.lootingEnchantBonus(int min, int max, int limit)` | LootFunction | 抢夺附魔加成。每级抢夺增加 min~max 个物品，上限为 limit |
| `.smelt()` | LootFunction | 熔炼效果（如生肉变熟肉） |
| `.zenscript(CustomLootFunction zenFunction)` | LootFunction | 自定义 ZenScript 函数。函数签名：`(IItemStack input, IRandom rng, LootContext context) → IItemStack` |
| `.parse(DataMap json)` | LootFunction | **已废弃 (0.3.0)**，JSON Map 现在会自动转换，直接传递即可 |

---

### LootCondition（条件实例）

> `import loottweaker.LootCondition;`
> 由 `Conditions` 工厂方法创建，或由 JSON Map 自动转换。

此类型无额外方法，仅作为参数传递给 `LootPool.addConditions()`、`LootPool.addItemEntry()` 等方法。

---

### LootFunction（函数实例）

> `import loottweaker.LootFunction;`
> 由 `Functions` 工厂方法创建，或由 JSON Map 自动转换。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addConditions(LootCondition[] conditions)` | LootFunction | 为此函数添加执行条件。返回自身，支持链式调用 |

---

### LootContext（战利品生成上下文）

> `import loottweaker.LootContext;`
> 用于自定义条件/函数中获取生成上下文信息。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `.lootedEntity()` | IEntity | 被掠夺的实体（可能为 null） |
| `.killerPlayer()` | IPlayer | 触发生成的玩家（可能为 null） |
| `.killer()` | IEntity | 触发生成的实体（可能为 null） |
| `.luck()` | float | 当前幸运值 |
| `.world()` | IWorld | 战利品生成所在的世界 |
| `.lootingModifier()` | int | 抢夺附魔等级 |

---

### LootGenerator（战利品生成器）

> `import loottweaker.LootGenerator;`
> 由 `LootTweaker.createLootGenerator(IWorld)` 创建。可复用对象，上下文设置不会在生成后重置。

#### 方法（支持链式调用）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.luck(float luck)` | LootGenerator | 设置幸运值 |
| `.lootedEntity(IEntity entity)` | LootGenerator | 设置被掠夺实体 |
| `.player(IPlayer player)` | LootGenerator | 设置触发玩家 |
| `.damageSource(IDamageSource damageSource)` | LootGenerator | 设置击杀伤害源 |
| `.generate(String tableId)` | IItemStack[] | 从指定战利品表生成物品并返回物品数组 |
| `.generateInto(String tableId, IEntity entity, @Optional String face, @Optional String overflow)` | void | 将生成的物品直接放入实体的背包。face 为 `"NONE"`/`"TOP"`/`"BOTTOM"`/`"NORTH"`/`"EAST"`/`"SOUTH"`/`"WEST"`；overflow 为 `"VOID"`（丢弃多余）或 `"DROP"`（掉落多余） |
| `.generateInto(String tableId, IBlockPos pos, @Optional String face, @Optional String overflow)` | void | 将生成的物品直接放入方块容器。参数同上 |

---

## JSON 格式 Map 自动转换

自 0.3.0 起，LootTweaker 方法中所有 `LootCondition` 和 `LootFunction` 参数均接受 JSON 格式 Map，会自动转换。JSON 中的键建议用双引号包裹，避免与 ZenScript 关键字冲突（如 `function`）。

```zenscript
// 等价写法
pool.addItemEntry(<minecraft:potato>, 1, 0, [], [Conditions.killedByPlayer()]);
pool.addItemEntry(<minecraft:potato>, 1, 0, [], [{"condition": "killed_by_player"}]);
```

---

## 自动 NBT/数量/元数据处理

LootTweaker 接受 `IItemStack` 的方法会自动保留该物品的 metadata、NBT 和数量。具体机制为自动生成对应的 `set_damage`、`set_data`、`set_count` 函数。若 `functions` 参数中已有同类函数则跳过自动生成。

```zenscript
// 以下两种写法等价
pool.addItemEntry(<minecraft:apple> * 2, 1);
pool.addItemEntry(<minecraft:apple>, 1, 1, [Functions.setCount(2, 2)], []);
```

---

## 使用示例

### 移除物品

```zenscript
import loottweaker.LootTweaker;

// 移除猪掉落的猪排
LootTweaker.getTable("minecraft:entities/pig")
    .getPool("main")
    .removeEntry("minecraft:porkchop");
```

### 添加物品到新池

```zenscript
import loottweaker.LootTweaker;

// 给牛的掉落表添加一个新池，必定掉落一个苹果
val cow = LootTweaker.getTable("minecraft:entities/cow");
val extra = cow.addPool("extra", 1, 1, 0, 0);
extra.addItemEntry(<minecraft:apple>, 5);
```

### 带条件的掉落

```zenscript
import loottweaker.LootTweaker;
import loottweaker.Conditions;

// 只有被玩家击杀时才掉落钻石
val pool = LootTweaker.getTable("minecraft:entities/zombie")
    .addPool("diamond_drop", 1, 1, 0, 0);
pool.addItemEntry(<minecraft:diamond>, 10, 1, [], [Conditions.killedByPlayer()]);
```

### 使用函数修改掉落物

```zenscript
import loottweaker.LootTweaker;
import loottweaker.Functions;

// 掉落 2~5 个胡萝卜
val pool = LootTweaker.getTable("minecraft:entities/zombie")
    .addPool("carrot_drop", 1, 1, 0, 0);
pool.addItemEntry(<minecraft:carrot>, 20, 1, [Functions.setCount(2, 5)], []);
```

### 使用自定义 ZenScript 条件和函数

```zenscript
import crafttweaker.util.IRandom;
import crafttweaker.item.IItemStack;
import loottweaker.LootTweaker;
import loottweaker.LootContext;
import loottweaker.Conditions;
import loottweaker.Functions;

val pool = LootTweaker.getTable("minecraft:entities/cow")
    .addPool("custom", 1, 1, 0, 0);

// 自定义条件：下雨天时生效
pool.addItemEntry(<minecraft:apple>, 10, 1, [], [
    Conditions.zenscript(function(rng as IRandom, context as LootContext) as boolean {
        return context.world().isRaining();
    })
]);

// 自定义函数：给物品加显示名
pool.addItemEntry(<minecraft:potato>, 10, 1, [
    Functions.zenscript(function(input as IItemStack, rng as IRandom, context as LootContext) as IItemStack {
        return input.withDisplayName("Super Potato");
    })
], []);
```

### 使用 LootGenerator 程序化生成战利品

```zenscript
import loottweaker.LootTweaker;

if (!world.remote) {
    val generator = LootTweaker.createLootGenerator(world)
        .luck(2.0)
        .player(somePlayer);
    for item in generator.generate("minecraft:entities/cow") {
        print(item);
    }
}
```

### 完整示例（来自官方文档）

```zenscript
import loottweaker.LootTweaker;
import loottweaker.LootTable;
import loottweaker.LootPool;
import loottweaker.Conditions;
import loottweaker.Functions;

// 获取羊的战利品表
val sheep = LootTweaker.getTable("minecraft:entities/sheep");

// 获取主池
val main = sheep.getPool("main");

// 添加新池
val sweetLoot = sheep.addPool("sweetLoot", 1, 1, 1, 1);

// 移除羊肉、修改抽取次数
main.removeEntry("minecraft:mutton");
main.setRolls(3, 6);
main.setBonusRolls(0, 2);

// 被玩家击杀时掉落 3 个苹果
sweetLoot.addItemEntry(<minecraft:apple> * 3, 20, 1, [], [Conditions.killedByPlayer()]);
// 被玩家击杀时掉落 4 根木棍（使用 JSON 条件）
sweetLoot.addItemEntry(<minecraft:stick> * 4, 20, 1, [], [{"condition": "killed_by_player"}]);
// 被玩家击杀且着火时掉落 1 个土豆
sweetLoot.addItemEntry(<minecraft:potato>, 20, 1, [], [
    {"condition": "entity_properties", "entity": "this", "properties": {"on_fire": true}},
    Conditions.killedByPlayer()
]);
// 掉落 2~5 个胡萝卜
sweetLoot.addItemEntry(<minecraft:carrot>, 20, 1, [Functions.setCount(2, 5)], []);
// 掉落 3~9 个红石（使用 JSON 函数）
sweetLoot.addItemEntry(<minecraft:redstone>, 20, 1, [{"count": {"min": 3.0, "max": 9.0}, "function": "minecraft:set_count"}], []);
// 掉落 1~3 把铁剑，10%~15% 损坏
sweetLoot.addItemEntry(<minecraft:iron_sword>, 20, 1, [
    {"count": {"min": 1.0, "max": 3.0}, "function": "minecraft:set_count"},
    Functions.setDamage(0.10, 0.15)
], []);

// 添加引用猪掉落表的嵌套条目
val pigLoot = sheep.addPool("pigLoot", 1, 1, 1, 1);
pigLoot.addLootTableEntry("minecraft:entities/pig", 40);
// 非玩家击杀时生效
pigLoot.addConditions([Conditions.killedByNonPlayer()]);
```

---

## 战利品表命名规则（Forge 格式）

- Forge 要求池和条目必须有名称
- **池名**在表内必须唯一；**条目名**在池内必须唯一
- LootTweaker 添加条目时会自动生成唯一名称，无需手动指定
- 但通过 LootTweaker 添加的池名必须手动确保唯一
- 未指定名称时的默认值：
  - 物品/方块条目 → 物品/方块的注册名
  - 战利品表条目 → 引用的表名
  - 空条目 → `"empty"`
  - 池 → 第一个为 `main`，后续为 `pool1`、`pool2`……

---

## 命令

| 命令 | 说明 |
|------|------|
| `/ct loottables list` | 列出所有内置战利品表 |
| `/ct loottables all` | 将所有表导出为 JSON 到 `dumps/` 目录 |
| `/ct loottables byName <表名>` | 导出指定表 |
| `/ct loottables target` | 导出玩家视线所指对象的战利品表 |
| `/ct loottables generate chest <表名>` | 在玩家视线位置用指定表生成一个箱子 |
| `/ct loottables generate entity <表名> <实体ID> [NBT]` | 在玩家视线位置生成实体，箱子矿车会在背包中生成物品，其他实体死亡时掉落 |

导出路径：`<minecraft根目录>/dumps/loot_tables/<namespace>/<path>.json`

---

## 注意事项

- LootTweaker 无法 dump 自身通过 `newTable()` 创建的表，需查看存档的 `data/loot_tables` 文件夹
- 并非所有实体都有战利品表（如凋灵），可安装 "More Loot Tables" 模组补充
- `setDamage` 的 max 参数不可超过 1.0
- 废弃警告可在 LootTweaker 配置中关闭，但版本更新时配置会重置
- 旧版 `loottweaker.vanilla.loot.Conditions` / `loottweaker.vanilla.loot.Functions` 导入路径已在 0.3.3 移除，必须使用 `loottweaker.Conditions` / `loottweaker.Functions`
