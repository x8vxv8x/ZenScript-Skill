# Advancements CraftTweaker API 参考

> Mod ID: `ctintegration`
> 前置条件: CraftTweaker Integration
> 导入: 见各章节

## API 列表

### AdvancementHelper

> `import mods.ctintegration.advancement.AdvancementHelper;`

用于通过 ID 获取进度。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getAdvancementById(IServer server, String id)` | IAdvancement | 获取指定 ID 的进度，可能返回 null |
| `.getAdvancements(IServer server)` | List\<IAdvancement\> | 获取所有进度列表 |

### IAdvancement

> `import mods.ctintegration.advancement.IAdvancement;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `id` | string | 进度的资源位置 |
| `displayText` | ITextComponent | 显示文本 |
| `title` | ITextComponent | 标题 |
| `description` | ITextComponent | 描述 |
| `requirements` | string[][] | 需求条件 |
| `requirementCount` | int | 需求数量 |
| `children` | List\<IAdvancement\> | 子进度列表 |
| `criterion` | List\<String\> | 标准列表 |
| `parent` | IAdvancement | 父进度 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.applyRewards(IPlayer player)` | void | 给予玩家进度奖励 |

### IAdvancementProgress

> `import mods.ctintegration.advancement.IAdvancementProgress;`

进度完成状态。通过 IPlayer 扩展获取。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.isDone()` | 无 | bool | 是否完成 |
| `.hasProgress()` | 无 | bool | 是否有进度 |
| `.grantCriterion(String criterion)` | criterion | bool | 授予标准 |
| `.revokeCriterion(String criterion)` | criterion | bool | 撤销标准 |
| `.getCompletedCriteria()` | 无 | List\<String\> | 获取已完成标准 |
| `.getRemainingCriteria()` | 无 | List\<String\> | 获取未完成标准 |
| `.getPercent()` | 无 | float | 获取完成百分比 |
| `.getProgressText()` | 无 | string | 获取进度文本 |
| `.isCriterionObtained(String criterion)` | criterion | bool | 检查标准是否已获得 |
| `.getCriterionObtainedDate(String criterion)` | criterion | IDate | 获取标准获得日期 |
| `.getFirstProgressDate(String criterion)` | criterion | IDate | 获取首次进度日期 |
| `.obtainCriterion(String criterion)` | criterion | void | 获得标准 |
| `.resetCriterion(String criterion)` | criterion | void | 重置标准 |
| `.setCompleted()` | 无 | bool | 设置为完成 |
| `.resetAll()` | 无 | void | 重置所有进度 |
