# Heterorustichromia CraftTweaker API 参考

> Mod ID: `rustichromia`
> 前置条件: 无
> 导入: 见各机器章节

Heterorustichromia 添加了多种机器，包括石磨、轧棉机和组装机。

---

## API 列表

### Quern（石磨）

> `import mods.rustichromia.Quern;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(String id, IIngredient[] inputs, result[] outputs, double minPower, double maxPower, double time)` | void | 添加石磨配方。`id` 为配方 ID，`inputs` 为输入物品数组，`outputs` 为输出（支持 IItemStack、WeightedItemStack、IBlockState），`minPower`/`maxPower` 为功率范围，`time` 为加工时间 |
| `.remove(String id)` | void | 移除指定 ID 的配方 |
| `.removeAll()` | void | 移除所有配方 |

### Gin（轧棉机）

> `import mods.rustichromia.Gin;`

注意：内部缓冲区只有在轧棉机关闭（无功率输入）时才会弹出。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(String id, IIngredient[] inputs, result[] internal, result[] external, double minPower, double maxPower, double time)` | void | 添加轧棉机配方。`internal` 为内部缓冲区输出，`external` 为外部输出 |
| `.remove(String id)` | void | 移除指定 ID 的配方 |
| `.removeAll()` | void | 移除所有配方 |

### Assembler（组装机）

> `import mods.rustichromia.Assembler;`

注意：Tier 1 有 2 个输入槽，Tier 2 有 4 个输入槽，Tier 3 有 6 个输入槽。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(String id, int tier, IIngredient[] inputs, result[] outputs, double minPower, double maxPower, double time)` | void | 添加组装机配方。`tier` 为等级（1-3） |
| `.remove(String id)` | void | 移除指定 ID 的配方 |
| `.removeAll()` | void | 移除所有配方 |
