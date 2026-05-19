# Applied Energistics 2 CraftTweaker API 参考

> Mod ID: `appliedenergistics2`
> 前置条件: 无
> 导入: `import mods.appliedenergistics2.<ClassName>;`

## API 列表

### Cannon（物质炮）

> `import mods.appliedenergistics2.Cannon;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerAmmo(IItemStack ammo, double weight)` | void | 注册物质炮弹药。`weight` 为材料重量（约等于原子量） |

### Grinder（石英磨具）

> `import mods.appliedenergistics2.Grinder;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, int turns, @Optional IItemStack secondary1Output, @Optional float secondary1Chance, @Optional IItemStack secondary2Output, @Optional float secondary2Chance)` | void | 添加研磨配方 |
| `.removeRecipe(IItemStack input)` | void | 移除指定输入的配方 |

### Inscriber（压印器）

> `import mods.appliedenergistics2.Inscriber;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, boolean inscribe, @Optional IItemStack topInput, @Optional IItemStack bottomInput)` | void | 添加压印配方。`inscribe` 为刻印模式（true 时不消耗上下输入） |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |

### Attunement（P2P 调谐）

> `import mods.appliedenergistics2.Attunement;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.attuneME(IItemStack item)` | void | 将物品绑定到 ME P2P 隧道 |
| `.attuneME(String modID)` | void | 将模组绑定到 ME P2P 隧道 |
| `.attuneItem(IItemStack item)` | void | 将物品绑定到物品 P2P 隧道 |
| `.attuneItem(String modID)` | void | 将模组绑定到物品 P2P 隧道 |
| `.attuneFluid(IItemStack item)` | void | 将物品绑定到流体 P2P 隧道 |
| `.attuneFluid(String modID)` | void | 将模组绑定到流体 P2P 隧道 |
| `.attuneRedstone(IItemStack item)` | void | 将物品绑定到红石 P2P 隧道 |
| `.attuneRedstone(String modID)` | void | 将模组绑定到红石 P2P 隧道 |
| `.attuneRF(IItemStack item)` | void | 将物品绑定到 RF P2P 隧道 |
| `.attuneRF(String modID)` | void | 将模组绑定到 RF P2P 隧道 |
| `.attuneIC2(IItemStack item)` | void | 将物品绑定到 EU P2P 隧道 |
| `.attuneIC2(String modID)` | void | 将模组绑定到 EU P2P 隧道 |
| `.attuneLight(IItemStack item)` | void | 将物品绑定到光照 P2P 隧道 |
| `.attuneLight(String modID)` | void | 将模组绑定到光照 P2P 隧道 |

### Spatial（空间 IO）

> `import mods.appliedenergistics2.Spatial;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.whitelistEntity(String fullEntityClassName)` | void | 将 TileEntity 类添加到空间 IO 白名单 |

**警告：** 某些 TileEntity（尤其是多方块结构）在空间 IO 中移动时可能导致意外错误或崩溃，请充分测试。

## 使用示例

### 示例一：石英磨具配方

```zenscript
import mods.appliedenergistics2.Grinder;

// 添加研磨配方：树叶研磨成树苗，30% 概率获得丛林树苗
Grinder.addRecipe(<minecraft:sapling>, <minecraft:leaves>, 4, <minecraft:sapling:5>, 0.3);

// 移除石英矿石的研磨配方
Grinder.removeRecipe(<minecraft:quartz_ore>);
```

### 示例二：压印器配方

```zenscript
import mods.appliedenergistics2.Inscriber;

// 刻印模式：用凋灵骷髅头将蛋变成凋灵骷髅刷怪蛋（不消耗骷髅头）
Inscriber.addRecipe(<minecraft:spawn_egg:5>, <minecraft:egg>, true, <minecraft:skull:1>);

// 合成模式：合成饼干（消耗所有输入）
Inscriber.addRecipe(<minecraft:cookie>, <minecraft:bread>, false, <minecraft:dye:3>, <minecraft:sugar>);

// 移除印刷硅配方
Inscriber.removeRecipe(<appliedenergistics2:material:20>);
```

### 示例三：P2P 调谐

```zenscript
import mods.appliedenergistics2.Attunement;

// 使用物品调谐 ME P2P
Attunement.attuneME(<appliedenergistics2:controller>);

// 使用模组 ID 调谐 ME P2P
Attunement.attuneME("actuallyadditions");

// 调谐其他类型 P2P
Attunement.attuneItem(<minecraft:chest>);
Attunement.attuneFluid(<minecraft:bucket>);
Attunement.attuneRedstone(<minecraft:redstone>);
```

### 示例四：物质炮弹药

```zenscript
import mods.appliedenergistics2.Cannon;

// 注册骨头作为物质炮弹药，重量 40.07
Cannon.registerAmmo(<minecraft:bone>, 40.07);
```

### 示例五：空间 IO 白名单

```zenscript
import mods.appliedenergistics2.Spatial;

// 将 Actually Additions 的小存储箱添加到空间 IO 白名单
Spatial.whitelistEntity("de.ellpeck.actuallyadditions.mod.tile.TileEntityGiantChest");
```

## 注意事项

- 压印器的刻印模式（inscribe=true）不消耗顶部和底部输入
- 石英磨具支持最多两个副产物，每个副产物有独立的产出概率
- P2P 调谐支持物品和模组 ID 两种方式，模组 ID 作为后备方案
- 空间 IO 白名单添加 TileEntity 时需要谨慎，某些多方块结构可能导致问题
