# Dropt CraftTweaker API 参考

> Mod ID: `dropt`
> 前置条件: 无
> 导入: `import mods.dropt.Dropt;`
> 提供嵌套链式的 builder 方法，请一定参考下方使用示例

Dropt 是一个灵活的方块掉落替换系统，支持多条件匹配、加权掉落、时运修正等。

---

## API 列表

### Dropt（工厂类）

> `import mods.dropt.Dropt;`

工厂类，用于创建其他对象。

#### 工厂方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.list(string name)` | 未说明 | 创建/获取规则列表 |
| `.rule()` | 未说明 | 创建规则 |
| `.harvester()` | 未说明 | 创建采集者匹配 |
| `.drop()` | 未说明 | 创建掉落物定义 |
| `.range(int fixed)` | 未说明 | 固定数量范围 |
| `.range(int min, int max)` | 未说明 | 区间数量范围 |
| `.weight(int weight)` | 未说明 | 权重 |
| `.weight(int weight, int fortuneMod)` | 未说明 | 带时运修正的权重 |

### RuleList（规则列表）

> `import mods.dropt.RuleList;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.priority(int priority)` | 未说明 | 设置优先级（越大越先匹配，默认 0） |
| `.add(Rule rule)` | 未说明 | 添加规则 |

### Rule（规则）

> `import mods.dropt.Rule;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.debug()` | 未说明 | 启用调试日志 |
| `.matchBlocks(string[] blocks)` | 未说明 | 匹配方块（白名单） |
| `.matchBlocks(string type, string[] blocks)` | 未说明 | 匹配方块，type: "WHITELIST"/"BLACKLIST" |
| `.matchDrops(IIngredient[] drops)` | 未说明 | 匹配掉落物（白名单） |
| `.matchDrops(string type, IIngredient[] drops)` | 未说明 | 匹配掉落物，type: "WHITELIST"/"BLACKLIST" |
| `.matchHarvester(Harvester harvester)` | 未说明 | 匹配采集者 |
| `.matchBiomes(string[] biomes)` | 未说明 | 匹配生物群系（白名单） |
| `.matchBiomes(string type, string[] biomes)` | 未说明 | 匹配生物群系，type: "WHITELIST"/"BLACKLIST" |
| `.matchDimensions(int[] dimensions)` | 未说明 | 匹配维度 ID（白名单） |
| `.matchDimensions(string type, int[] dimensions)` | 未说明 | 匹配维度，type: "WHITELIST"/"BLACKLIST" |
| `.matchVerticalRange(int min, int max)` | 未说明 | 匹配高度范围 |
| `.matchSpawnDistance(int min, int max)` | 未说明 | 匹配出生点距离（白名单） |
| `.matchSpawnDistance(string type, int min, int max)` | 未说明 | 匹配出生点距离，type: "WHITELIST"/"BLACKLIST" |
| `.replaceStrategy(string strategy)` | 未说明 | 设置替换策略 |
| `.dropStrategy(string strategy)` | 未说明 | 设置掉落策略 |
| `.dropCount(Range count)` | 未说明 | 设置选择器执行次数 |
| `.addDrop(Drop drop)` | 未说明 | 添加掉落 |
| `.fallthrough(bool value)` | 未说明 | 是否继续匹配后续规则 |

#### 替换策略

| 策略 | 说明 |
|------|------|
| `REPLACE_ALL` | 替换所有掉落（默认） |
| `REPLACE_ALL_IF_SELECTED` | 选中时替换所有 |
| `REPLACE_ITEMS` | 只替换匹配的掉落 |
| `REPLACE_ITEMS_IF_SELECTED` | 选中时替换匹配的 |
| `ADD` | 追加到现有掉落 |

#### 掉落策略

| 策略 | 说明 |
|------|------|
| `REPEAT` | 同一掉落可被选中多次（默认） |
| `UNIQUE` | 每个掉落只能选中一次 |

### Harvester（采集者匹配）

> `import mods.dropt.Harvester;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.type(string type)` | 未说明 | 设置类型：PLAYER / NON_PLAYER / ANY / EXPLOSION / REAL_PLAYER / FAKE_PLAYER |
| `.mainHand(string harvestLevel)` | 未说明 | 主手工具等级匹配 |
| `.mainHand(IItemStack[] items)` | 未说明 | 主手物品匹配（白名单） |
| `.mainHand(string type, IItemStack[] items)` | 未说明 | 主手物品匹配，type: "WHITELIST"/"BLACKLIST" |
| `.mainHand(string type, IItemStack[] items, string harvestLevel)` | 未说明 | 主手物品+等级匹配 |
| `.offHand(...)` | 未说明 | 副手（参数同 mainHand） |
| `.gameStages(string[] stages)` | 未说明 | 游戏阶段匹配（ANY） |
| `.gameStages(string require, string[] stages)` | 未说明 | 游戏阶段匹配，require: "ANY"/"ALL" |
| `.gameStages(string type, string require, string[] stages)` | 未说明 | 游戏阶段匹配，含类型过滤 |
| `.playerName(string[] names)` | 未说明 | 玩家名匹配（白名单） |
| `.playerName(string type, string[] names)` | 未说明 | 玩家名匹配，type: "WHITELIST"/"BLACKLIST" |

### Drop（掉落物定义）

> `import mods.dropt.Drop;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.force()` | 未说明 | 强制掉落 |
| `.selector(Weight weight)` | 未说明 | 设置选择器权重 |
| `.selector(Weight weight, string silkTouch)` | 未说明 | 带精准采集，silkTouch: "REQUIRED"/"EXCLUDED"/"ANY" |
| `.selector(Weight weight, string silkTouch, int fortune)` | 未说明 | 带精准采集和时运需求 |
| `.items(IItemStack[] items)` | 未说明 | 设置掉落物品 |
| `.items(string drop, IItemStack[] items)` | 未说明 | 设置掉落物品，drop: "ONE"/"ALL" |
| `.items(IItemStack[] items, Range range)` | 未说明 | 带数量范围的掉落物品 |
| `.items(string drop, IItemStack[] items, Range range)` | 未说明 | 带数量范围的掉落物品，drop: "ONE"/"ALL" |
| `.matchQuantity(IItemStack[] items)` | 未说明 | 等数替换 |
| `.xp(string replace, Range amount)` | 未说明 | 经验掉落，replace: "ADD"/"REPLACE" |
| `.replaceBlock(string block)` | 未说明 | 替换方块状态 |
| `.replaceBlock(string block, Map properties)` | 未说明 | 替换方块状态（含属性） |

### Range（数量范围）

> `import mods.dropt.Range;`

由 `Dropt.range()` 工厂方法创建。

### Weight（权重）

> `import mods.dropt.Weight;`

由 `Dropt.weight()` 工厂方法创建。

---

## 使用示例

### 基本使用方法 (嵌套链式的 builder 方法)

``` zenscript
import mods.dropt.Dropt;

Dropt.list("test_list")

    // Set the list priority
    .priority(0)

    // When stone is broken, should replace with string with custom name.
    .add(Dropt.rule()
        .matchBlocks(["minecraft:stone"])
        .addDrop(Dropt.drop()
            .items([<minecraft:string>.withTag({display: {Name: "Theory"}})])
        )
    )

    // When cobblestone or <ore:sand> is dropped, should replace with leather.
    .add(Dropt.rule()
        .matchDrops([<minecraft:cobblestone>.or(<ore:sand>)])
        .addDrop(Dropt.drop()
            .items([<minecraft:leather>])
        )
    )

    // When dirt is dropped, should replace with leather 25% of the time and
    // string 75% of the time.
    .add(Dropt.rule()
        .matchDrops([<minecraft:dirt>])
        .addDrop(Dropt.drop()
            .selector(Dropt.weight(25))
            .items([<minecraft:leather>])
        )
        .addDrop(Dropt.drop()
            .selector(Dropt.weight(75))
            .items([<minecraft:string>])
        )
    );
```

### 基础替换

```zenscript
import mods.dropt.Dropt;

Dropt.list("basic")
  .add(
      Dropt.rule()
      .matchBlocks(["minecraft:stone"])
      .addDrop(Dropt.drop().items([<minecraft:string>]))
  );
```

### 选择性移除

```zenscript
Dropt.list("remove_cobble")
  .add(
      Dropt.rule()
      .matchBlocks(["minecraft:stone", "minecraft:cobblestone"])
      .matchDrops([<minecraft:cobblestone>])
      .replaceStrategy("REPLACE_ITEMS")
      .addDrop(Dropt.drop())
  );
```

### 加权掉落

```zenscript
Dropt.list("weighted")
  .add(
      Dropt.rule()
      .matchBlocks(["minecraft:stone"])
      .addDrop(Dropt.drop().selector(Dropt.weight(75)))       // 75% 空
      .addDrop(Dropt.drop().selector(Dropt.weight(25)).items([<minecraft:diamond>]))  // 25% 钻石
  );
```

### 时运修正

```zenscript
Dropt.list("fortune")
  .add(
      Dropt.rule()
      .matchBlocks(["minecraft:quartz_ore"])
      .addDrop(Dropt.drop().items([<minecraft:quartz>], Dropt.range(1, 2)))
      .addDrop(Dropt.drop()
          .selector(Dropt.weight(10), "ANY", 1)     // 时运 1+
          .items([<minecraft:quartz>], Dropt.range(4, 8)))
      .addDrop(Dropt.drop()
          .selector(Dropt.weight(100), "ANY", 3)    // 时运 3
          .items([<minecraft:quartz>], Dropt.range(32, 64)))
  );
```

### 精准采集

```zenscript
Dropt.list("silk")
  .add(
      Dropt.rule()
      .matchBlocks(["minecraft:stone"])
      .replaceStrategy("REPLACE_ALL_IF_SELECTED")
      .addDrop(Dropt.drop()
          .selector(Dropt.weight(1), "REQUIRED")
          .items([<minecraft:string>]))
  );
```

### 工具限制

```zenscript
Dropt.list("tool")
  .add(
      Dropt.rule()
      .matchBlocks(["minecraft:dirt:*"])
      .matchHarvester(
          Dropt.harvester()
          .type("PLAYER")
          .mainHand("BLACKLIST", [], "shovel;0;-1")  // 非铲子
      )
      .addDrop(Dropt.drop())  // 空掉落
  );
```

### 方块状态替换

```zenscript
Dropt.list("blockstate")
  .add(
      Dropt.rule()
      .matchBlocks(["minecraft:stone"])
      .addDrop(Dropt.drop()
          .items([<minecraft:cobblestone>])
          .replaceBlock("minecraft:log", {axis: "y", variant: "oak"}))
  );
```

### fallthrough（继续匹配）

```zenscript
Dropt.list("multi")
  .add(
      Dropt.rule()
      .fallthrough()
      .matchBlocks(["minecraft:dirt"])
      .addDrop(Dropt.drop().items([<minecraft:diamond>]))
  )
  .add(
      Dropt.rule()
      .matchBlocks(["minecraft:dirt"])
      .replaceStrategy("ADD")
      .addDrop(Dropt.drop().items([<minecraft:emerald>]))
  );
```
