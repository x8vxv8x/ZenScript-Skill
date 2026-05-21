# 玩家统计 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: ZenUtils（部分需要 Roids-Tweaker）
> 导入: `import mods.zenutils.PlayerStat;`、`import mods.zenutils.IStatFormatter;`

PlayerStat、IStatFormatter 玩家统计 API。

---

## API 列表

### PlayerStat（玩家统计）

> `import mods.zenutils.PlayerStat;`

#### 获取 PlayerStat

| 方法 | 返回 | 说明 |
|------|------|------|
| `PlayerStat.getBasicStat(String)` | PlayerStat | 获取基础统计（用 `/ct stats` 查看所有） |
| `PlayerStat.getBlockStats(IBlockDefinition)` | PlayerStat | 方块相关统计 |
| `PlayerStat.getCraftStats(IItemDefinition)` | PlayerStat | 合成统计 |
| `PlayerStat.getObjectUseStats(IItemDefinition)` | PlayerStat | 物品使用统计 |
| `PlayerStat.getObjectBreakStats(IItemDefinition)` | PlayerStat | 物品破坏统计 |
| `PlayerStat.getObjectsPickedUpStats(IItemDefinition)` | PlayerStat | 物品拾取统计 |
| `PlayerStat.getDroppedObjectStats(IItemDefinition)` | PlayerStat | 物品掉落统计 |
| `PlayerStat.getKillEntityStats(IEntityDefinition)` | PlayerStat | 击杀实体统计 |
| `PlayerStat.getKilledByEntityStats(IEntityDefinition)` | PlayerStat | 被实体击杀统计 |

#### 创建 PlayerStat

| 方法 | 返回 | 说明 |
|------|------|------|
| `PlayerStat.create(String id, ITextComponent name, @Optional IStatFormatter)` | PlayerStat | 创建自定义统计（需在游戏初始化阶段调用） |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | ITextComponent | 统计名称 |

#### 玩家统计操作

| 方法 | 返回 | 说明 |
|------|------|------|
| `player.readStat(PlayerStat)` | int | 读取统计值 |
| `player.addStat(PlayerStat, @Optional int)` | void | 增加统计计数（默认 1） |
| `player.takeStat(PlayerStat)` | void | 重置统计值为 0 |

### IStatFormatter（统计格式化器）

> `import mods.zenutils.IStatFormatter;`

函数式接口：接收 `int`，返回 `string`。

| 预置格式化器 | 说明 |
|------|------|
| `IStatFormatter.simple()` | 数字分组显示（默认） |
| `IStatFormatter.time()` | 时间格式显示 |
| `IStatFormatter.distance()` | 距离单位显示 |
| `IStatFormatter.divideByTen()` | 除以十后显示 |

| 工具方法 | 返回 | 说明 |
|------|------|------|
| `IStatFormatter.numberFormat(int)` | string | 格式化整数（分组分隔符） |
| `IStatFormatter.decimalFormat(double)` | string | 格式化小数（保留2位） |

---

## Roids-Tweaker 扩展

### IPlayer 扩展

可在任何 IPlayer 上调用。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.addExperience(int amount)` | amount | void | 添加经验点（非等级） |
| `.removeExperience(int amount)` | amount | void | 移除经验点 |
| `.getTotalXP()` | 无 | int | 获取总经验量 |
| `.playSound(String sound, float volume, float pitch)` | sound, volume, pitch | void | 播放声音。客户端和服务端玩家行为不同，检查 `world.remote` 判断端 |
| `.sendPlaySoundPacket(String sound, String category, Position3f pos, float volume, float pitch)` | sound, category, pos, volume, pitch | void | 使玩家客户端播放声音 |
| `.isPlayerMP()` | 无 | bool | 是否为 EntityPlayerMP 实例（服务端玩家） |
| `.isFake()` | 无 | bool | 是否为 FakePlayer 实例 |
| `.getAdvancementProgress(IAdvancement advancement)` | advancement | IAdvancementProgress | 获取进度完成状态。玩家必须是 EntityPlayerMP 实例，否则返回 null |

### IRandom 扩展

可在任何 IRandom 上调用。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.nextGaussian()` | double | 返回服从标准正态分布的随机 double |
