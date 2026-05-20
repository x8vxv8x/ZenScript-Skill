# LightningCraft CraftTweaker API 参考

> Mod ID: `lightningcraft`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.lightningcraft.*;`

## API 列表

### LightningTransforming（闪电转化）

> `import moretweaker.lightningcraft.LightningTransforming;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IItemStack[] inputs)` | void | 添加闪电转化配方 |

### LightningCrusher（LE粉碎机）

> `import moretweaker.lightningcraft.LightningCrusher;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IIngredient input)` | void | 添加粉碎配方 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### LightningInfusion（LE灌注）

> `import moretweaker.lightningcraft.LightningInfusion;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IIngredient catalyst, int requiredLE, IIngredient[] inputs)` | void | 添加灌注配方。`catalyst` 为催化剂，`requiredLE` 为所需闪电能量，`inputs` 为周围材料 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |
