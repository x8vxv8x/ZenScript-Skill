# ProjectE CraftTweaker API 参考

> Mod ID: `projecte`
> 前置条件: 无
> 导入: `import mods.projecte.<ClassName>;`

## API 列表

### EntityRandomizer（实体随机化器）

> `import mods.projecte.EntityRandomizer;`

管理贤者之石实体随机化抛射物的实体转换列表。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addPeaceful(IEntityDefinition entityDefinition)` | void | 将实体添加到和平生物列表（可被转换为该实体） |
| `.addMob(IEntityDefinition entityDefinition)` | void | 将实体添加到敌对生物列表（可被转换为该实体） |
| `.removePeaceful(IEntityDefinition entityDefinition)` | void | 从和平生物列表中移除实体 |
| `.removeMob(IEntityDefinition entityDefinition)` | void | 从敌对生物列表中移除实体 |
| `.clearPeacefuls()` | void | 清除所有和平生物随机化条目（包括 CraftTweaker 添加的） |
| `.clearMobs()` | void | 清除所有敌对生物随机化条目（包括 CraftTweaker 添加的） |

实体必须是生物实体（living entity）。

### WorldTransmutation（世界转化）

> `import mods.projecte.WorldTransmutation;`

管理贤者之石的世界转化配方。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IItemStack input, @Optional IItemStack sneakOutput)` | void | 添加世界转化配方，潜行时使用 sneakOutput |
| `.add(IBlockState output, IBlockState input, @Optional IBlockState sneakOutput)` | void | 添加世界转化配方（方块状态版本） |
| `.remove(IItemStack output, IItemStack input, @Optional IItemStack sneakOutput)` | void | 移除匹配的世界转化配方 |
| `.remove(IBlockState output, IBlockState input, @Optional IBlockState sneakOutput)` | void | 移除匹配的世界转化配方（方块状态版本） |
| `.removeAll()` | void | 移除所有世界转化配方（包括用户添加的） |

如果 IItemStack 没有对应的方块，使用空气代替。

---

## Roids-Tweaker 扩展（需安装 Roids-Tweaker）

### EMCManager

> `import mods.ctintegration.projecte.EMCManager;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.mapEMC()` | void | 强制 ProjectE 映射所有 EMC 值。ProjectE 通常在服务器启动时映射，比 CraftTweaker 注册配方晚。在事件外获取 EMC 值前必须先调用。大型整合包中耗时较长，避免多次调用 |
| `.mapEMC(IItemStack item)` | void | 仅映射单个物品，比全量映射快 100-∞ 倍 |
| `.getEMC(IItemStack item)` | long | 获取物品 EMC 值。在事件外使用需先调用 `mapEMC` |
| `.getEMCSellValue(IItemStack item)` | long | 获取物品卖出价（取决于 ProjectE 配置）。同上需先调用 `mapEMC` |
| `.isEMCSet(IItemStack item)` | boolean | 检查物品是否已设置 EMC 值 |
| `.setEMC(IIngredient ingredient, long value)` | void | 设置 EMC 值。内部转换为 IItemStack 列表 |

### FuelManager

> `import mods.ctintegration.projecte.FuelManager;`

管理 ProjectE 燃料（EMC 充能物品和 EMC 收集器可升级物品）。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(IItemStack item)` | void | 添加燃料（必须是 ItemStack） |
| `.removeDefaults()` | void | 阻止 ProjectE 添加默认燃料（推荐替代 removeFuel） |
| `.removeFuel(IItemStack item)` | void | 移除燃料 |

### IItemStack 扩展

可在任何 IItemStack 上调用。

#### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getEMC()` | 无 | long | 获取 EMC 值 |
| `.setEMC(long amount)` | amount | void | 设置 EMC 值 |
| `.getEMCSellValue()` | 无 | long | 获取卖出价 |

注意：EMC getter 为小写开头。

### IPlayer 扩展

可在任何 IPlayer 上调用。

#### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getPersonalEMC()` | 无 | long | 获取玩家个人 EMC 值 |
| `.setPersonalEMC(long amount)` | amount | void | 设置玩家个人 EMC 值 |
