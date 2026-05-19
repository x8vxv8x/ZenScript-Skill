# Enchanting Plus CraftTweaker API 参考

> Mod ID: `eplus`
> 前置条件: 无
> 导入: `import mods.eplus.*;`

Enchanting Plus 允许玩家更好地控制附魔体验。CraftTweaker 可以用于对此模组应用某些限制。

---

## API 列表

### Eplus（附魔增强）

> `import mods.eplus.Eplus;`

#### 物品黑名单方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.blacklistItem(item as IItemStack)` | void | 禁止物品进入高级附魔台 |

#### 附魔黑名单方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.blacklistEnchantment(enchantment as IEnchantmentDefinition)` | void | 禁止特定附魔 |

---

## 注意事项

- 黑名单会阻止物品进入高级附魔台
- 黑名单会阻止特定附魔在高级附魔台中应用