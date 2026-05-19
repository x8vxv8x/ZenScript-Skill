# Blood Magic CraftTweaker API 参考

> Mod ID: `bloodmagic`
> 前置条件: Modtweaker
> 导入: `import mods.bloodmagic.*;`

## API 列表

### BloodAltar（血之祭坛）

> `import mods.bloodmagic.BloodAltar;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, int minimumTier, int syphon, int consumeRate, int drainRate)` | void | 添加血之祭坛配方。`minimumTier` 祭坛等级(JEI显示-1)。`syphon` 消耗 LP 总量。`consumeRate` LP 吸收速率。`drainRate` LP 不足时进度流失速率 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack input)` | void | 按输入移除配方 |

### AlchemyArray（炼金矩阵）

> `import mods.bloodmagic.AlchemyArray;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, IItemStack catalyst, @Optional string textureLocation)` | void | 添加炼金矩阵配方。`input` 先放置的物品，`catalyst` 后放置的催化剂 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack input, IItemStack catalyst)` | void | 按输入和催化剂移除配方 |

### AlchemyTable（炼金术桌）

> `import mods.bloodmagic.AlchemyTable;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack[] inputs, int syphon, int ticks, int minTier)` | void | 添加配方。`inputs` 最多 6 个 |
| `.addPotionRecipe(IItemStack[] inputs, IPotionEffect effects, int syphon, int ticks, int minTier)` | void | 添加药水配方。`inputs` 最多 5 个（需留位给催化剂） |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack[] inputs)` | void | 按输入移除配方 |

### TartaricForge（狱火熔炉）

> `import mods.bloodmagic.TartaricForge;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack[] inputs, double minSouls, double soulDrain)` | void | 添加狱火熔炉配方。`inputs` 最多 4 个。`minSouls` 最低灵魂需求。`soulDrain` 每次合成消耗灵魂 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack[] inputs)` | void | 按输入移除配方 |

## 使用示例

### 添加血之祭坛配方

```zenscript
import mods.bloodmagic.BloodAltar;

// T1 等级(填0)，消耗 20 LP，吸收速率 30，流失速率 40
BloodAltar.addRecipe(<minecraft:glass>, <minecraft:stick>, 0, 20, 30, 40);
```

### 添加狱火熔炉配方

```zenscript
import mods.bloodmagic.TartaricForge;

// 最多 4 个输入，最低 10 灵魂，每次消耗 10 灵魂
TartaricForge.addRecipe(<minecraft:diamond>, [<minecraft:dirt>, <minecraft:dirt>, <minecraft:dirt>, <minecraft:dirt>], 10, 10);
```
