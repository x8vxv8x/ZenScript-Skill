# RockyTweaks CraftTweaker API 参考

> Mod ID: `rockytweaks`
> 前置条件: 无
> 导入: `import mods.rockytweaks.<ClassName>;`

注：RockyTweaks 原名 RockyCore，提供铁砧和村民交易的 CraftTweaker 调整功能。

## API 列表

### Anvil（铁砧）

> `import mods.rockytweaks.Anvil;`

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient left, IIngredient right, IItemStack output, int expCost)` | void | 添加铁砧配方，expCost 为经验消耗 |
| `.addRecipe(IIngredient left, IIngredient right, IItemStack output, int expCost, IRecipeFunction function)` | void | 添加带自定义函数的铁砧配方 |

#### 移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(IIngredient[] inputs)` | void | 根据输入物品黑名单移除/禁用铁砧配方 |
| `.remove(IIngredient output)` | void | 根据输出物品移除/禁用铁砧配方 |
| `.removeAll()` | void | 移除所有铁砧配方 |

- 铁砧不使用常规配方系统，移除操作实质上是黑名单机制

### Merchant（村民交易）

> `import mods.rockytweaks.Merchant;`

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addTrade(String profession, String career, IItemStack input1, @Optional IItemStack input2, IItemStack output, int level)` | void | 添加村民交易，profession 为职业，career 为职业分支，level 为交易等级 |

- 移除功能目前不可用
- 使用 `/ct merchant professions` 查看有效职业
- 使用 `/ct merchant careers [profession]` 查看有效职业分支

## 使用示例

### 铁砧配方

```zenscript
import mods.rockytweaks.Anvil;

// 添加配方：书 + 8个石英 → 附魔锋利 I 的附魔书（消耗 5 经验）
Anvil.addRecipe(<minecraft:book>, <minecraft:quartz> * 8, <minecraft:enchanted_book>.withTag({StoredEnchantments: [{lvl: 1 as short, id: 16 as short}]}), 5);

// 带自定义函数的配方
Anvil.addRecipe(<minecraft:dirt>, <minecraft:sand>, <minecraft:gravel>, 1,
    function(output, input, craftinginfo) {
        if (!isNull(input.right.tag.display)
        && !isNull(input.right.tag.display.Name)
        && input.right.tag.display.Name == "Good Taco Seasoning") {
            return <minecraft:cooked_porkchop>;
        }
        return output;
    }
);

// 黑名单：禁用经验修补附魔书作为输入
Anvil.remove([<minecraft:enchanted_book>.withTag({StoredEnchantments: [{lvl: 1 as short, id: 70 as short}]})]);

// 黑名单：禁用锋利 V 钻石剑的组合
Anvil.remove([<minecraft:diamond_sword>, <minecraft:enchanted_book>.withTag({StoredEnchantments: [{lvl: 5 as short, id: 16 as short}]})]);

// 黑名单：禁用附魔书作为输出
Anvil.remove(<minecraft:enchanted_book>);
```

### 村民交易

```zenscript
import mods.rockytweaks.Merchant;

// 添加交易：傻子职业，1级交易，1个绿宝石 + 1个钻石 → 1个圆石
Merchant.addTrade("minecraft:nitwit", "nitwit", <minecraft:emerald>, <minecraft:diamond>, <minecraft:cobblestone>, 1);
```

## 注意事项

- 使用 `/ct merchant professions` 查看所有有效职业名称
- 使用 `/ct merchant careers [profession]` 查看指定职业的有效分支
- 村民交易移除功能目前不可用
