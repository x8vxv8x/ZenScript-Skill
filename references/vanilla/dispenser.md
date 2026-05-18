# Dispenser API

## IDispenser

> `import crafttweaker.dispenser.IDispenser;`

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `block` | IBlock | 发射器方块 |
| `position` | IBlockPos | 位置 |
| `world` | IWorld | 世界 |
| `facing` | EnumFacing | 朝向 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.dispense(IItemStack)` | IItemStack | bool | 发射物品 |
| `.dispense(IItemStack, int)` | IItemStack, int | bool | 发射指定数量物品 |
| `.getStackInSlot(int)` | int | IItemStack | 获取指定槽的物品 |
| `.setStackInSlot(int, IItemStack)` | int, IItemStack | void | 设置指定槽的物品 |
| `.isEmpty()` | 无 | bool | 是否为空 |
| `.clear()` | 无 | void | 清空发射器 |

---

## IDispenserBehavior

> `import crafttweaker.dispenser.IDispenserBehavior;`

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.dispense(IBlockSource, IItemStack)` | IBlockSource, IItemStack | IItemStack | 执行发射行为 |

---

## 注册发射器行为

```zenscript
// 为物品注册发射器行为
dispenser.addItemBehavior(<minecraft:arrow>, function(blockSource, itemStack) {
    // 自定义发射逻辑
    return itemStack;  // 返回剩余物品
});

// 移除发射器行为
dispenser.removeItemBehavior(<minecraft:arrow>);
```

---

## 发射器配方

```zenscript
// 添加发射器配方
dispenser.addRecipe(<minecraft:arrow>, <minecraft:bow>);

// 移除发射器配方
dispenser.removeRecipe(<minecraft:arrow>);
```
