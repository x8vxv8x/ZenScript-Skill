# Astral Sorcery CraftTweaker API 参考

> Mod ID: `astralsorcery`
> 前置条件: 无（原生 CraftTweaker 支持）
> 导入: `import mods.astralsorcery.<ClassName>;`

## API 列表

### Altar（祭坛）

> `import mods.astralsorcery.Altar;`

#### 移除配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeAltarRecipe(String recipeLocation)` | void | 根据配方名称移除祭坛配方 |

**注意：** 可在 JEI 或 Astral Tome 中悬停在配方输出上，按 F3 查看。

#### 添加配方方法 - Discovery（星辉合成台）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addDiscoveryAltarRecipe(String recipeLocation, IItemStack output, int starlightRequired, int craftingTickTime, IIngredient[] inputs)` | void | 添加星辉合成台配方 |

**参数说明：**
- `recipeLocation`：配方名称（必须提供）
- `output`：输出物品
- `starlightRequired`：所需星能
- `craftingTickTime`：制作时间（ticks）
- `inputs`：输入材料数组（长度必须为 9）

**输入顺序：**
```
[0] [1] [2]
[3] [4] [5]
[6] [7] [8]
```

#### 添加配方方法 - Attunement（星辉祭坛）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addAttunementAltarRecipe(String recipeLocation, IItemStack output, int starlightRequired, int craftingTickTime, IIngredient[] inputs)` | void | 添加星辉祭坛配方 |
- inputs长度必须为 13

**输入顺序：** 
```
[9]             [10]
    [0] [1] [2]
    [3] [4] [5]
    [6] [7] [9]
[11]            [12]
```

#### 添加配方方法 - Constellation（天辉祭坛）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addConstellationAltarRecipe(String recipeLocation, IItemStack output, int starlightRequired, int craftingTickTime, IIngredient[] inputs)` | void | 添加天辉祭坛配方 |
- inputs长度必须为 21

**输入顺序：**
```

[9]  [13]    [14] [10]
[15] [0] [1] [2]  [16]
     [3] [4] [5]
[17] [6] [7] [8]  [18]
[11] [19]    [20] [12]
```

#### 添加配方方法 - Trait（五彩祭坛）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addTraitAltarRecipe(String recipeLocation, IItemStack output, int starlightRequired, int craftingTickTime, IIngredient[] inputs, @Optional String constellationFocus)` | void | 添加五彩祭坛配方 |

**参数说明：**
- `constellationFocus`：所需星座（可选，未本地化字符串）
- inputs长度必须为 25 或更高（索引 25+ 为外围物品）
**输入顺序：** 
```
[9]  [13] [21] [14] [10]
[15] [0]  [1]  [2]  [16]
[22] [3]  [4]  [5]  [23]
[17] [6]  [7]  [8]  [18]
[11] [19] [24] [20] [12]
[25+] 外部物品（放在祭坛周围光波增幅器上）
```

---

### Grindstone（砂轮）

> `import mods.astralsorcery.Grindstone;`

#### 添加配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack input, IItemStack output)` | void | 添加研磨配方 |
| `.addRecipe(IItemStack input, IItemStack output, float doubleChance)` | void | 添加研磨配方（带双倍产出概率） |

#### 移除配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |

---

### StarlightInfusion（星能聚合器）

> `import mods.astralsorcery.StarlightInfusion;`

#### 添加配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addInfusion(IItemStack input, IItemStack output, boolean consumeMultiple, float consumptionChance, int craftingTickTime)` | void | 添加配方 |

**参数说明：**
- `input`：输入物品
- `output`：输出物品
- `consumeMultiple`：是否消耗多个输入
- `consumptionChance`：消耗概率
- `craftingTickTime`：制作时间（ticks）

#### 移除配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInfusion(IItemStack output)` | void | 移除指定输出的配方 |

---

### LiquidInteraction（液体交互）

> `import mods.astralsorcery.LiquidInteraction;`

#### 添加配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addInteraction(ILiquidStack liquid1, float chance1, ILiquidStack liquid2, float chance2, int weight, IItemStack output)` | void | 添加液体交互配方 |

**参数说明：**
- `liquid1`、`liquid2`：输入液体（数量表示消耗量）
- `chance1`、`chance2`：对应液体的消耗概率
- `weight`：配方权重（相对于其他相同液体对的交互）
- `output`：输出物品

#### 移除配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInteraction(ILiquidStack liquid1, ILiquidStack liquid2, @Optional IItemStack output)` | void | 移除液体交互配方 |

---

### LightTransmutation（星光嬗变）

> `import mods.astralsorcery.LightTransmutation;`

#### 添加配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addTransmutation(IItemStack input, IItemStack output, double cost)` | void | 添加嬗变配方 |

#### 移除配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeTransmutation(IItemStack stackToRemove, boolean matchMeta)` | void | 移除嬗变配方 |

**参数说明：**
- `matchMeta`：是否匹配物品元数据

---

### Lightwell（聚星缸）

> `import mods.astralsorcery.Lightwell;`

#### 添加配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addLiquefaction(IItemStack input, ILiquidStack output, float productionMultiplier, float shatterMultiplier, int colorHEX)` | void | 添加液化配方 |

**参数说明：**
- `input`：输入物品（催化剂）
- `output`：输出液体（仅类型有效，数量取决于日夜等因素）
- `productionMultiplier`：产出倍率（通常 0.3 - 1.2）
- `shatterMultiplier`：碎裂倍率（越高，催化剂碎裂概率越低）
- `colorHEX`：粒子颜色（十六进制）

#### 移除配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeLiquefaction(IItemStack input, @Optional ILiquidStack output)` | void | 移除液化配方 |

**注意：** 可将 `output` 设为 `null` 仅通过输入物品搜索。

---

### Utils（工具类）

> `import mods.astralsorcery.Utils;`

#### 获取水晶方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getCrystalORIngredient(boolean hasToBeCelestial, boolean hasToBeAttuned)` | IIngredient | 获取匹配的 AS 水晶配方材料 |

## 使用示例

### 示例一：祭坛配方

```zenscript
import mods.astralsorcery.Altar;

// 添加 星辉合成台配方
Altar.addDiscoveryAltarRecipe("mypack:dirt_recipe", <minecraft:dirt>, 200, 200, [
    <minecraft:grass>, null, <ore:treeLeaves>,
    null, <minecraft:grass>, null,
    <liquid:astralsorcery.liquidstarlight>, null, <ore:treeLeaves>]);

// 添加 五彩祭坛配方（带星座要求）
Altar.addTraitAltarRecipe("mypack:tnt_recipe", <minecraft:tnt>, 4500, 100, [
    <liquid:lava>, <liquid:lava>, <liquid:lava>, <liquid:lava>, <minecraft:gunpowder>,
    <liquid:lava>, <liquid:lava>, <liquid:lava>, <liquid:lava>, null,
    null, null, null, <ore:blockMarble>, <ore:blockMarble>,
    <astralsorcery:itemusabledust>, <astralsorcery:itemusabledust>, <astralsorcery:itemusabledust>, <astralsorcery:itemusabledust>, <ore:blockMarble>,
    <ore:blockMarble>, <minecraft:redstone>, <minecraft:redstone>, <minecraft:redstone>, <minecraft:redstone>,
    // 外部物品
    <minecraft:sand>, <minecraft:sand>, <minecraft:sand>, <minecraft:sand>, <minecraft:sand>
], "astralsorcery.constellation.evorsio");

// 移除配方
Altar.removeAltarRecipe("astralsorcery:shaped/internal/altar/lightwell");
```

### 示例二：砂轮和星能聚合配方

```zenscript
import mods.astralsorcery.Grindstone;
import mods.astralsorcery.StarlightInfusion;

// 添加磨石配方（50% 双倍产出）
Grindstone.addRecipe(<minecraft:cobblestone>, <minecraft:gravel>, 0.5);

// 添加星能聚合配方
StarlightInfusion.addInfusion(<astralsorcery:itemjournal>, <minecraft:bow>, false, 0.7, 200);

// 移除配方
Grindstone.removeRecipe(<minecraft:redstone>);
StarlightInfusion.removeInfusion(<minecraft:ice>);
```

### 示例三：液体交互和嬗变

```zenscript
import mods.astralsorcery.LiquidInteraction;
import mods.astralsorcery.LightTransmutation;

// 添加液体交互（岩浆 + 水 = 钻石）
LiquidInteraction.addInteraction(<liquid:lava> * 10, 0.1, <liquid:water> * 90, 0.2, 400, <minecraft:diamond>);

// 添加嬗变配方（草方块 -> 金矿，消耗 10 星光）
LightTransmutation.addTransmutation(<minecraft:grass>, <minecraft:gold_ore>, 10);

// 移除配方
LiquidInteraction.removeInteraction(<liquid:lava>, <liquid:starlight>);
LightTransmutation.removeTransmutation(<minecraft:end_stone>, false);
```

### 示例四：聚星缸配方

```zenscript
import mods.astralsorcery.Lightwell;

// 添加液化配方
Lightwell.addLiquefaction(<minecraft:dirt>, <liquid:water>, 1, 0.2, 0);

// 移除配方
Lightwell.removeLiquefaction(<astralsorcery:itemcraftingcomponent:0>, null);
```

## 注意事项

- 祭坛配方必须提供资源位置，可在 JEI 或 Astral Tome 中按 F3 查看
- 不同祭坛的输入数组长度要求不同：9、13、21、25
- 五彩祭坛的索引 25+ 物品需要放在祭坛周围的中继器上
- 聚星缸的产出倍率通常在 0.3 - 1.2 之间，过高会导致不合理产出
- 移除配方时，如果存在多个相同输出的配方，需要多次调用移除方法
