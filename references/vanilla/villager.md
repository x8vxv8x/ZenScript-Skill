# Villager CraftTweaker API 参考

> Mod ID: `roidtweaker`
> 前置条件: Roids-Tweaker
> 导入: 见各章节

## 概念说明

- **Profession（职业）**：村民外观（长袍颜色）。用 `namespace:path` 格式表示，如 `minecraft:farmer`。用 `/ct villager professions` 查看
- **Career（生涯）**：决定村民名称和交易池。属于某个职业。用 string 表示。用 `/ct villager careers` 查看。添加时需添加语言文件：`entity.Villager.INSERT_career_NaMe`
- **Level（等级）**：村民升级解锁新交易。首次使用交易 100% 升级，之后 20%。无最高等级限制，从 1 级开始
- **Trade（交易）**：属于某个生涯和等级，由函数 `(merchant, recipeList, random)` 定义。使用 IIngredient 添加交易时物品随机选择

**注意：** Villager 类中除 `getCareer` 外的所有方法应在 `#loader preinit` 或 `#loader contenttweaker` 中调用。IVillagerCareer 方法应在物品可用时调用（`#loader crafttweaker`）。

## API 列表

### Villager

> `import mods.roidtweaker.minecraft.villager.Villager;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addProfession(String name, @Optional String texture, @Optional String zombieTexture)` | void | 注册新职业。名称应以 `crafttweaker:` 开头。纹理默认为 `roidtweaker:textures/entity/villager/[name].png` |
| `.addCareer(String profession, String name)` | void | 为职业添加生涯 |
| `.addCareer(String profession, String[] name)` | void | 为职业添加多个生涯（推荐替代多次调用） |
| `.removeProfession(String profession)` | void | 阻止指定职业注册 |
| `.clearCareers(String profession)` | void | 清除职业的所有生涯。注意：Minecraft 对无生涯职业处理不佳，应至少添加一个替代 |
| `.removeCareer(String career)` | void | 阻止指定生涯注册。需要配置：`mixin category.villager category.allowDisablingCareers=true` |
| `.getCareer(String profession, int careerIndex)` | IVillagerCareer | 按职业和索引获取生涯对象。索引相对于移除后的注册表状态 |
| `.getCareer(String profession, String career)` | IVillagerCareer | 按职业名和生涯名获取生涯对象 |

### IVillagerCareer

> `import mods.roidtweaker.minecraft.villager.IVillagerCareer;`

村民生涯对象，用于添加和移除交易。建议保存到变量以便多次使用。

#### 添加交易

所有 IIngredient 参数在生成交易时随机选择一个 ItemStack。支持配置：`mixin category.villager category.allowMetaWildcards=true`

##### 基础交易

```
addTrade(int level, IIngredient sell, IIngredient buy1, @Optional IIngredient buy2, @Optional function(IRandom, IIngredient) as IItemStack getOutput)
```

`getOutput` 的 `sell` 参数即 `addTrade` 的 `sell` 参数。

##### 附魔物品输出

随机选择 min-max 等级附魔输出（类似附魔台）。

```
addTradeForEnchantedItem(int level, IIngredient sell, IIngredient buy1, @Optional IIngredient buy2, @Optional int minLevel = 5, @Optional int maxLevel = 20)
```

##### 药水物品输出

从提供的数组或所有已注册药水中随机选择填充 Potion 标签。

```
addTradeForPotionItem(int level, IIngredient sell, IIngredient buy1, @Optional IIngredient buy2, @Optional string[] potionKeys)
```

##### 高级交易

完全自定义控制。

```
addTradeAdvanced(int level, function(IRandom) as IItemStack[])
```

函数应返回长度为 3 的 IItemStack[]：`[sell, buy1, buy2]`。返回长度不正确或输出为 null 则禁用交易。

#### 移除交易

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeTrade(@Optional int level, @Optional int index)` | void | 移除指定索引的交易。用 `/ct villager trades` 获取索引。省略参数则清除该等级/职业的所有交易 |
