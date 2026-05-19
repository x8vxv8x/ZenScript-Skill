# Ex Sartagine: Requiem CraftTweaker API 参考

> Mod ID: `exsartagine`
> 前置条件: 无
> 导入: `import mods.exsartagine.ExSartagine;`

Ex Sartagine: Requiem 是一个烹饪模组，提供锅、平底锅、冶炼炉和水壶的配方管理。

---

## API 列表

### ExSartagine（主类）

> `import mods.exsartagine.ExSartagine;`

#### 放置方块和热源

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addPlaceable(placeableState as IBlockState)` | void | 添加可放置方块 |
| `.removePlaceable(placeableState as IBlockState)` | void | 移除可放置方块 |
| `.addHeatSource(heatSource as IBlockState)` | void | 添加热源方块（会自动添加到可放置列表） |
| `.removeHeatSource(heatSource as IBlockState)` | void | 移除热源方块 |

#### 锅配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addPotRecipe(input as IIngredient, output as IItemStack)` | void | 添加锅配方 |
| `.removePotRecipe(output as IItemStack)` | void | 按输出移除锅配方 |
| `.removePotRecipe(input as IIngredient, output as IItemStack)` | void | 按输入和输出移除锅配方 |

#### 平底锅配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addPanRecipe(input as IIngredient, output as IItemStack)` | void | 添加平底锅配方 |
| `.removePanRecipe(output as IItemStack)` | void | 按输出移除平底锅配方 |
| `.removePanRecipe(input as IIngredient, output as IItemStack)` | void | 按输入和输出移除平底锅配方 |

#### 冶炼炉配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addSmelterRecipe(input as IIngredient, output as IItemStack)` | void | 添加冶炼炉配方 |
| `.removeSmelterRecipe(output as IItemStack)` | void | 按输出移除冶炼炉配方 |
| `.removeSmelterRecipe(input as IIngredient, output as IItemStack)` | void | 按输入和输出移除冶炼炉配方 |

#### 水壶配方

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addKettleRecipe(inputs as IIngredient[], @Nullable catalyst as IIngredient, @Nullable fluid as ILiquidStack, outputs as IItemStack[], @Optional time as int)` | void | 添加水壶配方 |

**参数说明**:
- `inputs`: 输入材料数组
- `catalyst`: 催化剂（可为null）
- `fluid`: 流体（可为null）
- `outputs`: 输出物品数组
- `time`: 时间（可选）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeKettleRecipe(output as IItemStack)` | void | 按输出移除水壶配方 |
| `.removeKettleRecipe(outputs as IItemStack[])` | void | 按输出数组移除水壶配方 |
| `.removeKettleRecipe(inputs as IIngredient[], catalyst as IIngredient, outputs as IItemStack[], @Optional time as int)` | void | 按参数移除水壶配方 |
| `.removeKettleRecipe(inputs as IIngredient[], catalyst as IIngredient, fluid as ILiquidStack, outputs as IItemStack[], @Optional time as int)` | void | 按参数移除水壶配方 |