# Modular Machinery CraftTweaker API 参考

> 模块化机械，不是社区版，提醒用户区分。一定向用户询问安装的模组的类型！
> Mod ID: `modularmachinery`
> 前置条件: 无
> 导入: `import mods.modularmachinery.RecipeBuilder;` / `import mods.modularmachinery.RecipePrimer;`

## API 列表

### RecipeBuilder

> `import mods.modularmachinery.RecipeBuilder;`

用于创建 RecipePrimer 对象。

#### 创建方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.newBuilder(String recipeRegistryName, String associatedMachineRegistryName, int processingTickTime)` | RecipePrimer | 创建新的配方对象 |
| `.newBuilder(String recipeRegistryName, String associatedMachineRegistryName, int processingTickTime, int sortingPriority)` | RecipePrimer | 创建新的配方对象，带排序优先级 |

### RecipePrimer

> `import mods.modularmachinery.RecipePrimer;`

配方对象，支持链式调用（每个方法返回自身）。

#### 设置方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setChance(float chance)` | RecipePrimer | 设置配方概率 |
| `.addEnergyPerTickInput(int perTick)` | RecipePrimer | 添加每 tick 能量输入 |
| `.addEnergyPerTickOutput(int perTick)` | RecipePrimer | 添加每 tick 能量输出 |
| `.addFuelItemInout(int requiredTotalBurnTime)` | RecipePrimer | 添加燃料物品需求（总燃烧时间） |

#### 添加输入

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addItemInput(IItemStack stack)` | RecipePrimer | 添加物品输入 |
| `.addItemInput(IOreDictEntry oreDict)` | RecipePrimer | 添加矿辞输入（数量为 1） |
| `.addItemInput(IOreDictEntry oreDict, int amount)` | RecipePrimer | 添加指定数量的矿辞输入 |
| `.addFluidInput(ILiquidStack stack)` | RecipePrimer | 添加流体输入 |

#### 添加输出

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addItemOutput(IItemStack stack)` | RecipePrimer | 添加物品输出 |
| `.addItemOutput(IOreDictEntry oreDict)` | RecipePrimer | 添加矿辞输出（数量为 1） |
| `.addItemOutput(IOreDictEntry oreDict, int amount)` | RecipePrimer | 添加指定数量的矿辞输出 |
| `.addFluidOutput(ILiquidStack stack)` | RecipePrimer | 添加流体输出 |

#### 构建

| 方法 | 返回 | 说明 |
|------|------|------|
| `.build()` | void | 构建并注册配方。必须调用此方法配方才会生效 |

## 使用示例

### 分步调用

```zenscript
import mods.modularmachinery.RecipeBuilder;

val reci = mods.modularmachinery.RecipeBuilder.newBuilder("my_recipe", "my_machine", 1000, 0);

reci.addEnergyPerTickInput(100);
reci.addItemInput(<ore:ingotIron>);
reci.addItemOutput(<minecraft:gold_ingot>);
reci.build();
```

### 链式调用

```zenscript
import mods.modularmachinery.RecipeBuilder;

mods.modularmachinery.RecipeBuilder.newBuilder("another_recipe", "my_machine", 1000, 0)
    .addEnergyPerTickInput(100)
    .addFluidInput(<liquid:water> * 1000)
    .addFluidInput(<liquid:lava> * 1000)
    .addItemOutput(<minecraft:obsidian> * 2)
    .build();
```
