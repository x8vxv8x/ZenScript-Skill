---
name: zenscript
description: >
  CraftTweaker 1.12.2 ZenScript 编写、修改和排错支持。用于编写、编辑、
  审查或调试 .zs 脚本；当用户提到 CraftTweaker、ZenScript、CrT、整合包
  配方调整、scripts/ 目录、合成、熔炉、酿造、矿物词典、物品/方块/实体
  事件或模组专属 CraftTweaker 接口时使用。通过优先查阅参考资料来避免
  自造 ZenScript 方法和错误的配方语法。
globs: "**/*.zs"
---

# ZenScript Skill For CraftTweaker 1.12.2

## 核心原则

- 只使用 `references/` 中明确记录的 API；不要凭记忆补全或自造方法。
- 除非用户已经点名文件，否则先读 `references/index.md`，再决定要打开的正文文件。
- 先缩小到 1 到 3 个最可能文件；不要靠目录名猜路径，也不要整批打开同类拆分文件。
- `references/index.md` 只负责路由，不是 API 依据。命中后必须打开正文确认。
- 只有在语法、类型、全局字段、函数、控制流或 import 不确定时，才读 `references/language-basics.md` 的相关章节。
- 如果物品 id、方块 id、meta、NBT、配方名或模组版本不确定，让用户确认。
- 写完脚本后，提醒用户执行 `/ct syntax`，并把报错行号发回来。

## 工作流

处理非琐碎脚本时，按这个顺序执行：
1. 读 `references/index.md`，按关键词和任务类型定位最可能的文件。
2. 判断是 vanilla、utils 还是某个模组接口。
3. 只打开命中的精确文件；长文件先搜标题、方法名、事件名、机器名、导入或示例，再读相关章节。
4. 先看文件头或章节头的 `Mod ID`、`前置条件`、`导入`、`加载器` 和重要说明。
5. 只使用已读文档里出现的方法和属性；找不到就按“不可用”处理。
6. 如果多个已记录 API 都能完成目标但行为不同，先问用户要哪种行为。

## 路由规则

### Vanilla

统一先看 `references/index.md`，找到相关文件后再跳到精确文件。

### Utils

工具类，遇到下面这类需求，先看 `references/index.md` 的 Utils 区域：
- 字符串、文本格式、tooltip、本地化、模板字符串
- 日志、调试输出、预处理器
- 正则、数学、日期时间、UUID、十六进制
- 判空、可选链、空值合并
- 原生方法访问、自定义类、链式执行、区块坐标、配方模式

### Mods

模组接口放在 `references/mods/`。

查找顺序：
1. 提取用户原词、中文名、英文名、缩写、modid、版本词。
2. 规范化后先匹配 `references/mods/` 文件名。
3. 文件名未命中时，再搜文档开头的标题、`Mod ID`、`导入`、重要说明或常见缩写。
4. 只读取少量候选文件的文件头和目标章节；不要先打开多个模组文档做大范围比较。
5. 若有多个候选，先问用户，不要自行决定。

高风险变体必须确认版本：
- `modularmachinery.md` / `modularmachinery-ce.md`
- `nuclearcraft.md` / `nuclearcraft-overhauled.md`
- `immersiveengineering.md` / `immersivepetroleum.md` / `immersiveintelligence.md`

如果用户目标很模糊，例如“矿石翻倍”或“自定义机器配方”，先用 `references/index.md` 缩小 vanilla/utils 范围；若索引未覆盖，再去 `references/mods/` 缩小候选。

## 读取与使用规则

- 长文件不要整篇硬读。优先搜索 `^##`、`^###`、`导入`、方法名、事件名、机器名、`使用示例`。
- 不要因为同一文件里存在别的 API，就推断目标 API 也存在。
- 参考文件常见结构是：文件头、`API 列表`、方法表、属性表、示例、注意事项。只把与当前任务相关的部分作为依据。

API 表读取规则：
- `@ZenGetter`：只读属性，用 `.{属性名}` 访问
- `@ZenSetter`：可写属性，用 `.{属性名} = {值}`
- `@ZenGetter / @ZenSetter`：可读可写
- 方法：按文档中的签名调用

## 脚本风格

- 默认优先写短脚本，尤其是单个事件处理器、少量条件分支、一次性逻辑。
- 事件脚本优先内联：先判断服务端，再判断目标，再处理分支。
- 单次使用、没有复用价值、不会明显降低错误率的小逻辑，不要拆成辅助函数。
- 只有在下面情况才提取函数、常量或额外结构：
  - 同一逻辑重复 2 次以上
  - 用户明确要求“可复用”“便于维护”“模块化”
- 若用户已有现成脚本或明显的简洁风格偏好，优先做最小必要改动。

## 输出前检查

- import 与参考文件一致，并且只在需要时加入
- 用到的每个方法和属性都能在已读文档里找到
- 若语法、类型或 import 是否有不确定之处。如果有，是否已查 `references/language-basics.md`
- 需要名字的配方使用稳定字符串
- 不确定的物品 id、meta、NBT、模组可用性或模组版本已明确指出
- 最终回答提醒用户执行 `/ct syntax`

## 脚本文件约定

- 文件位置：`.minecraft/scripts/`，支持子目录
- 文件扩展名：`.zs`