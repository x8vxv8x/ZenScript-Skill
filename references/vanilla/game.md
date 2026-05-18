# Game API

## 全局字段

无需 import，直接使用的全局对象。

| 字段 | 类型 | 说明 |
|------|------|------|
| `recipes` | IRecipeManager | 工作台配方管理 |
| `furnace` | IFurnaceManager | 熔炉配方管理 |
| `brewing` | IBrewingManager | 酿造台管理 |
| `game` | IGame | 游戏相关函数 |
| `server` | IServer | 服务器相关 |
| `client` | IClient | 客户端相关 |
| `events` | IEventManager | 事件管理 |
| `format` | IFormatter | 格式化处理 |
| `itemUtils` | IItemUtils | 物品工具 |
| `loadedMods` | ILoadedMods | 已加载 mod 列表 |
| `logger` | ILogger | 日志工具 |
| `oreDict` | IOreDict | 矿物词典管理 |
| `vanilla` | IVanilla | 原版函数（如 seeds） |

---

## IGame

> `import crafttweaker.game.IGame;`

通过 `game` 全局关键字访问。

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `biomes` | List\<IBiome\> | 所有注册的生物群系 |
| `blocks` | List\<IBlockDefinition\> | 所有注册的方块定义 |
| `enchantments` | List\<IEnchantmentDefinition\> | 所有注册的附魔定义 |
| `entities` | List\<IEntityDefinition\> | 所有注册的实体定义 |
| `items` | List\<IItemDefinition\> | 所有注册的物品定义 |
| `liquids` | List\<ILiquidDefinition\> | 所有注册的流体定义 |
| `potions` | List\<IPotion\> | 所有注册的药水效果 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.setLocalization(string, string)` | string, string | void | 设置本地化（key, value） |
| `.setLocalization(string, string, string)` | string, string, string | void | 设置本地化（lang, key, value） |
| `.localize(string)` | string | string | 获取本地化字符串 |
| `.localize(string, string)` | string, string | string | 获取指定语言的本地化字符串 |
| `.getEntity(string)` | string | IEntityDefinition | 获取实体定义（等同于 `<entity:...>`） |
| `.getPotion(string)` | string | IPotion | 获取药水效果 |

---

## IClient

> `import crafttweaker.api.IClient;`

通过 `client` 全局关键字访问。仅在客户端可用，服务端无效。

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 当前客户端玩家 |
| `language` | string | 客户端语言 |

---

## IServer

> `import crafttweaker.server.IServer;`

通过 `server` 全局关键字访问。IServer 继承 ICommandSender。

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.isOp(IPlayer)` | IPlayer | bool | 检查玩家是否有 OP 权限 |
| `commandManager` | 无 | ICommandManager | 获取命令管理器 |

---

## ITeam

> `import crafttweaker.game.ITeam;`

ITeam 代表一个队伍。

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 队伍名称 |
| `allowFriendlyFire` | bool | 是否允许友军伤害 |
| `colorPrefix` | string | 颜色前缀 |
| `membershipCollection` | List\<string\> | 成员列表 |
| `deathMessageVisibility` | string | 死亡消息可见性 |
| `collisionRule` | string | 碰撞规则 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.formatString(string)` | string | string | 格式化队伍字符串 |

---

## ILoadedMods / IMod

> `import crafttweaker.mods.ILoadedMods;`
> `import crafttweaker.mods.IMod;`

通过 `loadedMods` 全局关键字访问。

### ILoadedMods 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `loadedMods in "modid"` | string | bool | 检查 mod 是否已加载 |
| `loadedMods.contains(string)` | string | bool | 检查 mod 是否已加载 |
| `loadedMods["modid"]` | string | IMod | 获取指定 mod |
| 遍历 `loadedMods` | 无 | IMod | 遍历所有已加载 mod |

### IMod 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `id` | string | mod ID |
| `name` | string | mod 名称 |
| `version` | string | mod 版本 |
| `description` | string | mod 描述 |
| `items` | IItemStack[] | mod 添加的所有物品 |

---

## 遍历所有模组物品

```zenscript
for mod in loadedMods {
    for item in mod.items {
        // 处理每个物品
    }
}
```
