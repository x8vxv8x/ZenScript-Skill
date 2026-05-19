# Botania CraftTweaker API 参考

> Mod ID: `botania`
> 前置条件: Modtweaker
> 导入: `import mods.botania.*;`

## API 列表

### Apothecary（花药台）

> `import mods.botania.Apothecary;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient[] input)` | void | 添加配方 |
| `.addRecipe(String output, IIngredient[] input)` | void | 添加配方（Botania 花名） |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 按输出移除配方 |
| `.removeRecipe(String output)` | void | 按花名移除配方 |

**注意**: 花药台**硬编码只接受花瓣**，虽然可以用任何物品添加配方，但只能投掷花瓣进去。

### Brew（酿造）

> `import mods.botania.Brew;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient[] input, String brewName)` | void | 添加酿造配方。`brewName` 为 Botania 注册的酿造名，可用 `/ct botbrews` 查看 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(String brewName)` | void | 按酿造名移除配方 |

### ElvenTrade（精灵交易）

> `import mods.botania.ElvenTrade;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient[] outputs, IIngredient[] input)` | void | 添加精灵交易配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |

### ManaInfusion（魔力灌注）

> `import mods.botania.ManaInfusion;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addInfusion(IItemStack output, IIngredient input, int mana)` | void | 添加魔力池灌注配方 |
| `.addAlchemy(IItemStack output, IIngredient input, int mana)` | void | 添加炼金催化配方 |
| `.addConjuration(IItemStack output, IIngredient input, int mana)` | void | 添加炼造催化配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |

### Orechid（矿石花）

> `import mods.botania.Orechid;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addOre(IOreDictEntry oreDict, int weight)` | void | 添加矿石花生成矿石。`weight` 为权重，**相同权重的两个配方会导致游戏崩溃** |
| `.addOre(String oreDict, int weight)` | void | 同上，使用字符串矿辞名 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeOre(IOreDictEntry oreDict)` | void | 按矿辞移除配方 |
| `.removeOre(String oreDict)` | void | 同上，使用字符串矿辞名 |

### OrechidIgnem（凝矿兰）

> `import mods.botania.OrechidIgnem;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addOre(IOreDictEntry oreDict, int weight)` | void | 添加凝矿兰生成矿石 |
| `.addOre(String oreDict, int weight)` | void | 同上，使用字符串矿辞名 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeOre(IOreDictEntry oreDict)` | void | 按矿辞移除配方 |
| `.removeOre(String oreDict)` | void | 同上，使用字符串矿辞名 |

### PureDaisy（白雏菊）

> `import mods.botania.PureDaisy;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient blockInput, IItemStack blockOutput, @Optional int time)` | void | 添加白雏菊配方。`time` 默认 150 tick |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |

### RuneAltar（符文祭坛）

> `import mods.botania.RuneAltar;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient[] input, int mana)` | void | 添加符文祭坛配方 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |

### Lexicon（植物魔法辞典）

> `import mods.botania.Lexicon;`

#### 页面添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addBrewPage(String name, String entry, int page_number, String brew, IIngredient[] recipe, String bottomText)` | void | 添加酿造页面 |
| `.addCraftingPage(String name, String entry, int page_number, String... recipeNames)` | void | 添加合成页面 |
| `.addElvenPage(String name, String entry, int page_number, IItemStack[] outputs, IIngredient[][] inputs)` | void | 添加精灵交易页面 |
| `.addEntityPage(String name, String entry, int page_number, String entity, int size)` | void | 添加实体页面 |
| `.addImagePage(String name, String entry, int page_number, String resource)` | void | 添加图片页面 |
| `.addLorePage(String name, String entry, int page_number)` | void | 添加传说页面 |
| `.addInfusionPage(String name, String entry, int page_number, IItemStack[] outputs, IIngredient[] inputs, int[] mana)` | void | 添加魔力注入页面 |
| `.addAlchemyPage(String name, String entry, int page_number, IItemStack[] outputs, IIngredient[] inputs, int[] mana)` | void | 添加炼金催化页面 |
| `.addConjurationPage(String name, String entry, int page_number, IItemStack[] outputs, IIngredient[] inputs, int[] mana)` | void | 添加复制催化页面 |
| `.addPetalPage(String name, String entry, int page_number, IItemStack[] outputs, IIngredient[][] inputs)` | void | 添加花瓣台页面 |
| `.addRunePage(String name, String entry, int page_number, IItemStack[] outputs, IIngredient[][] inputs, int[] mana)` | void | 添加符文祭坛页面 |
| `.addTextPage(String name, String entry, int page_number)` | void | 添加文本页面 |

#### 页面移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removePage(String entry, int page_number)` | void | 移除指定页面 |

#### 条目管理方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addEntry(String entry, String catagory, IItemStack stack)` | void | 添加辞典条目 |
| `.removeEntry(String entry)` | void | 移除辞典条目 |

#### 分类管理方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addCategory(String name)` | void | 添加辞典分类 |
| `.removeCategory(String name)` | void | 移除辞典分类 |
| `.setCategoryIcon(String name, String icon)` | void | 设置分类图标 |

#### 配方映射方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipeMapping(IItemStack stack, String Entry, int page)` | void | 添加配方映射 |
| `.removeRecipeMapping(IItemStack stack)` | void | 移除配方映射 |

## 使用示例

### 添加花药台配方

```zenscript
import mods.botania.Apothecary;

Apothecary.addRecipe(<minecraft:melon>, [<ore:petalLime>, <ore:petalLime>, <ore:petalLime>]);
```

### 添加魔力灌注配方

```zenscript
import mods.botania.ManaInfusion;

ManaInfusion.addInfusion(<minecraft:grass>, <ore:stone>, 1000);
ManaInfusion.addAlchemy(<minecraft:gold_ore>, <ore:stone>, 5000);
ManaInfusion.addConjuration(<minecraft:stone>, <minecraft:stone>, 1000);
```

### 添加符文祭坛配方

```zenscript
import mods.botania.RuneAltar;

RuneAltar.addRecipe(<minecraft:planks>, [<minecraft:grass>, <minecraft:dirt>], 200);
```
