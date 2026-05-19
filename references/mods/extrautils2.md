# Extra Utilities 2 CraftTweaker API 参考

> Mod ID: `extrautils2`
> 前置条件: Modtweaker
> 导入: `import mods.extrautils2.*;`

## API 列表

### Crusher（粉碎机）

> `import mods.extrautils2.Crusher;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IItemStack input, @Optional IItemStack secondaryOutput, @Optional float secondaryChance)` | void | 添加粉碎配方，可选副产物及概率 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(IItemStack output)` | void | 按输出移除配方 |

### Resonator（共振仪）

> `import mods.extrautils2.Resonator;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IItemStack input, int energy, @Optional boolean addOwnerTag)` | void | 添加共振仪配方。`energy` 为能量消耗（1 GP = 100 energy）。`addOwnerTag` 是否添加所有者标签 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(IItemStack output)` | void | 按输出移除配方 |

## 使用示例

### 添加粉碎机配方

```zenscript
import mods.extrautils2.Crusher;

// 金块粉碎为 9 个金锭，10% 概率产出铁锭
Crusher.add(<minecraft:gold_ingot> * 9, <minecraft:gold_block>, <minecraft:iron_ingot>, 0.1f);

// 无副产物
Crusher.add(<minecraft:iron_ingot> * 9, <minecraft:iron_block>);
```

### 添加共振仪配方

```zenscript
import mods.extrautils2.Resonator;

// 1 GP = 100 energy，金块转化为红石块消耗 100 energy (1 GP)
Resonator.add(<minecraft:redstone_block>, <minecraft:gold_block>, 100);

// 不添加所有者标签
Resonator.add(<minecraft:gold_block>, <minecraft:iron_block>, 200, false);
```
