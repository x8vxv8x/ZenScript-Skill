# FTB Quests CraftTweaker API 参考

> Mod ID: `ftbquests`
> 前置条件: ZenUtils
> 导入: `import mods.zenutils.ftbq.*;`

FTB Quests 事件集成，通过 ZenUtils 提供。用于监听任务完成、自定义奖励等事件。

---

## 事件注册

通过全局 `events` 对象访问。

| 方法 | 事件类型 | 说明 |
|------|------|------|
| `events.onTaskCompleted(handler)` | TaskCompletedEvent | 任务完成事件 |
| `events.onQuestCompleted(handler)` | QuestCompletedEvent | 任务线完成事件 |
| `events.onChapterCompleted(handler)` | ChapterCompletedEvent | 章节完成事件 |
| `events.onTaskStarted(handler)` | TaskStartedEvent | 任务开始事件 |
| `events.onCustomReward(handler)` | CustomRewardEvent | 自定义奖励事件 |
| `events.onCustomTask(handler)` | CustomTaskEvent | 自定义任务事件 |
| `events.clearFTBQEvents()` | - | 清除所有 FTB Quests 事件监听器 |

---

## API 列表

### QuestObjectBase（基础对象）

> `import mods.zenutils.ftbq.QuestObjectBase;`

所有 FTB Quests 对象的基类。

| 属性 | 返回 | 说明 |
|------|------|------|
| `id` | int | 唯一标识符 |
| `parentID` | int | 父对象 ID |
| `title` | String | 标题 |
| `data` | IData | NBT 数据 |
| `icon` | IItemStack | 图标物品 |
| `codeString` | String | 字符串表示 |
| `type` | String | 对象类型 |
| `tags` | String[] | 标签数组 |
| `hasTag(String)` | bool | 检查是否包含指定标签 |

支持 `==` 运算符。

### Chapter（章节）

> `import mods.zenutils.ftbq.Chapter;`

继承 `QuestObjectBase`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `quests` | List\<Quest\> | 章节中的所有任务线 |

### Quest（任务线）

> `import mods.zenutils.ftbq.Quest;`

继承 `QuestObjectBase`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `canRepeat` | bool | 是否可重复 |
| `chapter` | Chapter | 所属章节 |
| `x` | double | GUI 地图 X 位置 |
| `y` | double | GUI 地图 Y 位置 |
| `width` | double | 节点宽度 |
| `height` | double | 节点高度 |
| `tasks` | List\<Task\> | 所有任务 |
| `rewards` | List\<Reward\> | 所有奖励 |
| `dependencies` | List\<QuestObjectBase\> | 依赖的任务对象 |
| `subtitle` | String | 副标题 |
| `shape` | String | 节点形状 |
| `disableJEI` | bool | 是否禁用 JEI 集成 |

### Task（任务）

> `import mods.zenutils.ftbq.Task;`

继承 `QuestObjectBase`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `quest` | Quest | 所属任务线 |

### Reward（奖励）

> `import mods.zenutils.ftbq.Reward;`

继承 `QuestObjectBase`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `quest` | Quest | 所属任务线 |

---

## 事件类型

### ObjectCompletedEvent（完成事件基类）

> `import mods.zenutils.ftbq.ObjectCompletedEvent;`

| 属性 | 返回 | 说明 |
|------|------|------|
| `onlineMembers` | List\<IPlayer\> | 在线成员 |
| `notifyPlayers` | List\<IPlayer\> | 被通知的玩家 |

### QuestCompletedEvent

> `import mods.zenutils.ftbq.QuestCompletedEvent;`

继承 `ObjectCompletedEvent`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `quest` | Quest | 完成的任务线 |

### ChapterCompletedEvent

> `import mods.zenutils.ftbq.ChapterCompletedEvent;`

继承 `ObjectCompletedEvent`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `chapter` | Chapter | 完成的章节 |

### TaskCompletedEvent

> `import mods.zenutils.ftbq.TaskCompletedEvent;`

继承 `ObjectCompletedEvent`。

| 属性 | 返回 | 说明 |
|------|------|------|
| `task` | Task | 完成的任务 |

### TaskStartedEvent

> `import mods.zenutils.ftbq.TaskStartedEvent;`

| 属性 | 返回 | 说明 |
|------|------|------|
| `task` | Task | 开始的任务 |

### CustomRewardEvent

> `import mods.zenutils.ftbq.CustomRewardEvent;`

继承 `IEventCancelable`（可取消）。

| 属性 | 返回 | 说明 |
|------|------|------|
| `player` | IPlayer | 相关玩家 |
| `notify` | bool | 是否通知玩家 |
| `reward` | Reward | 奖励对象 |

### CustomTaskEvent

> `import mods.zenutils.ftbq.CustomTaskEvent;`

继承 `IEventCancelable`（可取消）。具体属性参见 wiki。

---

## 使用示例

### 任务完成通知

```zenscript
events.onQuestCompleted(function(event as QuestCompletedEvent) {
    var quest = event.quest;
    for player in event.notifyPlayers {
        player.sendMessage("完成任务: " ~ quest.title);
    }
});
```

### 自定义奖励

```zenscript
events.onCustomReward(function(event as CustomRewardEvent) {
    event.player.sendMessage("获得自定义奖励!");
});
```

### 自定义任务条件

```zenscript
events.onCustomTask(function(event as CustomTaskEvent) {
    // 自定义任务完成条件
});
```
