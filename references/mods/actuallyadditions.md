# Actually Additions CraftTweaker API 参考

> Mod ID: `actuallyadditions`
> 前置条件: Modtweaker
> 导入: `import mods.actuallyadditions.*;`

## API 列表

### AtomicReconstructor（原子再构机器）

> `import mods.actuallyadditions.AtomicReconstructor;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, int energyUsed)` | void | 添加原子再构机配方，`energyUsed` 为消耗能量 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 按输出移除配方 |

### BallOfFur（毛球掉落）

> `import mods.actuallyadditions.BallOfFur;`

#### 掉落添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addReturn(IItemStack output, int chance)` | void | 添加毛球掉落物，`chance` 为权重 |

#### 掉落移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeReturn(IItemStack output)` | void | 按输出移除掉落物 |

### Compost（堆肥）

> `import mods.actuallyadditions.Compost;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack outputDisplay, IItemStack input, IItemStack inputDisplay)` | void | 添加堆肥配方，`outputDisplay`/`inputDisplay` 为 JEI 显示用 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 按输出移除配方 |

### Crusher（粉碎机）

> `import mods.actuallyadditions.Crusher;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, @Optional IItemStack outputSecondary, @Optional int outputSecondaryChance)` | void | 添加粉碎配方，可选副产物及概率 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 按输出移除配方 |

### Empowerer（充能台）

> `import mods.actuallyadditions.Empowerer;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, IItemStack modifier1, IItemStack modifier2, IItemStack modifier3, IItemStack modifier4, int energyPerStand, int time)` | void | 添加充能配方 |
| `.addRecipe(IItemStack output, IItemStack input, IItemStack modifier1, IItemStack modifier2, IItemStack modifier3, IItemStack modifier4, int energyPerStand, int time, float[] particleColourArray)` | void | 添加充能配方（自定义粒子颜色，RGB 数组） |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 按输出移除配方 |

### MiningLens（采矿透镜）

> `import mods.actuallyadditions.MiningLens;`

#### 矿石添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addStoneOre(IOreDictEntry ore, int weight)` | void | 添加主世界采矿透镜矿石，`weight` 为权重 |
| `.addNetherOre(IOreDictEntry ore, int weight)` | void | 添加下界采矿透镜矿石，`weight` 为权重 |

#### 矿石移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeStoneOre(IOreDictEntry ore)` | void | 移除主世界矿石 |
| `.removeNetherOre(IOreDictEntry ore)` | void | 移除下界矿石 |

### OilGen（原油发电机）

> `import mods.actuallyadditions.OilGen;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack fluid, int genAmount)` | void | 添加燃油配方，`genTime` 默认 100 |
| `.addRecipe(ILiquidStack fluid, int genAmount, int genTime)` | void | 添加燃油配方，`genTime` 为发电时长(tick) |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(ILiquidStack output)` | void | 按流体移除配方 |

### TreasureChest（藏宝箱）

> `import mods.actuallyadditions.TreasureChest;`

#### 掉落添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addLoot(IItemStack returnItem, int chance, int minAmount, int maxAmount)` | void | 添加藏宝箱掉落物 |

#### 掉落移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeLoot(IItemStack returnItem)` | void | 按物品移除掉落物 |

## 使用示例

### 添加原子再构机配方

```zenscript
import mods.actuallyadditions.AtomicReconstructor;

// 将煤炭转化为火焰弹，消耗 1000 能量
AtomicReconstructor.addRecipe(<minecraft:fire_charge>, <minecraft:coal:1>, 1000);
```

### 添加粉碎机配方

```zenscript
import mods.actuallyadditions.Crusher;

// 粉碎铁矿石，50% 概率产出圆石作为副产物
Crusher.addRecipe(<minecraft:iron_ingot>, <minecraft:iron_ore>, <minecraft:stone>, 50);
```

### 添加充能台配方

```zenscript
import mods.actuallyadditions.Empowerer;

// 每个支架消耗 500 能量，100 tick 完成
Empowerer.addRecipe(<minecraft:iron_ingot>, <minecraft:leaves>, <minecraft:redstone>, <minecraft:redstone>, <minecraft:redstone>, <minecraft:redstone>, 500, 100);
```
