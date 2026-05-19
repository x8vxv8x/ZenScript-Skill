# Vanilla Death Chest CraftTweaker API 参考

> Mod ID: `vanilladeathchest`
> 前置条件: 无
> 导入: `import mods.vanilladeathchest.<ClassName>;`

## API 列表

### DeathChestSpawning (死亡箱子生成)

> `import mods.vanilladeathchest.DeathChestSpawning;`

#### 设置方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.setChatMessage(string stage, string message)` | void | 设置死亡箱子聊天消息，支持 %s 占位符（X、Y、Z坐标） |
| `.setContainerDisplayName(string stage, string name)` | void | 设置容器显示名称 |
| `.setRegistryNameRegex(string stage, string regex)` | void | 设置注册名正则表达式过滤 |
| `.setUseContainerInInventory(string stage, bool flag)` | void | 设置是否使用背包中的容器 |

### DeathChestDefense (死亡箱子防御)

> `import mods.vanilladeathchest.DeathChestDefense;`

#### 设置方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.setUnlocker(string stage, IItemStack unlocker)` | void | 设置解锁物品，物品数量可设置消耗/伤害量 |
| `.setDamageUnlockerInsteadOfConsume(string stage, bool flag)` | void | 设置是否伤害解锁物品而非消耗 |
| `.setUnlockFailedChatMessage(string stage, string message)` | void | 设置解锁失败聊天消息，支持 %s 占位符 |
| `.setDefenseEntity(string stage, IEntityDefinition defenseEntity)` | void | 设置防御实体 |
| `.setDefenseEntityNBT(string stage, IData nbt)` | void | 设置防御实体NBT数据 |
| `.setDefenseEntitySpawnCount(string stage, int count)` | void | 设置防御实体生成数量 |