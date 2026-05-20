# Galacticraft CraftTweaker API 参考

> Mod ID: `galacticraft`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.galacticraft.*;`

## API 列表

### CircuitFabricator（电路制造机）

> `import moretweaker.galacticraft.CircuitFabricator;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IIngredient[] inputs)` | void | 添加电路制造配方 |
| `.remove(IItemStack output)` | void | 按输出移除配方 |

### Compressor（压缩机）

> `import moretweaker.galacticraft.Compressor;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addShaped(IItemStack output, IItemStack[][] inputs)` | void | 添加有序压缩配方 |
| `.addShapeless(IItemStack output, IIngredient[] inputs)` | void | 添加无序压缩配方 |
| `.remove(IItemStack output)` | void | 按输出移除配方 |
