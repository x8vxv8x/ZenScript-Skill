# Nature's Aura CraftTweaker API 参考

> Mod ID: `naturesaura`
> 前置条件: 无
> 导入: `import mods.naturesaura.Altar;` / `import mods.naturesaura.TreeRitual;` / `import mods.naturesaura.Offering;` / `import mods.naturesaura.AnimalSpawner;`

## API 列表

### Altar（自然祭坛）

> `import mods.naturesaura.Altar;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String name, IIngredient input, IItemStack output, IIngredient catalyst, int aura, int time)` | void | 添加自然祭坛配方 |
| `.removeRecipe(IItemStack output)` | void | 根据输出物品移除配方 |

参数说明：
- `name`：配方注册名
- `input`：输入物品
- `output`：输出物品
- `catalyst`：催化剂方块（放置在四个角落），可为 null
- `aura`：完成配方所需的灵气量
- `time`：处理时间（tick）

### TreeRitual（森林仪式）

> `import mods.naturesaura.TreeRitual;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String name, IIngredient saplingType, IItemStack output, int time, IIngredient[] items)` | void | 添加森林仪式配方 |
| `.removeRecipe(IItemStack output)` | void | 根据输出物品移除配方 |

参数说明：
- `name`：配方注册名
- `saplingType`：需要放置并生长成树的树苗
- `output`：仪式产出物品
- `time`：处理时间（tick）
- `items`：仪式所需物品列表

### Offering（献祭）

> `import mods.naturesaura.Offering;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String name, IIngredient input, int inputAmount, IIngredient startItem, IItemStack output)` | void | 添加献祭配方 |
| `.removeRecipe(IItemStack output)` | void | 根据输出物品移除配方 |

参数说明：
- `name`：配方注册名
- `input`：献祭物品
- `inputAmount`：所需献祭物品数量（input 变量的数量会被忽略）
- `startItem`：启动献祭所需的物品
- `output`：献祭产出物品

### AnimalSpawner（生物生成祭坛）

> `import mods.naturesaura.AnimalSpawner;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String name, String entity, int aura, int time, IIngredient[] ingredients)` | void | 添加生物生成配方 |
| `.removeRecipe(String name)` | void | 根据配方注册名移除配方 |

参数说明：
- `name`：配方注册名
- `entity`：要生成的实体名称
- `aura`：完成配方所需的灵气量
- `time`：处理时间（tick）
- `ingredients`：所需物品列表

---

## RandomTweaker 扩展（需安装 RandomTweaker）

> `import mods.randomtweaker.naturesaura.IWorld;`
> `import mods.randomtweaker.naturesaura.IAuraChunk;`

### IWorld 扩展（灵气查询）

> `import mods.randomtweaker.naturesaura.IWorld;`

IWorld 的扩展类，IWorld 实例可直接使用这些方法。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getAuraChunk(pos as IBlockPos)` | IAuraChunk | 返回 pos 所在的灵气区块 |
| `.getHighestSpot(pos as IBlockPos, radius as int, defaultSpot as IBlockPos)` | IBlockPos | 返回以 pos 为中心、radius 为半径的范围内灵气量最高的坐标。最高灵气量小于 0 时返回 defaultSpot |
| `.getLowestSpot(pos as IBlockPos, radius as int, defaultSpot as IBlockPos)` | IBlockPos | 返回灵气量最低的坐标。最低灵气量大于 0 时返回 defaultSpot |
| `.getSpotAmountInArea(pos as IBlockPos, radius as int)` | int | 返回范围内灵气点总和 |
| `.getAuraInArea(pos as IBlockPos, radius as int)` | int | 返回范围内灵气总和 |
| `.triangulateAuraInArea(pos as IBlockPos, radius as int)` | int | 返回范围内灵气总和（每个灵气点的灵气量乘以与 pos 距离的百分比：`1 - (距离 / radius)`） |

#### 使用示例

```zenscript
import mods.randomtweaker.naturesaura.IAuraChunk;

events.onPlayerRightClickItem(function(event as PlayerRightClickItemEvent) {
    var world as IWorld = event.world;
    if(!world.remote && <minecraft:stick>.matches(event.item)) {
        var auraChunk as IAuraChunk = world.getAuraChunk(event.position);
        var highestPos = world.getHighestSpot(event.position, 4, event.position);
        var lowestPos = world.getLowestSpot(event.position, 4, event.position);
        var spotAmount as int = world.getSpotAmountInArea(event.position, 4);
        var auraTotal as int = world.getAuraInArea(event.position, 4);
        var triangulateAura as int = world.triangulateAuraInArea(event.position, 4);
    }
});
```

### IAuraChunk（灵气区块）

> `import mods.randomtweaker.naturesaura.IAuraChunk;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.drainAura(pos as IBlockPos, amount as int, aimForZero as bool, simulate as bool)` | int | 消耗给定 pos 的灵气。`aimForZero` 为 true 时灵气被消耗至负数则返回消耗前的灵气量。返回实际消耗的灵气 |
| `.drainAura(pos as IBlockPos, amount as int)` | int | 同上，后两个参数默认 false |
| `.storeAura(pos as IBlockPos, amount as int, aimForZero as bool, simulate as bool)` | int | 增加给定 pos 的灵气。`aimForZero` 为 true 时灵气被增加至正数则返回增加前的灵气量。返回实际增加的灵气 |
| `.storeAura(pos as IBlockPos, amount as int)` | int | 同上，后两个参数默认 false |
| `.getDrainSpot(pos as IBlockPos)` | int | 返回 pos 的灵气量 |

#### 使用示例

```zenscript
import mods.randomtweaker.naturesaura.IAuraChunk;

events.onPlayerRightClickItem(function(event as PlayerRightClickItemEvent) {
    var world as IWorld = event.world;
    var pos as IBlockPos = event.position;

    if(!world.remote && <minecraft:stick>.matches(event.item)) {
        var auraChunk as IAuraChunk = world.getAuraChunk(event.position);
        auraChunk.drainAura(pos, 10000);   // 消耗 10000 灵气
        auraChunk.storeAura(pos, 10000);   // 增加 10000 灵气
        var amount as int = auraChunk.getDrainSpot(pos); // 获取灵气量
    }
});
```
