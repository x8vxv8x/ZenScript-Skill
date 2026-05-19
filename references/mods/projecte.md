# ProjectE CraftTweaker API 参考

> Mod ID: `projecte`
> 前置条件: 无
> 导入: `import mods.projecte.<ClassName>;`

## API 列表

### EntityRandomizer（实体随机化器）

> `import mods.projecte.EntityRandomizer;`

管理贤者之石实体随机化抛射物的实体转换列表。

#### 添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addPeaceful(IEntityDefinition entityDefinition)` | void | 将实体添加到和平生物列表（可被转换为该实体） |
| `.addMob(IEntityDefinition entityDefinition)` | void | 将实体添加到敌对生物列表（可被转换为该实体） |

#### 移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removePeaceful(IEntityDefinition entityDefinition)` | void | 从和平生物列表中移除实体 |
| `.removeMob(IEntityDefinition entityDefinition)` | void | 从敌对生物列表中移除实体 |
| `.clearPeacefuls()` | void | 清除所有和平生物随机化条目（包括 CraftTweaker 添加的） |
| `.clearMobs()` | void | 清除所有敌对生物随机化条目（包括 CraftTweaker 添加的） |

- 实体必须是生物实体（living entity）

### WorldTransmutation（世界转化）

> `import mods.projecte.WorldTransmutation;`

管理贤者之石的世界转化配方。

#### 添加方法（IItemStack 版本）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IItemStack input, @Optional IItemStack sneakOutput)` | void | 添加世界转化配方，潜行时使用 sneakOutput |

- 如果 IItemStack 没有对应的方块，使用空气代替

#### 添加方法（IBlockState 版本）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IBlockState output, IBlockState input, @Optional IBlockState sneakOutput)` | void | 添加世界转化配方（方块状态版本） |

#### 移除方法（IItemStack 版本）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(IItemStack output, IItemStack input, @Optional IItemStack sneakOutput)` | void | 移除匹配的世界转化配方 |

#### 移除方法（IBlockState 版本）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(IBlockState output, IBlockState input, @Optional IBlockState sneakOutput)` | void | 移除匹配的世界转化配方（方块状态版本） |

#### 全部移除

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeAll()` | void | 移除所有世界转化配方（包括用户添加的） |