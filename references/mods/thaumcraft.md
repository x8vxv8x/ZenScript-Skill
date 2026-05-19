# Thaumcraft CraftTweaker API 参考

> Mod ID: `thaumcraft`
> 前置条件: Modtweaker
> 导入: `import mods.thaumcraft.*;`

## Aspect（要素）

```
<aspect:ignis>          // 要素 CTAspectStack（大小为 1）
<aspect:ignis> * 10     // 指定数量的要素
```

## API 列表

### ArcaneWorkbench（奥术工作台）

> `import mods.thaumcraft.ArcaneWorkbench;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerShapedRecipe(String name, String research, int vis, CTAspectStack[] aspectList, IItemStack output, IIngredient[][] input)` | void | 添加有序奥术配方。`research` 研究名(空串=无需研究)。`vis` 魔力消耗 |
| `.registerShapelessRecipe(String name, String research, int vis, CTAspectStack[] aspectList, IItemStack output, IIngredient[] input)` | void | 添加无序奥术配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(String name)` | void | 按配方名移除 |
| `.removeRecipe(IItemStack output)` | void | 按输出移除 |

### Crucible（坩埚）

> `import mods.thaumcraft.Crucible;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerRecipe(String name, String researchKey, IItemStack output, IIngredient input, CTAspectStack[] aspects)` | void | 添加坩埚配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(String name)` | void | 按配方名移除 |
| `.removeRecipe(IItemStack output)` | void | 按输出移除 |

### Infusion（注魔）

> `import mods.thaumcraft.Infusion;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerRecipe(String name, String research, IItemStack output, int instability, CTAspectStack[] aspects, IIngredient centralItem, IIngredient[] recipe)` | void | 添加注魔配方。`instability` 不稳定度 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(String name)` | void | 按配方名移除 |
| `.removeRecipe(IItemStack output)` | void | 按输出移除 |

### LootBag（战利品袋）

> `import mods.thaumcraft.LootBag;`

战利品类型: 0=普通, 1=稀有, 2=史诗

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addLoot(WeightedItemStack stack, int[] bagTypes)` | void | 添加战利品。`bagTypes` 为影响的袋子类型数组 |
| `.removeLoot(IItemStack stack, int[] bagTypes)` | void | 移除战利品 |

### SalisMundus（世界盐）

> `import mods.thaumcraft.SalisMundus;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addSingleConversion(IBlock in, IItemStack out, @Optional String research)` | void | 添加方块转换配方 |
| `.addSingleConversion(IOreDictEntry in, IItemStack out, @Optional String research)` | void | 添加矿辞转换配方 |
| `.removeSingleConversion(IIngredient output)` | void | 移除转换配方（`<*>` 移除所有） |

### SmeltingBonus（冶炼奖励）

> `import mods.thaumcraft.SmeltingBonus;`

炼狱熔炉冶炼物品时触发的额外掉落。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addSmeltingBonus(IIngredient input, WeightedItemStack stack)` | void | 添加冶炼奖励 |
| `.removeSmeltingBonus(IIngredient input, IItemStack stack)` | void | 移除冶炼奖励 |

### Warp（扭曲）

> `import mods.thaumcraft.Warp;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setWarp(IItemStack stack, int amount)` | void | 设置物品的扭曲值 |

### CTAspect（要素）

> `import thaumcraft.aspect.CTAspect;`

通过 `<aspect:name>.internal` 获取。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `chatColour` | string | 聊天颜色 |
| `name` | string | 要素名 |

### CTAspectStack（要素堆）

> `import thaumcraft.aspect.CTAspectStack;`

通过 `<aspect:name>` 获取。

#### @ZenGetter（只读）

| 属性 | 类型 | 说明 |
|------|------|------|
| `amount` | int | 数量 |
| `internal` | CTAspect | 底层要素 |

#### 设置数量

```zenscript
val aspect = <aspect:ignis> * 10;
val aspect1 = <aspect:ignis>.setAmount(10);
```

### 扩展 IEntityDefinition

> Thaumcraft 扩展了 `IEntityDefinition`，可对任何实体使用：

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setAspects(CTAspectStack...)` | void | 设置实体要素（覆盖原有） |
| `.removeAspects(CTAspectStack...)` | void | 移除实体要素 |

### 扩展 IItemStack

> Thaumcraft 扩展了 `IItemStack`，可对任何物品使用：

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setAspects(CTAspectStack...)` | void | 设置物品要素（覆盖原有） |
| `.removeAspects(CTAspectStack...)` | void | 移除物品要素 |

## 命令

| 命令 | 说明 |
|------|------|
| `/ct thaumcraftDump` | 将所有 Thaumcraft 信息输出到 crafttweaker.log |

## 使用示例

### 添加奥术工作台配方

```zenscript
import mods.thaumcraft.ArcaneWorkbench;

ArcaneWorkbench.registerShapedRecipe("test", "", 20, [<aspect:aer>, <aspect:ignis>, <aspect:terra>], <minecraft:diamond>, [[<minecraft:dirt>], [<minecraft:stick>], [<minecraft:grass>]]);
```

### 添加注魔配方

```zenscript
import mods.thaumcraft.Infusion;

Infusion.registerRecipe("testName", "", <minecraft:diamond>, 20, [<aspect:aer>, <aspect:ignis>], <minecraft:grass>, [<minecraft:stick>, <minecraft:dirt>]);
```

### 设置物品和实体要素

```zenscript
<minecraft:stone>.setAspects(<aspect:ignis> * 5);
<entity:blaze>.removeAspects(<aspect:ignis>);
```
