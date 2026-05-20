# IChunkPos CraftTweaker API 参考

> Mod ID: `roidtweaker`
> 前置条件: Roids-Tweaker
> 导入: `import mods.roidtweaker.minecraft.IChunkPos;`

区块坐标接口，封装 MC 的 ChunkPos。

## API 列表

### IChunkPos

> `import mods.roidtweaker.minecraft.IChunkPos;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getChunkPos(int x, int z)` | IChunkPos | 从区块坐标创建 |
| `.getChunkPos(IBlockPos pos)` | IChunkPos | 从方块坐标转换 |

#### 实例方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getBlockPos(int x, int y, int z)` | x, y, z | IBlockPos | 获取相对于此区块的方块坐标 |
