# Enchantments CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.enchantments.IEnchantment;`、`import crafttweaker.enchantments.IEnchantmentDefinition;`

附魔系统 API，用于操作附魔和物品附魔。

---

## API 列表

### IEnchantment（附魔实例）

> `import crafttweaker.enchantments.IEnchantment;`

IEnchantment 是附魔定义加上附魔等级的组合。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `definition` | IEnchantmentDefinition | 附魔定义 |
| `level` | int | 附魔等级 |
| `displayName` | string | 显示名称（可读写） |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.makeStack(int)` | IEnchantment | 创建指定等级的附魔 |
| `.makeTag()` | IData | 获取附魔的 NBT 标签（也可用 `ench as IData`） |

### IEnchantmentDefinition（附魔定义）

> `import crafttweaker.enchantments.IEnchantmentDefinition;`

IEnchantmentDefinition 是附魔本身的定义（不含等级），通过 `<enchantment:...>` 获取。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `id` | int | 附魔 ID |
| `name` | string | 附魔名称（可读写） |
| `maxLevel` | int | 最大等级 |
| `minLevel` | int | 最小等级 |
| `isAllowedOnBooks` | bool | 是否允许出现在附魔台 |
| `isTreasureEnchantment` | bool | 是否宝藏附魔 |
| `isCurse` | bool | 是否诅咒 |
| `registryName` | string | 注册名 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.makeEnchantment(int)` | IEnchantment | 创建指定等级的附魔（也可用 `ench * level`） |
| `.canApply(IItemStack)` | bool | 是否可应用到物品 |
| `.canApplyAtEnchantmentTable(IItemStack)` | bool | 是否可通过附魔台应用到物品 |
| `.getMinEnchantability(int)` | int | 获取指定等级的最低附魔需求 |
| `.getMaxEnchantability(int)` | int | 获取指定等级的最高附魔需求 |
| `.getTranslatedName(int)` | string | 获取翻译后的名称（如 "smite IV"） |
| `enchA == enchB` | bool | 比较两个附魔定义是否相同（基于 ID） |

---

## 使用示例

### 物品附魔方法

```zenscript
// 检查是否可在工作台附魔
<minecraft:diamond_pickaxe>.canApplyAtCraftingTable(<enchantment:fortune>);

// 添加附魔
<minecraft:diamond_pickaxe>.addEnchantment(<enchantment:fortune> * 3);  // 时运 III

// 获取物品附魔列表
<minecraft:diamond_pickaxe>.enchantments  // List<IEnchantment>

// 检查物品是否已附魔
<minecraft:diamond_pickaxe>.isEnchanted  // bool

// 检查物品是否可附魔
<minecraft:diamond_pickaxe>.isEnchantable  // bool
```

### 遍历所有附魔

```zenscript
for enchantment in game.enchantments {
    print(enchantment.name ~ ": " ~ enchantment.displayName);
}
```
