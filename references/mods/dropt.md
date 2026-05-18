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
| `.list(string name)` | `RuleList` | 创建/获取规则列表，相同名称返回同一对象 |
| `.rule()` | `Rule` | 创建新规则 |
| `.harvester()` | `Harvester` | 创建新采集者匹配 |
| `.drop()` | `Drop` | 创建新掉落物定义 |
| `.range(int fixed)` | `Range` | 固定数量范围 |
| `.range(int min, int max)` | `Range` | 区间数量范围（最小值和最大值均为包含） |
| `.range(int min, int max, int fortuneModifier)` | `Range` | 带时运修正的区间数量范围（最小值和最大值均为包含） |
| `.weight(int weight)` | `Weight` | 权重 |
| `.weight(int weight, int fortuneModifier)` | `Weight` | 带时运修正的权重 |

### RuleList（规则列表）

> `import mods.dropt.RuleList;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.priority(int priority)` | `RuleList` | 设置优先级（越大越先匹配，默认 0） |
| `.add(Rule rule)` | `RuleList` | 添加规则到列表 |

### Rule（规则）

> `import mods.dropt.Rule;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.debug()` | `Rule` | 启用调试日志（用完后请关闭，会产生大量日志） |
| `.matchBlocks(string[] blocks)` | `Rule` | 匹配方块（白名单） |
| `.matchBlocks(string type, string[] blocks)` | `Rule` | 匹配方块，type: "WHITELIST"/"BLACKLIST" |
| `.matchDrops(IIngredient[] drops)` | `Rule` | 匹配掉落物（白名单） |
| `.matchDrops(string type, IIngredient[] drops)` | `Rule` | 匹配掉落物，type: "WHITELIST"/"BLACKLIST" |
| `.matchHarvester(Harvester harvester)` | `Rule` | 匹配采集者 |
| `.matchBiomes(string[] biomes)` | `Rule` | 匹配生物群系（白名单） |
| `.matchBiomes(string type, string[] biomes)` | `Rule` | 匹配生物群系，type: "WHITELIST"/"BLACKLIST" |
| `.matchDimensions(int[] dimensions)` | `Rule` | 匹配维度 ID（白名单） |
| `.matchDimensions(string type, int[] dimensions)` | `Rule` | 匹配维度，type: "WHITELIST"/"BLACKLIST" |
| `.matchVerticalRange(int min, int max)` | `Rule` | 匹配高度范围 |
| `.matchSpawnDistance(int min, int max)` | `Rule` | 匹配出生点距离（白名单） |
| `.matchSpawnDistance(string type, int min, int max)` | `Rule` | 匹配出生点距离，type: "WHITELIST"/"BLACKLIST" |
| `.replaceStrategy(string strategy)` | `Rule` | 设置替换策略 |
| `.dropStrategy(string strategy)` | `Rule` | 设置掉落策略 |
| `.dropCount(Range count)` | `Rule` | 设置选择器执行次数 |
| `.addDrop(Drop drop)` | `Rule` | 添加掉落 |
| `.fallthrough(boolean fallthrough)` | `Rule` | 匹配后是否继续匹配后续规则 |

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
| `.type(string type)` | `Harvester` | 设置类型：PLAYER / NON_PLAYER / ANY / EXPLOSION / REAL_PLAYER / FAKE_PLAYER |
| `.mainHand(string harvestLevel)` | `Harvester` | 主手工具等级匹配 |
| `.mainHand(IItemStack[] items)` | `Harvester` | 主手物品匹配（白名单） |
| `.mainHand(string type, IItemStack[] items)` | `Harvester` | 主手物品匹配，type: "WHITELIST"/"BLACKLIST" |
| `.mainHand(string type, IItemStack[] items, string harvestLevel)` | `Harvester` | 主手物品+等级匹配 |
| `.offHand(string harvestLevel)` | `Harvester` | 副手工具等级匹配 |
| `.offHand(IItemStack[] items)` | `Harvester` | 副手物品匹配（白名单） |
| `.offHand(string type, IItemStack[] items)` | `Harvester` | 副手物品匹配，type: "WHITELIST"/"BLACKLIST" |
| `.offHand(string type, IItemStack[] items, string harvestLevel)` | `Harvester` | 副手物品+等级匹配 |
| `.gameStages(string[] stages)` | `Harvester` | 游戏阶段匹配（ANY） |
| `.gameStages(string require, string[] stages)` | `Harvester` | 游戏阶段匹配，require: "ANY"/"ALL" |
| `.gameStages(string type, string require, string[] stages)` | `Harvester` | 游戏阶段匹配，含类型过滤 |
| `.playerName(string[] names)` | `Harvester` | 玩家名匹配（白名单） |
| `.playerName(string type, string[] names)` | `Harvester` | 玩家名匹配，type: "WHITELIST"/"BLACKLIST" |

### Drop（掉落物定义）

> `import mods.dropt.Drop;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.force()` | `Drop` | 强制掉落，忽略选择器 |
| `.selector(Weight weight)` | `Drop` | 设置选择器权重 |
| `.selector(Weight weight, string silkTouch)` | `Drop` | 带精准采集，silkTouch: "REQUIRED"/"EXCLUDED"/"ANY" |
| `.selector(Weight weight, string silkTouch, int fortuneLevelRequired)` | `Drop` | 带精准采集和时运需求 |
| `.items(IItemStack[] items)` | `Drop` | 设置掉落物品 |
| `.items(string drop, IItemStack[] items)` | `Drop` | 设置掉落物品，drop: "ONE"/"ALL" |
| `.items(IItemStack[] items, Range range)` | `Drop` | 带数量范围的掉落物品 |
| `.items(string drop, IItemStack[] items, Range range)` | `Drop` | 带数量范围的掉落物品，drop: "ONE"/"ALL" |
| `.matchQuantity(IItemStack[] drops)` | `Drop` | 等数替换 |
| `.xp(string replace, Range amount)` | `Drop` | 经验掉落，replace: "ADD"/"REPLACE" |
| `.replaceBlock(string block)` | `Drop` | 替换方块状态 |
| `.replaceBlock(string block, Map properties)` | `Drop` | 替换方块状态（含属性） |

### Range（数量范围）

> `import mods.dropt.Range;`

由 `Dropt.range()` 工厂方法创建。用于 `Drop.items()` 和 `Drop.xp()` 等方法中表示数量范围。

### Weight（权重）

> `import mods.dropt.Weight;`

由 `Dropt.weight()` 工厂方法创建。用于 `Drop.selector()` 方法中定义选择权重。

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

### 游戏阶段

```
import mods.dropt.Dropt;
import mods.dropt.Harvester;

Dropt.list("list_name")

  .add(Dropt.rule()
      .matchBlocks(["minecraft:stone"])
      .matchHarvester(Dropt.harvester()
        .gameStages("WHITELIST", "ALL", ["stage_A", "stage_B"]) // 设定玩家需要的阶段
      )
      .addDrop(Dropt.drop()
          .items([<minecraft:string>])
      )
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

### fallthrough（穿透传递）

```zenscript
Dropt.list("multi")
  .add(
      Dropt.rule()
      .fallthrough(true)
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
