# JEI CraftTweaker API 参考

> Mod ID: `jei`
> 前置条件: 无
> 导入: `import mods.jei.JEI;`

## API 列表

### JEI

> `import mods.jei.JEI;`

#### 隐藏方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.hide(IItemStack item)` | void | 从 JEI 中隐藏指定物品 |
| `.hide(ILiquidStack liquid)` | void | 从 JEI 中隐藏指定流体 |
| `.removeAndHide(IIngredient output)` | void | 从 JEI 中隐藏物品/流体，同时移除其所有合成台配方 |
| `.removeAndHide(IIngredient output, bool NBTMatch)` | void | 同上，可指定是否匹配 NBT |
| `.hideCategory(String category)` | void | 隐藏整个 JEI 分类。可用 `/ct jeiCategories` 查看所有已注册分类 |

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addItem(IItemStack item)` | void | 向 JEI 添加物品（适用于未自动添加的物品或带 NBT 的物品） |
| `.addDescription(IItemStack item, string... desc)` | void | 为物品添加 JEI 描述页面 |
| `.addDescription(IItemStack[] items, string... desc)` | void | 为多个物品添加共享的 JEI 描述页面 |
| `.addDescription(IOreDictEntry dict, string... desc)` | void | 为矿辞条目添加 JEI 描述页面 |
| `.addDescription(ILiquidStack liquid, string... desc)` | void | 为流体添加 JEI 描述页面 |

## 使用示例

### 隐藏物品

```zenscript
import mods.jei.JEI;

// 隐藏钻石
mods.jei.JEI.hide(<minecraft:diamond>);

// 隐藏流体
mods.jei.JEI.hide(<liquid:water>);

// 隐藏物品并移除配方
mods.jei.JEI.removeAndHide(<minecraft:iron_leggings>);
```

### 添加描述

```zenscript
import mods.jei.JEI;

// 为铁锭添加描述
mods.jei.JEI.addDescription(<minecraft:iron_ingot>, "这是铁锭的描述文本");

// 为矿辞添加描述（支持多段文本）
mods.jei.JEI.addDescription(<ore:ingotIron>, "你可以用这些来创造东西", "", "比如盔甲...");
```
