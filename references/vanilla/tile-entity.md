# Tile Entity CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.tileentity.ITileEntity;`

方块实体 API，用于获取和操作方块实体数据。

---

## API 列表

### ITileEntity（方块实体）

> `import crafttweaker.tileentity.ITileEntity;`

#### @ZenGetter

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

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getNBT()` | IData | 获取 NBT 数据 |
| `.setNBT(IData)` | void | 设置 NBT 数据 |
| `.update(IData)` | void | 更新 NBT 数据 |
| `.markDirty()` | void | 标记为已修改 |
| `.invalidate()` | void | 使无效 |
| `.remove()` | void | 移除 |

### IMobSpawnerBaseLogic（刷怪笼逻辑）

> `import crafttweaker.tileentity.IMobSpawnerBaseLogic;`

IMobSpawnerBaseLogic 包含刷怪笼如何以及在何处生成实体的各种信息。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `nbtData` | IData | 刷怪笼的 NBT 数据（可读写） |
| `entityDefinition` | IEntityDefinition | 要生成的实体定义（可读写） |
| `world` | IWorld | 刷怪笼所在世界（只读） |
| `blockPos` | IBlockPos | 刷怪笼方块的位置（只读） |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.updateSpawner()` | void | 更新刷怪笼，用于生成实体和倒计时 |
| `.setDelayToMin()` | void | 将刷怪笼延迟设置为最小值 |

---

## 使用示例

### 获取 Tile Entity

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

### Tile Entity 数据操作

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

---

## ZenUtils 扩展（需安装 ZenUtils + ContentTweaker）

> `import mods.zenutils.cotx.*;`

该部分是对 ContentTweaker 方块实体的扩展。

### TileEntity（方块实体定义）

> `import mods.zenutils.cotx.TileEntity;`

用于定义自定义方块实体的行为。通过 `VanillaFactory.createActualTileEntity(int)` 创建。

| 方法 | 返回 | 说明 |
|------|------|------|
| `VanillaFactory.createActualTileEntity(int)` | TileEntity | 创建自定义方块实体 |

### TileEntityInGame（方块实体实例）

> `import mods.zenutils.cotx.TileEntityInGame;`

表示游戏中的自定义方块实体实例。通过 `world.getCustomTileEntity(IBlockPos)` 获取。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `id` | int | 方块实体 ID（只读） |
| `data` | IData | 自定义数据（可读写） |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `updateCustomData(IData)` | void | 更新自定义数据 |

### ZenUtils 扩展示例

```zenscript
// 获取自定义方块实体
val teInGame = world.getCustomTileEntity(blockPos);
print(teInGame.id);
print(teInGame.data);

// 更新数据
teInGame.updateCustomData({key: "value"});
```
