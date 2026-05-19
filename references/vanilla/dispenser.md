# Dispenser CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.dispenser.IBlockSource;`、`import crafttweaker.dispenser.DispenserSound;`

发射器行为 API，用于自定义发射器行为和配方。

---

## API 列表

### IBlockSource（方块源）

> `import crafttweaker.dispenser.IBlockSource;`

IBlockSource 包含发射器激活时的一些信息，在自定义发射器行为中作为参数传入。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `x` | double | 发射器的 X 坐标 |
| `y` | double | 发射器的 Y 坐标 |
| `z` | double | 发射器的 Z 坐标 |
| `world` | IWorld | 发射器所在世界 |
| `blockState` | IBlockState | 发射器的方块状态 |
| `pos` | IBlockPos | 发射器的位置 |
| `facing` | IFacing | 发射器的朝向 |

### DispenserSound（发射器音效）

> `import crafttweaker.dispenser.DispenserSound;`

DispenserSound 是一个枚举，表示发射器的三种音效。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `DispenserSound.dispense()` | DispenserSound | 发射音效 |
| `DispenserSound.fail()` | DispenserSound | 失败音效 |
| `DispenserSound.launch()` | DispenserSound | 发射弹射物音效 |

### IItemDefinition 发射器行为方法

以下方法作用于 IItemDefinition（通过 `<modid:item>.definition` 获取）。

#### 添加发射器行为

```zenscript
itemDef.addDispenserBehavior(IDispenserBehavior behavior, @Optional IDispenserSoundFunction soundFunction);
```

- `IDispenserBehavior`：定义发射器如何发射物品的函数。参数为 `IBlockSource`（发射器信息）和 `IItemStack`（要发射的物品），必须返回 `IItemStack`（发射后剩余的物品）。
- `IDispenserSoundFunction`：可选，定义发射器播放什么音效。参数为 `IBlockSource`，必须返回 `DispenserSound`。

#### 移除发射器行为

```zenscript
itemDef.removeDispenserBehavior();
```

移除指定物品的发射器行为。

#### 添加弹射物发射行为

```zenscript
itemDef.addShootingProjectileDispenserBehavior(IEntityDefinition projectile, @Optional float inaccuracy, @Optional float velocity);
```

- `projectile`：弹射物实体定义
- `inaccuracy`：不精确度（默认 6.0）
- `velocity`：速度（默认 1.1）

---

## 使用示例

### 自定义发射器行为

```zenscript
import crafttweaker.dispenser.DispenserSound;

// 为粘土球添加发射器行为
<minecraft:clay_ball>.definition.addDispenserBehavior(function(source, item) {
    item.mutable().shrink(1);
    return item;
}, function(source) {
    return DispenserSound.launch();
});
```

### 移除发射器行为

```zenscript
// 发射器不再发射箭矢
<minecraft:arrow>.definition.removeDispenserBehavior();
```

### 发射弹射物

```zenscript
// 为苹果添加发射鸡蛋的行为
<minecraft:apple>.definition.addShootingProjectileDispenserBehavior(<entity:minecraft:egg>);

// 指定不精确度和速度
<minecraft:apple>.definition.addShootingProjectileDispenserBehavior(<entity:minecraft:egg>, 3.0, 1.5);
```
