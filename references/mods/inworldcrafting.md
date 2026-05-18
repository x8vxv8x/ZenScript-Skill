# InWorldCrafting CraftTweaker API 参考

> Mod ID: `inworldcrafting`
> 前置条件: inworldcrafting
> 导入: `import mods.inworldcrafting.*;`

InWorldCrafting 允许通过脚本定义世界中的物品转化配方（流体转化、火焰燃烧、爆炸转化）。

---

## API 列表

### FluidToItem（流体转化物品）

> `import mods.inworldcrafting.FluidToItem;`

物品掉入流体后转化为指定物品。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `FluidToItem.transform(IItemStack output, ILiquidStack inputFluid, IIngredient[] inputItems, @Optional boolean consume)` | 未说明 | 流体中物品转化配方。`output` 为产出物品，`inputFluid` 为流体，`inputItems` 为所需物品数组，`consume` 为是否消耗输入物品（默认 true） |

---

### FluidToFluid（流体转化流体）

> `import mods.inworldcrafting.FluidToFluid;`

物品掉入流体后将流体转化为另一种流体。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `FluidToFluid.transform(ILiquidStack output, ILiquidStack inputFluid, IIngredient[] inputItems, @Optional boolean consume)` | 未说明 | 流体转化配方。`output` 为产出流体，`inputFluid` 为源流体，`inputItems` 为所需物品数组，`consume` 为是否消耗输入物品（默认 true） |

---

### FireCrafting（火焰燃烧）

> `import mods.inworldcrafting.FireCrafting;`

物品被火焰燃烧后转化为指定物品。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `FireCrafting.addRecipe(IItemStack output, IIngredient inputItem, @Optional int ticks)` | 未说明 | 火焰燃烧配方。`output` 为产出物品，`inputItem` 为输入物品，`ticks` 为燃烧持续时间（默认 40 tick = 2 秒） |

---

### ExplosionCrafting（爆炸转化）

> `import mods.inworldcrafting.ExplosionCrafting;`

物品或方块被爆炸后转化为指定物品。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `ExplosionCrafting.explodeItemRecipe(IItemStack output, IIngredient inputItem, @Optional int survicechance)` | 未说明 | 物品爆炸配方。`output` 为产出物品，`inputItem` 为输入物品，`survicechance` 为成功概率百分比（默认 100） |
| `ExplosionCrafting.explodeBlockRecipe(IItemStack output, IItemStack blockStack, @Optional int itemSpawnChance)` | 未说明 | 方块爆炸配方。`output` 为产出物品，`blockStack` 为方块物品形式（会比较 metadata），`itemSpawnChance` 为产出概率百分比（默认 100） |

---

## 重要提示

**不要重复添加相同物品，使用 `<物品> * 数量` 语法。** 游戏会将附近相同物品实体合并为堆叠，单独添加多个相同物品会导致配方在堆叠满时无法触发。

```zenscript
// 错误：重复添加相同物品
FluidToItem.transform(<minecraft:diamond>, <liquid:water>, [<ore:ingotIron>, <ore:ingotIron>, <ore:dustGold>]);

// 正确：使用数量语法
FluidToItem.transform(<minecraft:diamond>, <liquid:water>, [<ore:ingotIron> * 2, <ore:dustGold>]);
```

---

## 使用示例

### 流体转化物品

```zenscript
import mods.inworldcrafting.FluidToItem;

// 将桦木板扔进杂酚油中转化为防腐木
FluidToItem.transform(<immersiveengineering:treated_wood>, <liquid:creosote>, [<minecraft:planks:2>]);

// 将玻璃瓶扔进水中转化为水瓶
FluidToItem.transform(<minecraft:potion>.withTag({Potion: "minecraft:water"}), <liquid:water>, [<minecraft:glass_bottle>], true);
```

### 流体转化流体

```zenscript
import mods.inworldcrafting.FluidToFluid;

// 将 4 个原木扔进极寒流体中转化为岩浆
FluidToFluid.transform(<liquid:lava>, <liquid:cryotheum>, [<ore:logWood> * 4]);
```

### 火焰燃烧

```zenscript
import mods.inworldcrafting.FireCrafting;

// 将 4 个原木燃烧 60 tick 后转化为煤炭块
FireCrafting.addRecipe(<thermalfoundation:storage_resource>, <ore:logWood> * 4, 60);
```

### 爆炸转化

```zenscript
import mods.inworldcrafting.ExplosionCrafting;

// 铁锭被爆炸后有 15% 概率转化为钢锭
ExplosionCrafting.explodeItemRecipe(<ore:ingotSteel>.firstItem, <ore:ingotIron>, 15);

// 金合欢木板被爆炸后有 75% 概率掉落 8 根木棍
ExplosionCrafting.explodeBlockRecipe(<minecraft:stick> * 8, <minecraft:planks:4>, 75);
```
