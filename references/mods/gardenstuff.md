# Garden Stuff CraftTweaker API 参考

> Mod ID: `gardenstuff`
> 前置条件: 无
> 导入: `import mods.gardenstuff.CompostBin;`

Garden Stuff 是一个花园相关模组集合，原版 CraftTweaker 集成。

---

## API 列表

### CompostBin（堆肥箱）

> `import mods.gardenstuff.CompostBin;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack item, int processTime)` | void | 添加可堆肥物品。processTime 为基准机器每 tick 产生的能量 |
| `.add(IOreDictEntry oredictKey, int processTime)` | void | 添加可堆肥的矿辞条目 |

---

## 使用示例

### 示例一：添加堆肥物品

```zenscript
import mods.gardenstuff.CompostBin;

// 添加胡萝卜为可堆肥物品，每 tick 产生 150 能量
mods.gardenstuff.CompostBin.add(<minecraft:carrot>, 150);

// 使用矿辞添加所有胡萝卜类物品
mods.gardenstuff.CompostBin.add(<ore:cropCarrot>, 150);
```
