# 玩家生命周期事件 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.event.*;`

玩家登录、登出、重生、维度切换、克隆等生命周期事件。

---

## API 列表

### PlayerLoggedInEvent（玩家登录事件）

> `import crafttweaker.event.PlayerLoggedInEvent;`

玩家登录时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 登录的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerLoggedOutEvent（玩家登出事件）

> `import crafttweaker.event.PlayerLoggedOutEvent;`

玩家登出时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | IPlayer | 登出的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerRespawnEvent（玩家重生事件）

> `import crafttweaker.event.PlayerRespawnEvent;`

玩家重生时触发。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `endConquered` | bool | 是否因跳过末地折跃门（Credits 传送门）而重生 |
| `player` | IPlayer | 重生的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerChangedDimensionEvent（玩家切换维度事件）

> `import crafttweaker.event.PlayerChangedDimensionEvent;`

玩家切换维度时触发（如进入/离开下界）。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `from` | int | 来源维度 ID |
| `fromWorld` | IWorld | 来源世界 |
| `to` | int | 目标维度 ID |
| `toWorld` | IWorld | 目标世界 |
| `player` | IPlayer | 切换维度的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。

### PlayerCloneEvent（玩家克隆事件）

> `import crafttweaker.event.PlayerCloneEvent;`

玩家被克隆时触发。通常在重生或从末地返回时发生。

实现接口：IPlayerEvent

| 属性 | 类型 | 说明 |
|------|------|------|
| `originalPlayer` | IPlayer | 原始玩家对象 |
| `wasDeath` | bool | 是否因死亡而克隆（维度传送时为 false） |
| `player` | IPlayer | 克隆后的玩家 |

继承自 IPlayerEvent 的 `entityLivingBase`。
