# 玩家交互模拟 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: ZenUtils
> 导入: `import mods.zenutils.*;`

玩家交互模拟（左键/右键），仅应在服务端调用。

@since 1.14.3

---

## API 列表

### IPlayer 扩展

对 `crafttweaker.player.IPlayer` 的扩展，所有玩家对象自动可用。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.replaceItemInInventory(int slot, IItemStack stack)` | bool | 替换玩家背包指定槽位的物品 |
| `.readStat(PlayerStat stat)` | int | 读取统计值 |
| `.addStat(PlayerStat stat, @Optional int amount)` | void | 增加统计计数（默认 1） |
| `.takeStat(PlayerStat stat)` | void | 将统计值重置为 0 |

### simulateRightClickItem

模拟玩家右键使用物品（不指向方块或实体）。

| 参数 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| item | IItemStack | 使用的物品 | |
| hand | IEntityEquipmentSlot | 使用的手（仅 mainHand/offHand） | mainHand |

返回 `String`：`SUCCESS`、`PASS` 或 `FAIL`

### simulateRightClickBlock

模拟玩家右键点击方块。

| 参数 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| item | IItemStack | 使用的物品 | |
| hand | IEntityEquipmentSlot | 使用的手 | mainHand |
| pos | IBlockPos | 方块位置 | 根据玩家视线确定 |
| side | IFacing | 点击的方块面 | 根据玩家视线确定 |
| hitX | float | 点击相对 X 坐标（0~1） | 根据玩家视线确定 |
| hitY | float | 点击相对 Y 坐标（0~1） | 根据玩家视线确定 |
| hitZ | float | 点击相对 Z 坐标（0~1） | 根据玩家视线确定 |

返回 `String`：`SUCCESS`、`PASS` 或 `FAIL`

### simulateRightClickEntity

模拟玩家右键点击实体。

| 参数 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| entity | IEntity | 目标实体 | |
| item | IItemStack | 使用的物品 | 手中物品 |
| hand | IEntityEquipmentSlot | 使用的手 | mainHand |

返回 `String`：`SUCCESS`、`PASS` 或 `FAIL`

### simulateLeftClickBlock

模拟玩家左键点击方块。

| 参数 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| item | IItemStack | 使用的物品 | 主手物品 |
| pos | IBlockPos | 方块位置 | 根据玩家视线确定 |
| side | IFacing | 点击的方块面 | 根据玩家视线确定 |

无返回值。

### simulateUseItemFinish

模拟玩家完成使用物品（如吃完食物）。返回结果物品（如牛奶桶→空桶）。

| 参数 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| item | IItemStack | 使用的物品 | |
| hand | IEntityEquipmentSlot | 使用的手 | 当前激活手 |
