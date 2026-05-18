# Dispenser CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.dispenser.IDispenser;`、`import crafttweaker.dispenser.IDispenserBehavior;`

发射器行为 API，用于自定义发射器行为和配方。

---

## API 列表

### IDispenser（发射器）

> `import crafttweaker.dispenser.IDispenser;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `block` | IBlock | 发射器方块 |
| `position` | IBlockPos | 位置 |
| `world` | IWorld | 世界 |
| `facing` | EnumFacing | 朝向 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.dispense(IItemStack)` | bool | 发射物品 |
| `.dispense(IItemStack, int)` | bool | 发射指定数量物品 |
| `.getStackInSlot(int)` | IItemStack | 获取指定槽的物品 |
| `.setStackInSlot(int, IItemStack)` | void | 设置指定槽的物品 |
| `.isEmpty()` | bool | 是否为空 |
| `.clear()` | void | 清空发射器 |

### IDispenserBehavior（发射器行为）

> `import crafttweaker.dispenser.IDispenserBehavior;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.dispense(IBlockSource, IItemStack)` | IItemStack | 执行发射行为 |

---

## 使用示例

### 注册发射器行为

```zenscript
// 为物品注册发射器行为
dispenser.addItemBehavior(<minecraft:arrow>, function(blockSource, itemStack) {
    // 自定义发射逻辑
    return itemStack;  // 返回剩余物品
});

// 移除发射器行为
dispenser.removeItemBehavior(<minecraft:arrow>);
```

### 发射器配方

```zenscript
// 添加发射器配方
dispenser.addRecipe(<minecraft:arrow>, <minecraft:bow>);

// 移除发射器配方
dispenser.removeRecipe(<minecraft:arrow>);
```
