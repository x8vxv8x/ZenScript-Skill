# Dropt 掉落系统 API

> `import mods.dropt.Dropt;`

Dropt 是一个灵活的方块掉落替换系统，支持多条件匹配、加权掉落、时运修正等。

## 类一览

| 类 | 导入 | 说明 |
|----|------|------|
| Dropt | `mods.dropt.Dropt` | 工厂类，创建其他对象 |
| RuleList | `mods.dropt.RuleList` | 规则列表 |
| Rule | `mods.dropt.Rule` | 单条规则 |
| Harvester | `mods.dropt.Harvester` | 采集者匹配 |
| Drop | `mods.dropt.Drop` | 掉落物定义 |
| Range | `mods.dropt.Range` | 数量范围 |
| Weight | `mods.dropt.Weight` | 权重 |

## Dropt 工厂方法

```zenscript
Dropt.list("name")           // 创建/获取 RuleList
Dropt.rule()                 // 创建 Rule
Dropt.harvester()            // 创建 Harvester
Dropt.drop()                 // 创建 Drop
Dropt.range(int fixed)       // 固定数量
Dropt.range(int min, int max)// 范围数量
Dropt.weight(int weight)     // 权重
Dropt.weight(int weight, int fortuneMod)  // 带时运修正的权重
```

## RuleList

```zenscript
list.priority(int)   // 优先级（越大越先匹配，默认 0）
list.add(Rule)       // 添加规则
```

## Rule

```zenscript
rule.debug()                            // 启用调试日志
rule.matchBlocks(string[])              // 匹配方块（白名单）
rule.matchBlocks(string type, string[]) // type: "WHITELIST"/"BLACKLIST"
rule.matchDrops(IIngredient[])          // 匹配掉落物
rule.matchDrops(string type, IIngredient[])
rule.matchHarvester(Harvester)          // 匹配采集者
rule.matchBiomes(string[])              // 匹配生物群系
rule.matchBiomes(string type, string[])
rule.matchDimensions(int[])             // 匹配维度 ID
rule.matchDimensions(string type, int[])
rule.matchVerticalRange(int min, int max)   // 匹配高度范围
rule.matchSpawnDistance(int min, int max)   // 匹配出生点距离
rule.matchSpawnDistance(string type, int min, int max)
rule.replaceStrategy(string)            // 替换策略
rule.dropStrategy(string)               // 掉落策略
rule.dropCount(Range)                   // 选择器执行次数
rule.addDrop(Drop)                      // 添加掉落
rule.fallthrough(bool)                  // 继续匹配后续规则
```

### 替换策略

| 策略 | 说明 |
|------|------|
| `REPLACE_ALL` | 替换所有掉落（默认） |
| `REPLACE_ALL_IF_SELECTED` | 选中时替换所有 |
| `REPLACE_ITEMS` | 只替换匹配的掉落 |
| `REPLACE_ITEMS_IF_SELECTED` | 选中时替换匹配的 |
| `ADD` | 追加到现有掉落 |

### 掉落策略

| 策略 | 说明 |
|------|------|
| `REPEAT` | 同一掉落可被选中多次（默认） |
| `UNIQUE` | 每个掉落只能选中一次 |

## Harvester

```zenscript
h.type(string)               // PLAYER / NON_PLAYER / ANY / EXPLOSION / REAL_PLAYER / FAKE_PLAYER
h.mainHand(string harvestLevel)  // 主手工具等级匹配
h.mainHand(IItemStack[])         // 主手物品匹配（白名单）
h.mainHand(string type, IItemStack[])
h.mainHand(string type, IItemStack[], string harvestLevel)
h.offHand(...)                   // 副手（同 mainHand 参数）
h.gameStages(string[])           // 游戏阶段匹配
h.gameStages(string require, string[])     // require: "ANY"/"ALL"
h.gameStages(string type, string require, string[])
h.playerName(string[])           // 玩家名匹配
h.playerName(string type, string[])
```

## Drop

```zenscript
drop.force()                                         // 强制掉落
drop.selector(Weight)                                // 选择器
drop.selector(Weight, string silkTouch)              // REQUIRED/EXCLUDED/ANY
drop.selector(Weight, string silkTouch, int fortune) // 带时运需求
drop.items(IItemStack[])                             // 掉落物品
drop.items(string drop, IItemStack[])                // drop: "ONE"/"ALL"
drop.items(IItemStack[], Range)                      // 带数量范围
drop.items(string drop, IItemStack[], Range)
drop.matchQuantity(IItemStack[])                     // 等数替换
drop.xp(string replace, Range amount)               // 经验掉落 replace: "ADD"/"REPLACE"
drop.replaceBlock(string block)                      // 替换方块状态
drop.replaceBlock(string block, Map properties)
```

---

## 使用示例

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
