# Tile Entity API

## ITileEntity

> `import crafttweaker.tileentity.ITileEntity;`

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `block` | IBlock | 方块 |
| `blockState` | IBlockState | 方块状态 |
| `position` | IBlockPos | 位置 |
| `world` | IWorld | 世界 |
| `data` | IData | NBT 数据 |
| `x` | int | X 坐标 |
| `y` | int | Y 坐标 |
| `z` | int | Z 坐标 |
| `hasWorld` | bool | 是否有世界 |
| `isEmpty` | bool | 是否为空 |
| `isInvalid` | bool | 是否无效 |
| `isRemoved` | bool | 是否已移除 |
| `commandString` | string | 命令字符串 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getNBT()` | 无 | IData | 获取 NBT 数据 |
| `.setNBT(IData)` | IData | void | 设置 NBT 数据 |
| `.update(IData)` | IData | void | 更新 NBT 数据 |
| `.markDirty()` | 无 | void | 标记为已修改 |
| `.invalidate()` | 无 | void | 使无效 |
| `.remove()` | 无 | void | 移除 |

---

## 获取 Tile Entity

```zenscript
// 从世界获取
val tileEntity = world.getTileEntity(blockPos);

// 从方块获取
val tileEntity = block.getTileEntity();

// 检查方块是否有 Tile Entity
if (block.hasTileEntity) {
    val tileEntity = world.getTileEntity(blockPos);
}
```

---

## Tile Entity 数据操作

```zenscript
// 获取 Tile Entity 数据
val data = tileEntity.data;

// 读取数据
if (!isNull(data.custom)) {
    val value = data.custom.asInt();
    print(value);
}

// 更新数据
tileEntity.update({custom: 42});
```
