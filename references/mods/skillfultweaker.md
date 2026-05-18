# SkillfulTweaker CraftTweaker API 参考

> Mod ID: `skillful`
> 前置条件: Skillful
> 导入: `import skillful.skill.*;`、`import skillful.event.*;`

SkillfulTweaker 是 Skillful 模组的 CraftTweaker 插件，支持注册新技能、查询技能统计、监听技能经验/等级变化事件。

---

## API 列表

### SkillType（技能类型）

> `import skillful.skill.SkillType;`

表示技能类型。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `maxLevel` | `int` | 最大等级 |
| `id` | `string` | 技能 ID，格式 `"domain:path"` |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getLevelRequiredXP(int level)` | `int` | 获取指定等级升级所需经验 |

---

### SkillTypeBuilder（技能类型构建器）

> `import skillful.skill.SkillTypeBuilder;`

用于构建 SkillType 的构建器。

#### 工厂方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `SkillTypeBuilder.create(string id)` | `SkillTypeBuilder` | 创建构建器实例。id 标准格式为 `"domain:path"`，若不含 `":"` 则自动格式化为 `"crt:*"`（如 `create("test")` 生成 `"crt:test"`） |

#### 构建方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setMaxLevel(int maxLevel)` | `SkillTypeBuilder` | 设置最大等级 |
| `.setLevelRequiredXp(function<int, int> required)` | `SkillTypeBuilder` | 设置升级所需经验，参数为匿名函数（接收等级，返回所需经验） |
| `.setColor(string color)` | `SkillTypeBuilder` | 设置 SkillInfo 中的显示颜色 |
| `.build()` | `SkillType` | 生成并返回 SkillType |

#### 可用颜色值

| 颜色 | 说明 |
|------|------|
| `"blue"` | 蓝色 |
| `"red"` | 红色 |
| `"green"` | 绿色 |
| `"yellow"` | 黄色 |
| `"purple"` | 紫色 |
| `"white"` | 白色 |
| `"pink"` | 粉色（默认） |

---

### Skill（技能实例）

> `import skillful.skill.Skill;`

表示玩家的技能实例，展示玩家对某技能的掌握程度。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `skillType` | `SkillType` | 对应的技能类型 |
| `level` | `int` | 当前等级 |
| `xp` | `int` | 当前经验 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.isAcquired()` | `bool` | 是否已学习（level > 0） |
| `.isClueless()` | `bool` | 等级和经验是否均为 0 |
| `.isCompleted()` | `bool` | 是否已达最大等级 |
| `.changeXp(IPlayer player, int change)` | `void` | 变更技能经验 |
| `.clear(IPlayer player)` | `void` | 清空经验和等级（设为 0） |
| `.cheat(IPlayer player)` | `void` | 将等级设为最大值，经验设为 0 |
| `.getSkillStat(string id)` | `Skill` | 根据技能类型 ID 获取玩家的技能实例 |
| `.clearSkillInfoCache()` | `void` | 清除玩家的 SkillInfo 缓存 |

---

### SkillManager（技能管理器）

> `import skillful.skill.SkillManager;`

Skillful 的技能管理类。

#### 工厂方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `SkillManager.getInstance()` | `SkillManager` | 获取单例实例 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getSkillTypes()` | `SkillType[]` | 获取所有已注册的技能类型 |
| `.getSkillType(string id)` | `SkillType` | 根据 ID 获取技能类型。若不存在，会注册一个最大等级和升级经验均为 32767 的虚拟技能类型并返回 |

---

### SkillRegisterEvent（技能注册事件）

> `import skillful.event.skill.registry.SkillRegisterEvent;`

用于注册技能类型的事件。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addSkill(SkillType skill)` | `void` | 注册一个技能类型 |

---

### SkillLevelEvent（技能等级变化事件）

> `import skillful.event.skill.lvl.SkillLevelEvent;`

技能等级变化时触发。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | `IPlayer` | 等级变化的玩家 |
| `skill` | `Skill` | 技能实例 |
| `level` | `int` | 当前等级 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.isUp()` | `bool` | 是否为升级 |
| `.isDown()` | `bool` | 是否为降级 |

---

### SkillXPPreEvent（技能经验变化前事件）

> `import skillful.event.skill.xp.SkillXPPreEvent;`

技能经验变化前触发。可取消，取消后经验不会变化。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `amount` | `int` | 经验变化量（可读写） |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | `IPlayer` | 经验变化的玩家 |
| `skill` | `Skill` | 技能实例 |

---

### SkillXPPostEvent（技能经验变化后事件）

> `import skillful.event.skill.xp.SkillXPPostEvent;`

技能经验变化后触发。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `player` | `IPlayer` | 经验变化的玩家 |
| `skill` | `Skill` | 技能实例 |
| `amount` | `int` | 经验变化量 |

---

### EventManager（事件管理器）

> `import skillful.event.EventManager;`

Skillful 的事件管理类。

#### 工厂方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `EventManager.getInstance()` | `EventManager` | 获取单例实例 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.onSkillRegister(function<SkillRegisterEvent> event)` | `void` | 添加技能注册事件监听器 |
| `.onSkillXPPre(function<SkillXPPreEvent> event)` | `void` | 添加技能经验变化前事件监听器 |
| `.onSkillXPPost(function<SkillXPPostEvent> event)` | `void` | 添加技能经验变化后事件监听器 |
| `.onSkillLevel(function<SkillLevelEvent> event)` | `void` | 添加技能等级变化事件监听器 |
| `.clear()` | `void` | 清除所有事件监听器 |

---

## 使用示例

### 注册技能并监听经验变化

```zenscript
import skillful.event.EventManager;
import skillful.event.skill.registry.SkillRegisterEvent;
import skillful.skill.Skill;
import skillful.skill.SkillType;
import skillful.skill.SkillTypeBuilder;

import crafttweaker.events.IEventManager;
import crafttweaker.event.BlockBreakEvent;
import crafttweaker.player.IPlayer;

val manager as EventManager = EventManager.getInstance();

// 创建技能类型：最大等级 100，升级经验 = 等级 * 200，白色显示
val testSkill as SkillType = SkillTypeBuilder.create("test:test")
    .setMaxLevel(100)
    .setColor("white")
    .setLevelRequiredXp(function(level as int) {
        return level * 200;
    })
    .build();

// 注册技能
manager.onSkillRegister(function(event as SkillRegisterEvent) {
    event.addSkill(testSkill);
});

// 破坏方块时增加 1 经验
events.onBlockBreak(function(event as BlockBreakEvent) {
    val player as IPlayer = event.player;
    player.getSkillStat("test:test").changeXp(player, 1);
});
```

### 监听技能升级并给予奖励

```zenscript
import skillful.event.EventManager;
import skillful.event.skill.lvl.SkillLevelEvent;

EventManager.getInstance().onSkillLevel(function(event as SkillLevelEvent) {
    if (event.isUp() && event.level == 10) {
        event.player.sendChat("你的技能达到了 10 级！");
        event.player.give(<minecraft:diamond>);
    }
});
```

### 取消特定经验变化

```zenscript
import skillful.event.EventManager;
import skillful.event.skill.xp.SkillXPPreEvent;

EventManager.getInstance().onSkillXPPre(function(event as SkillXPPreEvent) {
    // 阻止经验减少
    if (event.amount < 0) {
        event.amount = 0;
    }
});
```
