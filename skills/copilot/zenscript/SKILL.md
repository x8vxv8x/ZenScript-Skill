---
applyTo: "**/*.zs"
---

# CraftTweaker 1.12.2 ZenScript

## 硬规则

- 不要自造 ZenScript API。只允许使用随 Skill 提供的 `references/` 文件里明确写出的 API。
- 不确定方法、属性、导入、前置条件或语法时，先查参考文件，不要凭记忆补全。
- 如果物品 id、方块 id、meta、NBT 结构或配方名不确定，让用户确认，或提示他在游戏里执行 `/ct hand`。
- 脚本写完后，提醒用户在游戏里执行 `/ct syntax`，并把报错行号发回来。

## 工作流

处理每个非琐碎脚本时，按下面顺序执行：

1. 读取 `references/language-basics.md`，确认基础语法、括号处理器、类型、全局字段、控制流、函数和 import。
2. 判断任务类别：原版合成、熔炉/酿造/种子、事件、物品/方块/流体、工具类型，或某个模组的扩展接口。
3. 根据"查阅路线"打开任务相关参考文件。长文件不要整篇硬读，先搜索标题、导入、前置条件、方法名、事件名或机器名，再读取相关章节。
4. 读取目标文件开头的 `Mod ID`、`前置条件`、`导入`、`加载器` 和重要说明。
5. 只使用已加载参考中出现的方法/属性；不在参考里的 API 按"不可用"处理。
6. 如果多个已记录 API 都能完成同一件事，而且行为不同，先问用户要哪种行为；如果只是写法不同，选最简单、最直接的已文档化方案。

## 参考资料位置

使用随 Skill 打包的 `references/` 目录；如果缺失，就说明参考资料丢失，务必停止工作并告知用户。

## 参考导航

`references/` 包含 `language-basics.md`、`vanilla/`、`utils/`、`mods/`。

### 参考文件格式

大多数参考文件使用相同格式：文件头写 `Mod ID`、`前置条件`、`导入`，有些还写 `加载器` 或重要说明；`API 列表` 下按类、机器或管理器分节；方法表为 `方法 / 返回 / 说明`，属性表为 `属性 / 类型 / 说明`；末尾可能有 `使用示例`、`常见错误`、`注意事项`。

阅读长文件时，先用标题或关键词定位，例如 `^##`、`^###`、`导入`、目标机器名、方法名、事件名、`使用示例`。只把相关章节作为依据，不要因为同一文件里其他 API 存在就推断目标 API 存在。

### API 表读取规则

- @ZenGetter：只读属性，使用 `.{属性名}` 访问
- @ZenSetter：可写属性，使用 `.{属性名} = {值}`
- @ZenGetter / @ZenSetter：读写属性，使用 `.{属性名}` 访问，`.{属性名} = {值}` 修改
- 方法：使用 `.{方法签名}({参数})` 调用

### 查阅路线

始终先读 `language-basics.md`，再按需求追加读取，例如：

| 用户需求 | 追加读取 |
|------|------|
| 工作台合成、移除、替换、配方函数 | `vanilla/recipes/crafting.md` |
| 熔炉、酿造、草丛种子掉落 | `vanilla/recipes/furnace-brewing.md` |
| 物品数量、NBT、条件、转换器 | `vanilla/items.md`，需要 NBT 时再读 `utils/data.md` |
| 方块、方块状态、世界操作 | `vanilla/blocks.md`、`vanilla/world.md` |
| 玩家、实体、掉落、伤害 | `vanilla/players.md`、`vanilla/entities/`、`vanilla/damage.md` |
| 事件监听 | `vanilla/events/overview.md`，再读 `block.md`、`entity.md`、`player.md` 或 `other.md` |
| 模组机器配方或专属系统 | 按"模组匹配"定位 `mods/*.md` |
| NBT、IData、Map/List 数据 | `utils/data.md`、`utils/maps.md`、`utils/arrays.md` |

## 模组匹配

模组参考文件存放在 `references/mods/` 目录下，按需查找：

1. 用户提到某个模组时，不要只拼接文件名。先按"模组名称模糊匹配流程"查找候选文件。
2. 找到候选后，读取文件头、目标类/机器章节和示例，使用其中记录的 API。
3. 遇到同名或变体模组时先确认版本，例如 `modularmachinery.md` 与 `modularmachinery-ce.md`、`nuclearcraft.md` 与 `nuclearcraft-overhauled.md`。
4. 没找到就告诉用户该模组的 CraftTweaker API 参考尚未收录，或者请他提供文档。

### 名称模糊匹配流程

用户可能使用中文名、英文全称、缩写、带空格写法、带连字符写法或 modid。按下面顺序查找：

1. 提取用户原词和上下文关键词，保留中文名、英文名、缩写和版本词。
2. 规范化待查词：转小写，去掉空格、连字符、下划线、冒号、撇号和中文标点；同时保留原词用于全文搜索。
3. 先匹配 `references/mods/` 文件名的规范化形式。
4. 如果文件名未命中，搜索模组文档开头的标题、`Mod ID`、`导入`、重要说明和常见缩写。
5. 如果仍未命中，全文搜索 `references/mods/`，但只把搜索命中的文件作为候选，仍必须打开文件头确认。
6. 如果出现多个候选，列出候选并询问用户具体是哪一个，不要自行选择。

### 高风险变体

| 用户说法 | 候选文件 | 注意 |
|------|------|------|
| 模块化机械 / Modular Machinery / MMCE | `modularmachinery.md` 或 `modularmachinery-ce.md` | 两者 `Mod ID` 都是 `modularmachinery`，必须确认是否社区版 |
| NuclearCraft / NC | `nuclearcraft.md` 或 `nuclearcraft-overhauled.md` | 普通版和 Overhauled 共用 `Mod ID: nuclearcraft`，必须确认版本 |
| 沉浸工程 / IE | `immersiveengineering.md`、`immersivepetroleum.md`、`immersiveintelligence.md` | 同系列文件较多，按用户目标确认 |

### 模糊需求

当用户提出模糊目标（如"矿石翻倍""自定义机器配方"）而未指定模组时：

1. 先列出或搜索 `references` 下所有 `.md` 文件。
2. 根据文件名、文件头和标题判断哪些可能相关。
3. 读取候选文件的文件头、标题和 API 表，确认其 API 是否支持该操作。
4. 如果找到可用 API，就推荐并说明用法。
5. 如果没有相关模组文件，就告诉用户先确认整合包里装了哪些模组，或者在游戏里执行 `/ct hand` 查看物品归属模组。

## 输出检查清单

在最终输出 ZenScript 之前，确认：

- import 与参考文件一致，并且只在需要时加入
- 用到的每个方法/属性都能在已加载参考文件里找到
- 已先读取 `references/language-basics.md`，再读取任务相关 API 文件
- 需要名字的配方必须使用稳定的字符串
- 不确定的物品 id、meta、NBT 或模组可用性要明确指出
- 最终回答要提醒用户用 `/ct syntax` 检查语法

## 脚本文件约定

- 文件位置：`.minecraft/scripts/` 目录，支持子目录
- 文件扩展名：`.zs`
