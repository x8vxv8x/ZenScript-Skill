# BedrockCraft CraftTweaker API 参考

> Mod ID: `bedrockcraft`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.bedrockcraft.*;`

## API 列表

### DustInfusion（粉尘灌注）

> `import moretweaker.bedrockcraft.DustInfusion;`

`block` 为目标方块（需要点击的方块）。配方按 `block` 移除，而非按输出。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack block, IItemStack output)` | void | 添加粉尘灌注配方 |
| `.removeRecipe(IItemStack block)` | void | 按目标方块移除配方 |

### BedrockRitual（基岩仪式）

> `import moretweaker.bedrockcraft.BedrockRitual;`

`inputs` 数组长度必须为 2、3、4、6 或 12。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient center, int bedrockAmount, IIngredient[] inputs)` | void | 添加基岩仪式配方。`center` 为中心物品，`bedrockAmount` 为所需基岩数量 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |
