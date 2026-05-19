# Tinkers' Complement CraftTweaker API 参考

> Mod ID: `tcomplement`
> 前置条件: Modtweaker
> 导入: `import mods.tcomplement.*;`

## API 列表

### Blacklist（冶炼炉黑名单）

> `import mods.tcomplement.Blacklist;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, IItemStack input)` | void | 将物品加入冶炼炉黑名单（禁止熔炼） |
| `.removeRecipe(IItemStack input)` | void | 将物品从黑名单移除 |

### Overrides（熔炼器覆盖）

> `import mods.tcomplement.Overrides;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, IItemStack input, @Optional int temp)` | void | 添加熔炼覆盖配方。`temp` 可选温度 |
| `.removeRecipe(ILiquidStack output, @Optional IItemStack input)` | void | 按输出移除覆盖配方 |

### HighOven（高炉）

> `import mods.tcomplement.highoven.HighOven;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(IIngredient fuel, int time, int rate)` | void | 添加高炉燃料。`time` 持续时间(秒)。`rate` 每秒温度增量 |
| `.removeFuel(IIngredient fuel)` | void | 移除高炉燃料 |
| `.addMeltingOverride(ILiquidStack output, IIngredient input, @Optional int temp)` | void | 添加熔炼覆盖。`temp` 最低熔炼温度(K) |
| `.removeMeltingOverride(ILiquidStack output, @Optional IItemStack input)` | void | 移除熔炼覆盖 |
| `.addHeatRecipe(ILiquidStack output, ILiquidStack input, int temp)` | void | 添加热量配方（流体转换）。`temp` 最低温度(K) |
| `.removeHeatRecipe(ILiquidStack output, @Optional ILiquidStack input)` | void | 移除热量配方 |
| `.newMixRecipe(ILiquidStack output, ILiquidStack input, int temp)` | MixRecipeBuilder | 创建混合配方构建器 |
| `.removeMixRecipe(ILiquidStack output, @Optional ILiquidStack input)` | void | 移除混合配方 |
| `.manageMixRecipe(ILiquidStack output, @Optional ILiquidStack input)` | MixRecipeManager | 获取混合配方管理器 |

### MixRecipeBuilder（混合配方构建器）（添加高炉合金配方或者冶炼炉合金配方时使用）

> `import mods.tcomplement.highoven.MixRecipeBuilder;`

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `output` | ILiquidStack | 输出流体 |
| `input` | ILiquidStack | 输入流体 |
| `temp` | int | 最低温度(K) |

#### @ZenGetter（只读）

| 属性 | 类型 | 说明 |
|------|------|------|
| `oxidizers` | List\<IIngredient\> | 氧化剂列表 |
| `reducers` | List\<IIngredient\> | 还原剂列表 |
| `purifiers` | List\<IIngredient\> | 净化剂列表 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addOxidizer(IIngredient oxidizer, int consumeChance)` | MixRecipeBuilder | 添加氧化剂。`consumeChance` 消耗概率(%) |
| `.addReducer(IIngredient reducer, int consumeChance)` | MixRecipeBuilder | 添加还原剂 |
| `.addPurifier(IIngredient purifier, int consumeChance)` | MixRecipeBuilder | 添加净化剂 |
| `.removeOxidizer(IIngredient oxidizer)` | MixRecipeBuilder | 移除氧化剂 |
| `.removeReducer(IIngredient reducer)` | MixRecipeBuilder | 移除还原剂 |
| `.removePurifier(IIngredient purifier)` | MixRecipeBuilder | 移除净化剂 |
| `.removeAllOxidizer()` | MixRecipeBuilder | 移除所有氧化剂 |
| `.removeAllReducer()` | MixRecipeBuilder | 移除所有还原剂 |
| `.removeAllPurifier()` | MixRecipeBuilder | 移除所有净化剂 |
| `.register()` | void | 注册配方（**必须调用**） |

### MixRecipeManager（混合配方管理器）

> `import mods.tcomplement.highoven.MixRecipeManager;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeOxidizer(IIngredient oxidizer)` | MixRecipeManager | 强制移除氧化剂 |
| `.removeReducer(IIngredient reducer)` | MixRecipeManager | 强制移除还原剂 |
| `.removePurifier(IIngredient purifier)` | MixRecipeManager | 强制移除净化剂 |
| `.addOxidizer(IIngredient oxidizer, int consumeChance)` | MixRecipeManager | 添加氧化剂 |
| `.addReducer(IIngredient reducer, int consumeChance)` | MixRecipeManager | 添加还原剂 |
| `.addPurifier(IIngredient purifier, int consumeChance)` | MixRecipeManager | 添加净化剂 |

**注意**: 移除优先于添加。移除矿辞中的某个物品会阻止整个矿辞被添加。

## 使用示例

### 添加高炉燃料和热量配方

```zenscript
import mods.tcomplement.highoven.HighOven;

HighOven.addFuel(<minecraft:hay_block>, 3600, 5);
HighOven.addHeatRecipe(<liquid:iron> * 144, <liquid:lava> * 1000, 1450);
```

### 向高炉添加混合配方

```zenscript
import mods.tcomplement.highoven.HighOven;
import mods.tcomplement.highoven.MixRecipeBuilder;

var builder = HighOven.newMixRecipe(<liquid:steel> * 72, <liquid:iron> * 144, 1350);
builder.addOxidizer(<minecraft:redstone>, 95);
builder.addReducer(<minecraft:glowstone>, 5);
builder.addPurifier(<ore:dustCoal>, 50);
builder.register();
```
