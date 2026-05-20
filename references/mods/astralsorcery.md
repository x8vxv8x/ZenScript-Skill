# Astral Sorcery CraftTweaker API 参考

> Mod ID: `astralsorcery`
> 前置条件: 无（原生 CraftTweaker 支持）
> 导入: `import mods.astralsorcery.<ClassName>;`

## API 列表

### Altar（祭坛）

> `import mods.astralsorcery.Altar;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeAltarRecipe(String recipeLocation)` | void | 根据配方名称移除祭坛配方 |
| `.removeAltarRecipe(IItemStack output, int altarLevel)` | void | 根据输出物品和祭坛等级移除配方（已弃用，v1.10+ 推荐使用上方字符串版本）。`altarLevel`：0=星辉合成台、1=星辉祭坛、2=天辉祭坛 |
| `.addDiscoveryAltarRecipe(String recipeLocation, IItemStack output, int starlightRequired, int craftingTickTime, IIngredient[] inputs)` | void | 添加星辉合成台配方（inputs 长度必须为 9） |
| `.addAttunementAltarRecipe(String recipeLocation, IItemStack output, int starlightRequired, int craftingTickTime, IIngredient[] inputs)` | void | 添加星辉祭坛配方（inputs 长度必须为 13） |
| `.addConstellationAltarRecipe(String recipeLocation, IItemStack output, int starlightRequired, int craftingTickTime, IIngredient[] inputs)` | void | 添加天辉祭坛配方（inputs 长度必须为 21） |
| `.addTraitAltarRecipe(String recipeLocation, IItemStack output, int starlightRequired, int craftingTickTime, IIngredient[] inputs, @Optional String constellationFocus)` | void | 添加五彩祭坛配方（inputs 长度必须为 25+） |

**注意：** 可在 JEI 或 Astral Tome 中悬停在配方输出上，按 F3 查看配方名称。

**输入顺序：**

星辉合成台（9 格）：
```
[0] [1] [2]
[3] [4] [5]
[6] [7] [8]
```

星辉祭坛（13 格）：
```
[9]             [10]
    [0] [1] [2]
    [3] [4] [5]
    [6] [7] [8]
[11]            [12]
```

天辉祭坛（21 格）：
```
[9]  [13]    [14] [10]
[15] [0] [1] [2]  [16]
     [3] [4] [5]
[17] [6] [7] [8]  [18]
[11] [19]    [20] [12]
```

五彩祭坛（25+ 格）：
```
[9]  [13] [21] [14] [10]
[15] [0]  [1]  [2]  [16]
[22] [3]  [4]  [5]  [23]
[17] [6]  [7]  [8]  [18]
[11] [19] [24] [20] [12]
[25+] 外部物品（放在祭坛周围光波增幅器上）
```

### Grindstone（砂轮）

> `import mods.astralsorcery.Grindstone;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack input, IItemStack output)` | void | 添加研磨配方 |
| `.addRecipe(IItemStack input, IItemStack output, float doubleChance)` | void | 添加研磨配方（带双倍产出概率） |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |

### StarlightInfusion（星能聚合器）

> `import mods.astralsorcery.StarlightInfusion;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addInfusion(IItemStack input, IItemStack output, boolean consumeMultiple, float consumptionChance, int craftingTickTime)` | void | 添加配方。`consumeMultiple` 是否消耗多个输入。`consumptionChance` 消耗概率 |
| `.removeInfusion(IItemStack output)` | void | 移除指定输出的配方 |

### LiquidInteraction（液体交互）

> `import mods.astralsorcery.LiquidInteraction;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addInteraction(ILiquidStack liquid1, float chance1, ILiquidStack liquid2, float chance2, int weight, IItemStack output)` | void | 添加液体交互配方。`liquid1`/`liquid2` 数量表示消耗量。`chance1`/`chance2` 消耗概率。`weight` 配方权重 |
| `.removeInteraction(ILiquidStack liquid1, ILiquidStack liquid2, @Optional IItemStack output)` | void | 移除液体交互配方 |

### LightTransmutation（星光嬗变）

> `import mods.astralsorcery.LightTransmutation;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addTransmutation(IItemStack input, IItemStack output, double cost)` | void | 添加嬗变配方 |
| `.removeTransmutation(IItemStack stackToRemove, boolean matchMeta)` | void | 移除嬗变配方。`matchMeta` 是否匹配物品元数据 |

### Lightwell（聚星缸）

> `import mods.astralsorcery.Lightwell;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addLiquefaction(IItemStack input, ILiquidStack output, float productionMultiplier, float shatterMultiplier, int colorHEX)` | void | 添加液化配方。`productionMultiplier` 产出倍率（通常 0.3-1.2）。`shatterMultiplier` 碎裂倍率（越高碎裂概率越低）。`colorHEX` 粒子颜色 |
| `.removeLiquefaction(IItemStack input, @Optional ILiquidStack output)` | void | 移除液化配方。可将 `output` 设为 `null` 仅通过输入物品搜索 |

### Utils（工具类）

> `import mods.astralsorcery.Utils;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getCrystalORIngredient(boolean hasToBeCelestial, boolean hasToBeAttuned)` | IIngredient | 获取匹配的 AS 水晶配方材料 |

---

## RandomTweaker 扩展（需安装 RandomTweaker）

> `import mods.randomtweaker.astralsorcery.IPlayer;`
> `import mods.randomtweaker.astralsorcery.AttunementAltar;`
> `import mods.randomtweaker.astralsorcery.AttunementStartEvent;`
> `import mods.randomtweaker.astralsorcery.AttunementRecipeCompleteEvent;`

### IPlayer 扩展（星能力系统）

> `import mods.randomtweaker.astralsorcery.IPlayer;`

IPlayer 的扩展类，提供操作玩家星能力和共鸣星座的方法。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getPerkPercentToNextLevel()` | float | 返回升级星能力等级所需经验与超出现等级经验的百分比 |
| `.getPerkLevel()` | int | 返回当前星能力等级 |
| `.getPerkExp()` | double | 返回当前星能力总经验 |
| `.getAttunedConstellation()` | string | 获取玩家共鸣星座名称 |
| `.getKnownConstellations()` | List\<String> | 获取玩家已连线的星座名称 |
| `.getSeenConstellations()` | List\<String> | 获取玩家已知（已发现但未连线）星座名称 |
| `.modifyPerkExp(double exp)` | bool | 添加玩家星能力经验。如有共鸣星座返回 true，否则返回 false。`exp` 最大为 `(下一级容纳经验 - 当前容纳经验) * 0.08`。仅服务端可用 |
| `.setPerkExp(double exp)` | bool | 设置玩家星能力经验。参数含义同上。仅服务端可用 |

#### 使用示例

```zenscript
import mods.randomtweaker.astralsorcery.IPlayer;

events.onPlayerRightClickItem(function(event as PlayerRightClickItemEvent) {
    var player as IPlayer = event.player;
    var world as IWorld = event.world;

    if(!world.remote && <minecraft:stick>.matches(event.item)) {
        player.setPerkExp(158);
        var percent as float = player.getPerkPercentToNextLevel();
        var level as int = player.getPerkLevel();
        var exp as double = player.getPerkExp();
        var constellation as string = player.getAttunedConstellation();
        var knownConstellation as [string] = player.getKnownConstellations();
        var seenConstellation as [string] = player.getSeenConstellations();
        player.modifyPerkExp(13);
    }
});
```

### AttunementAltar（共鸣祭坛配方）

> `import mods.randomtweaker.astralsorcery.AttunementAltar;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(input as IIngredient, output as IItemStack, constellation as string)` | void | 添加共鸣祭坛配方，指定共鸣星座。星座名可通过 `/as constellation playerName` 按 Tab 查看，需全小写 |
| `.addRecipe(input as IIngredient, output as IItemStack)` | void | 添加共鸣祭坛配方，无需指定星座 |

**注意：** 共鸣祭坛会优先匹配有星座的配方。

#### 使用示例

```zenscript
import mods.randomtweaker.astralsorcery.AttunementAltar;

AttunementAltar.addRecipe(<minecraft:stick>, <minecraft:dirt>, "astralsorcery.constellation.discidia");
AttunementAltar.addRecipe(<minecraft:dirt>, <minecraft:stick>);
```

### AttunementStartEvent（共鸣开始事件）

> `import mods.randomtweaker.astralsorcery.AttunementStartEvent;`

当共鸣开始时触发。实现了 IEntityEvent。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 共鸣祭坛所处世界 |
| `constellation` | string | 共鸣的星座 |
| `entity` | IEntity | 与共鸣祭坛共鸣的实体（物品实体或生物） |

#### 实例方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getWorld()` | IWorld | 与 world Getter 一致 |
| `.getConstellation()` | string | 与 constellation Getter 一致 |

### AttunementRecipeCompleteEvent（共鸣配方完成事件）

> `import mods.randomtweaker.astralsorcery.AttunementRecipeCompleteEvent;`

当共鸣配方完成时触发。实现了 IEventCancelable（可取消，取消后配方不输出物品并返还输入）和 IEntityEvent。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `input` | IItemStack | 在共鸣祭坛上触发配方的物品 |
| `output` | IItemStack | 配方输出的物品 |
| `world` | IWorld | 共鸣祭坛所在的世界 |
| `constellation` | string | 共鸣的星座 |
| `entity` | IEntity | 与共鸣祭坛共鸣的实体 |
| `itemEntity` | IEntityItem | 与共鸣祭坛共鸣的物品实体 |

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `output` | IItemStack | 设置配方输出的物品 |

#### 实例方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getInput()` | IItemStack | 与 input Getter 一致 |
| `.getOutput()` | IItemStack | 与 output Getter 一致 |
| `.setOutput(output as IItemStack)` | void | 与 output Setter 一致 |
| `.getWorld()` | IWorld | 与 world Getter 一致 |
| `.getItemEntity()` | IEntityItem | 与 itemEntity Getter 一致 |
| `.getConstellation()` | string | 与 constellation Getter 一致 |
| `.getAdditionalOutput()` | List\<IItemStack> | 获取额外输出的物品 |
| `.addAdditionalOutput(additionalOutput as IItemStack)` | void | 添加额外输出的物品 |

#### 使用示例

```zenscript
import mods.randomtweaker.astralsorcery.AttunementAltar;
import mods.randomtweaker.astralsorcery.AttunementRecipeCompleteEvent;

AttunementAltar.addRecipe(<minecraft:stick>.withAmount(2), <minecraft:dirt>, "astralsorcery.constellation.discidia");

events.onAttunementRecipeComplete(function(event as AttunementRecipeCompleteEvent) {
    var world as IWorld = event.world;
    if(!world.remote && <minecraft:stick>.matches(event.itemEntity.item)) {
        var output as IItemStack = event.output;
        var constellation as string = event.constellation;

        if(<minecraft:dirt>.matches(output) && constellation == "astralsorcery.constellation.discidia") {
            event.setOutput(<minecraft:planks>.withAmount(10));
            event.addAdditionalOutput(<minecraft:stone>.withAmount(64));
            // event.cancel(); // 取消事件（取消后上述修改无效，返还输入物品）
        }
    }
});
```
