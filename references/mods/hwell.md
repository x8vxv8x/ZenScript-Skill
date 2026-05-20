# Hearth Well CraftTweaker API 参考

> Mod ID: `hwell`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.hwell.*;`

注意：Hearth Well 有原生 CraftTweaker 支持，但缺少某些核心配方功能。**如果使用 MoreTweaker 修改核心配方，不要同时使用原生支持，否则可能出错。**

## API 列表

### MoreCoring（核心配方扩展）

> `import moretweaker.hwell.MoreCoring;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addCoring(String coreId, String shardId, IItemStack[] output, IItemStack[] input)` | void | 添加核心配方 |
| `.removeCoring(@Nullable String coreId, @Nullable String shardId)` | void | 移除核心配方。若 `coreId` 或 `shardId` 为 null，则匹配所有核心/碎片 |

#### 核心 ID

| 字符串 | 说明 |
|------|------|
| `core_stone` | 岩石核心 |
| `core_anima` | 灵魂核心 |
| `core_heat` | 温暖核心 |
| `core_green` | 翠绿核心 |
| `core_sentient` | 感知核心 |

#### 碎片 ID

| 字符串 | 说明 |
|------|------|
| `shard_c` | 火土碎片 |
| `shard_fe` | 圣地碎片 |
| `shard_au` | 曙光碎片 |
| `shard_o` | 生命之根碎片 |
| `shard_h` | 活世界碎片 |
| `shard_ca` | 先天之力碎片 |
| `shard_p` | 晨星碎片 |
| `shard_n` | 纯净给予者碎片 |

## 使用示例

```zenscript
import moretweaker.hwell.MoreCoring;

// 移除温暖核心的所有配方
MoreCoring.removeCoring("core_heat", null);
```
