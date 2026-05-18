# Container API

## IContainer

> `import crafttweaker.container.IContainer;`

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 容器名称 |
| `displayName` | string | 显示名称 |
| `commandString` | string | 命令字符串 |
| `inventorySlots` | IInventorySlot[] | 物品槽列表 |
| `inventorySize` | int | 物品栏大小 |
| `maxStackSize` | int | 最大堆叠数 |
| `isEmpty` | bool | 是否为空 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getStackInSlot(int)` | int | IItemStack | 获取指定槽的物品 |
| `.setStackInSlot(int, IItemStack)` | int, IItemStack | void | 设置指定槽的物品 |
| `.insertItem(int, IItemStack, bool)` | int, IItemStack, bool | IItemStack | 插入物品 |
| `.extractItem(int, int, bool)` | int, int, bool | IItemStack | 提取物品 |
| `.getSlotLimit(int)` | int | int | 获取槽容量限制 |
| `.isItemValid(int, IItemStack)` | int, IItemStack | bool | 物品是否可放入槽 |
| `.clear()` | 无 | void | 清空容器 |
| `.markDirty()` | 无 | void | 标记为已修改 |

---

## IInventorySlot

> `import crafttweaker.container.IInventorySlot;`

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `stack` | IItemStack | 物品堆叠 |
| `slotIndex` | int | 槽索引 |
| `isEmpty` | bool | 是否为空 |
| `maxStackSize` | int | 最大堆叠数 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.putStack(IItemStack)` | IItemStack | void | 放入物品 |
| `.getStack()` | 无 | IItemStack | 获取物品 |
| `.decrStackSize(int)` | int | IItemStack | 减少物品数量 |
| `.isItemValid(IItemStack)` | IItemStack | bool | 物品是否可放入 |
| `.clear()` | 无 | void | 清空槽 |

---

## 玩家物品栏

```zenscript
// 获取玩家物品栏
val inventory = player.inventory;

// 获取主手物品
val mainHand = player.mainHandHeldItem;

// 获取副手物品
val offHand = player.offHandHeldItem;

// 给予物品
player.give(<minecraft:diamond>);

// 检查物品栏是否有物品
if (player.inventory.hasItem(<minecraft:diamond>)) {
    // 有钻石
}
```

---

## ZenUtils 扩展（需安装 ZenUtils）

> `import mods.zenutils.ItemHandler;`

### CrTItemHandler（物品处理器）

通过 `world.getItemHandler(IBlockPos)` 获取方块实体的物品容器。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `world.getItemHandler(IBlockPos, @Optional IFacing)` | IBlockPos, IFacing（可选） | ItemHandler | 获取方块实体的物品容器 |
| `sizeSlots` | 无 | int | 获取槽位数量 |
| `getStackInSlot(int)` | int | IItemStack | 获取指定槽位的物品 |
| `insertItem(int, IItemStack, bool)` | int, IItemStack, bool | IItemStack | 向指定槽位插入物品。第三个参数为 false 时仅模拟 |
| `extractItem(int, int, bool)` | int, int, bool | IItemStack | 从指定槽位提取物品。第三个参数为 false 时仅模拟 |
| `setStackInSlot(int, IItemStack)` | int, IItemStack | void | 直接设置指定槽位的物品 |
| `getSlotLimit(int)` | int | int | 获取指定槽位的最大堆叠数 |
