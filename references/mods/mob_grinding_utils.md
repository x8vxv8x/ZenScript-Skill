# Mob Grinding Utils CraftTweaker API 参考

> Mod ID: `mob_grinding_utils`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.mob_grinding_utils.*;`

## API 列表

### ChickenFeed（鸡饲料）

> `import moretweaker.mob_grinding_utils.ChickenFeed;`

可修改鸡饲料掉落的刷怪蛋。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setSpawnEgg(String mobId, IItemStack spawnegg)` | void | 设置生物 ID 对应的刷怪蛋 |
| `.resetSpawnEgg(String mobId)` | void | 重置生物 ID 对应的刷怪蛋为默认 |

## 使用示例

```zenscript
import moretweaker.mob_grinding_utils.ChickenFeed;

// 将末影人的刷怪蛋改为末影珍珠
ChickenFeed.setSpawnEgg("minecraft:enderman", <minecraft:ender_pearl>);
```
