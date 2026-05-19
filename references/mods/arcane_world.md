# Arcane World CraftTweaker API 参考

> Mod ID: `arcane_world`
> 前置条件: 无
> 导入: `import mods.ArcaneWorld;`

## API 列表

### ArcaneWorld

> `import mods.ArcaneWorld;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createRitualSummon(String name, String displayName, String entityID, IIngredient... inputs)` | void | 创建召唤仪式 |
| `.createRitualDragonBreath(String name, String displayName, IIngredient... inputs)` | void | 创建龙息仪式 |
| `.createArenaRitual(String name, String displayName, String entityID, IIngredient... inputs)` | void | 创建竞技场仪式（传送到副本维度并召唤实体） |
| `.createRitualWeather(String name, String displayName, String weatherType, IIngredient... inputs)` | void | 创建天气仪式 |
| `.createRitualTime(String name, String displayName, int timeChange, IIngredient... inputs)` | void | 创建时间仪式 |
| `.createRitualCreateItem(String name, String displayName, IItemStack result, IIngredient... inputs)` | void | 创建物品仪式（类似合成配方） |
| `.createRitualDungeon(String name, String displayName, IIngredient... inputs)` | void | 创建副本仪式（传送到副本维度） |
| `.createRitualCommand(String name, String displayName, String[] commands, IIngredient... inputs)` | void | 创建命令仪式 |
| `.remove(String registryName)` | void | 根据注册名移除仪式 |
| `.removeAll()` | void | 移除所有仪式 |

**参数说明：**
- `name`：仪式注册名
- `displayName`：仪式显示名称
- `entityID`：实体 ID（如 `"minecraft:creeper"`）
- `weatherType`：天气类型，可选值：`"clear"`, `"rain"`, `"thunder"`
- `timeChange`：时间变化值（可为负数以倒退时间）
- `result`：输出物品
- `commands`：要执行的命令数组
- `inputs`：输入材料（可变参数）

**注意：** 通过 CraftTweaker 添加的仪式注册名为 `"crafttweaker:<name>"`

## 使用示例

### 示例一：创建召唤仪式

```zenscript
import mods.ArcaneWorld;

// 创建召唤苦力怕的仪式
ArcaneWorld.createRitualSummon("summon_creeper", "召唤苦力怕", "minecraft:creeper",
    <minecraft:gunpowder>, <minecraft:flint>, <minecraft:redstone>);
```

### 示例二：创建天气和时间仪式

```zenscript
import mods.ArcaneWorld;

// 创建晴天仪式
ArcaneWorld.createRitualWeather("clear_weather", "晴天", "clear",
    <minecraft:sunflower>, <minecraft:gold_ingot>);

// 创建时间前进仪式（+1000 ticks）
ArcaneWorld.createRitualTime("advance_time", "时间前进", 1000,
    <minecraft:clock>, <minecraft:redstone>);
```

### 示例三：创建物品仪式

```zenscript
import mods.ArcaneWorld;

// 创建物品合成仪式
ArcaneWorld.createRitualCreateItem("create_diamond", "钻石合成", <minecraft:diamond>,
    <minecraft:coal>, <minecraft:coal>, <minecraft:coal>, <minecraft:gold_ingot>);
```

### 示例四：创建命令仪式

```zenscript
import mods.ArcaneWorld;

// 创建执行命令的仪式
ArcaneWorld.createRitualCommand("give_items", "给予物品",
    ["give @p minecraft:diamond 1", "give @p minecraft:gold_ingot 5"],
    <minecraft:command_block>, <minecraft:redstone>);
```

### 示例五：移除仪式

```zenscript
import mods.ArcaneWorld;

// 移除指定仪式
ArcaneWorld.remove("crafttweaker:summon_creeper");

// 移除所有仪式
ArcaneWorld.removeAll();
```

## 注意事项

- 天气类型支持：clear（晴天）、rain（雨天）、thunder（雷暴）
- 时间变化值可为负数，用于倒退时间
- 通过 CraftTweaker 添加的仪式注册名格式为 `"crafttweaker:<name>"`
- 竞技场仪式会将玩家传送到 Arcane World 的副本维度
- 输入材料使用可变参数（IIngredient...），支持任意数量的输入
