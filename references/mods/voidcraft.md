# VoidCraft CraftTweaker API 参考

> Mod ID: `voidcraft`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.voidcraft.*;`

## API 列表

### VoidMacerator（虚空打粉机）

> `import moretweaker.voidcraft.VoidMacerator;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IIngredient input, optional int voidicPower)` | void | 添加研磨配方。`voidicPower` 为虚空能量消耗 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### VoidFurnace（虚空高炉）

> `import moretweaker.voidcraft.VoidFurnace;`

可添加自定义配方，但只能将铁粉和煤粉放入槽位。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IIngredient input1, IIngredient input2, optional int voidicPower)` | void | 添加高炉配方。`voidicPower` 为虚空能量消耗 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### VoidAlchemy（虚空炼金台）

> `import moretweaker.voidcraft.VoidAlchemy;`

`inputs` 数组长度必须为 6。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IIngredient[] inputs, optional int voidicPower)` | void | 添加炼金配方。`voidicPower` 为虚空能量消耗 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |

### VoidInfusion（虚空灌注）

> `import moretweaker.voidcraft.VoidInfusion;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IIngredient input, int voidicFluid)` | void | 添加灌注配方。`voidicFluid` 为虚空流体消耗 |
| `.remove(IIngredient output)` | void | 按输出移除配方 |
| `.removeAll()` | void | 移除所有配方 |
