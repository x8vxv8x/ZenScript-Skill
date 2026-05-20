# Draconic Evolution CraftTweaker API 参考

> Mod ID: `draconicevolution`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.draconicevolution.*;`

## API 列表

### FusionCrafting（聚合核心）

> `import moretweaker.draconicevolution.FusionCrafting;`

催化剂（catalyst）为配方开始前放置在中心的物品。

#### 配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IItemStack catalyst, int tier, long energyCost, IIngredient[] ingredients)` | void | 添加聚合配方。`tier` 为等级，`energyCost` 为能量消耗，`ingredients` 为周围材料 |
| `.remove(IIngredient catalyst)` | void | 按催化剂移除配方 |
| `.removeAll()` | void | 移除所有配方 |

#### 等级字段

`tier` 参数的值存储在 `FusionCrafting` 类的字段中：

| 字段 | 说明 |
|------|------|
| `FusionCrafting.BASIC` | 基础等级 |
| `FusionCrafting.WYVERN` | 飞龙等级 |
| `FusionCrafting.DRACONIC` | 龙素等级 |
| `FusionCrafting.CHAOTIC` | 混沌等级 |

## 使用示例

```zenscript
import moretweaker.draconicevolution.FusionCrafting;

// 将煤炭通过飞龙等级聚合为钻石，消耗 100000 能量，需要两个石头作为材料
FusionCrafting.add(<minecraft:diamond>, <minecraft:coal>, FusionCrafting.WYVERN, 100000, [<minecraft:stone>, <minecraft:stone>]);
```
