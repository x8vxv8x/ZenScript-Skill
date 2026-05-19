# JAOPCA CraftTweaker API 参考

> Mod ID: `jaopca`
> 前置条件: 无
> 导入: `import mods.jaopca.JAOPCA;`

## API 列表

### JAOPCA

> `import mods.jaopca.JAOPCA;`

#### 检查方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.containsEntry(String entryName)` | bool | 检查指定名称的 entry 是否存在 |
| `.getOre(String oreName)` | OreEntry | 获取指定名称的 OreEntry，不存在则返回 null。注意大小写敏感，大部分材料首字母大写 |
| `.getOresForEntry(String entryName)` | OreEntry[] | 获取拥有指定 entry 的所有 OreEntry 列表 |
| `.getOresForType(String oreType)` | OreEntry[] | 获取指定 oreType 的所有 OreEntry 列表 |
| `.getAllOres()` | OreEntry[] | 获取所有已注册的 OreEntry 列表 |

### OreEntry

OreEntry 代表一种材料（如 Gold、Diamond、Coal 等），可通过前缀获取对应的矿辞、物品和流体。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `energyModifier` | double | 能量修正系数 |
| `rarity` | double | 稀有度 |
| `oreType` | string | 矿石类型（如 "INGOT"、"GEM"、"DUST"） |
| `oreName` | string | 矿石名称（如 "Gold"） |
| `oreNameSynonyms` | string[] | 矿石名称同义词列表（如 "Aluminum" 和 "Aluminium"） |
| `hasExtra` | bool | 是否有第一副产物 |
| `extra` | OreEntry | 第一副产物的 OreEntry，不存在则返回 null |
| `extraName` | string | 第一副产物名称，不存在则返回 null |
| `hasSecondExtra` | bool | 是否有第二副产物 |
| `secondExtra` | OreEntry | 第二副产物的 OreEntry，不存在则返回 null |
| `secondExtraName` | string | 第二副产物名称，不存在则返回 null |
| `hasThirdExtra` | bool | 是否有第三副产物 |
| `thirdExtra` | OreEntry | 第三副产物的 OreEntry，不存在则返回 null |
| `thirdExtraName` | string | 第三副产物名称，不存在则返回 null |

#### 获取方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getOreDictEntry(String prefix)` | IOreDictEntry | 获取指定前缀的矿辞条目，如 `getOreDictEntry("dust")` 返回 `<ore:dustGold>` |
| `.getItemStack(String prefix)` | IItemStack | 获取指定前缀的物品，不存在返回 null |
| `.getItemStack(String prefix, String fallback)` | IItemStack | 获取指定前缀的物品，不存在时尝试 fallback 前缀 |
| `.getLiquidStack(String prefix)` | ILiquidStack | 获取指定前缀的流体，不存在返回 null |
| `.getLiquidStack(String prefix, String fallback)` | ILiquidStack | 获取指定前缀的流体，不存在时尝试 fallback 前缀 |

#### 副产物方法（第一副产物）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getOreDictEntryExtra(String prefix)` | IOreDictEntry | 获取第一副产物指定前缀的矿辞 |
| `.getItemStackExtra(String prefix)` | IItemStack | 获取第一副产物指定前缀的物品 |
| `.getItemStackExtra(String prefix, String fallback)` | IItemStack | 获取第一副产物指定前缀的物品，带 fallback |
| `.getLiquidStackExtra(String prefix)` | ILiquidStack | 获取第一副产物指定前缀的流体 |
| `.getLiquidStackExtra(String prefix, String fallback)` | ILiquidStack | 获取第一副产物指定前缀的流体，带 fallback |

#### 副产物方法（第二副产物）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getOreDictEntrySecondExtra(String prefix)` | IOreDictEntry | 获取第二副产物指定前缀的矿辞 |
| `.getItemStackSecondExtra(String prefix)` | IItemStack | 获取第二副产物指定前缀的物品 |
| `.getItemStackSecondExtra(String prefix, String fallback)` | IItemStack | 获取第二副产物指定前缀的物品，带 fallback |
| `.getLiquidStackSecondExtra(String prefix)` | ILiquidStack | 获取第二副产物指定前缀的流体 |
| `.getLiquidStackSecondExtra(String prefix, String fallback)` | ILiquidStack | 获取第二副产物指定前缀的流体，带 fallback |

#### 副产物方法（第三副产物）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getOreDictEntryThirdExtra(String prefix)` | IOreDictEntry | 获取第三副产物指定前缀的矿辞 |
| `.getItemStackThirdExtra(String prefix)` | IItemStack | 获取第三副产物指定前缀的物品 |
| `.getItemStackThirdExtra(String prefix, String fallback)` | IItemStack | 获取第三副产物指定前缀的物品，带 fallback |
| `.getLiquidStackThirdExtra(String prefix)` | ILiquidStack | 获取第三副产物指定前缀的流体 |
| `.getLiquidStackThirdExtra(String prefix, String fallback)` | ILiquidStack | 获取第三副产物指定前缀的流体，带 fallback |

## 使用示例

### 获取材料信息

```zenscript
import mods.jaopca.JAOPCA;

val goldEntry = mods.jaopca.JAOPCA.getOre("Gold");
val dustGold = goldEntry.getOreDictEntry("dust"); // <ore:dustGold>
val itemGold = goldEntry.getItemStack("coin");    // <jaopca:item_coingold>
val liquidGold = goldEntry.getLiquidStack("molten"); // <liquid:gold>
```

### 遍历所有材料

```zenscript
import mods.jaopca.JAOPCA;

val allOres = mods.jaopca.JAOPCA.getAllOres();
for ore in allOres {
    val nugget = ore.getItemStack("nugget");
    if (nugget != null) {
        // 处理该材料的粒
    }
}
```
