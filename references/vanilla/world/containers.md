# 世界容器操作 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: ZenUtils
> 导入: `import mods.zenutils.ItemHandler;`、`import mods.zenutils.LiquidHandler;`、`import mods.zenutils.ILiquidTankProperties;`

CrTItemHandler、CrTLiquidHandler、ILiquidTankProperties 容器操作 API。

---

## API 列表

### CrTItemHandler（物品容器）

> `import mods.zenutils.ItemHandler;`

@since 1.6.3

物品容器操作，类似箱子或玩家背包。

#### 获取实例

| 方法 | 返回 | 说明 |
|------|------|------|
| `world.getItemHandler(IBlockPos, @Optional IFacing)` | ItemHandler | 从方块实体获取物品容器 |
| `player.getPlayerInventoryItemHandler()` | ItemHandler | 获取玩家背包容器 |
| `player.getPlayerBaubleItemHandler()` | ItemHandler | 获取玩家饰品栏容器（需安装 Baubles） |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `size` | int | 可用槽位数 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getStackInSlot(int)` | IItemStack | 获取指定槽位物品（可为 null） |
| `.setStackInSlot(int, IItemStack)` | bool | 设置指定槽位物品 |
| `.insertItem(int, IItemStack, bool simulate)` | IItemStack | 插入物品，返回剩余部分（全部接受返回 null） |
| `.extractItem(int, int amount, bool simulate)` | IItemStack | 提取物品 |
| `.getSlotLimit(int)` | int | 获取指定槽位最大堆叠数 |
| `.isItemValid(int, IItemStack)` | bool | 检查物品是否可插入该槽位 |

支持 for 循环遍历。

### CrTLiquidHandler（流体容器）

> `import mods.zenutils.LiquidHandler;`

@since 1.9.8

流体容器操作。

#### 获取实例

| 方法 | 返回 | 说明 |
|------|------|------|
| `world.getLiquidHandler(IBlockPos, @Optional IFacing)` | LiquidHandler | 从方块实体获取流体容器 |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `tankProperties` | List\<ILiquidTankProperties\> | 流体槽属性列表（只读） |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.drain(int maxDrain, bool doDrain)` | ILiquidStack | 排出流体（不区分流体类型） |
| `.drain(ILiquidStack resource, bool doDrain)` | ILiquidStack | 排出指定流体 |
| `.fill(ILiquidStack resource, bool doFill)` | int | 填充流体，返回实际填充量 |

### ILiquidTankProperties（流体槽属性）

> `import mods.zenutils.ILiquidTankProperties;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `contents` | ILiquidStack | 流体内容副本（可为 null） |
| `capacity` | int | 最大容量（mB） |
| `canFill` | bool | 是否可填充 |
| `canDrain` | bool | 是否可排出 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.canFillFluidType(ILiquidStack)` | bool | 是否可填充指定类型流体 |
| `.canDrainFluidType(ILiquidStack)` | bool | 是否可排出指定类型流体 |
