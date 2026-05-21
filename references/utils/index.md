# Utils 工具索引

`references/utils/` 收录的是通用工具能力，不限于 `IData`、Map、Array。

使用规则：

- 当需求涉及字符串、文本格式、日志、正则、数学、日期时间、预处理器、原生类访问、自定义类、空值安全、模板字符串、链式执行、UUID、区块坐标、十六进制或配方模式时，先读本文件，再打开对应参考。
- 本文件只负责导航，不提供 API 细节。实际写脚本时，仍需打开目标文件，读取文件头的 `Mod ID`、`前置条件`、`导入` 和相关章节。
- 某些工具来自 ZenUtils、CraftTweaker Integration、Roids-Tweaker、EventTweaker 或 CTUtils。若前置条件不满足，按“不可用”处理。

---

## 快速路由

| 需求或关键词 | 先读文件 | 备注 |
|------|------|------|
| NBT、`IData`、数据树、玩家持久化数据、JSON/NBT 转换 | `data.md` | 处理通用数据结构时优先使用 |
| 数组、列表、切片、遍历、追加元素 | `arrays.md` | 包含基础语法和部分扩展 |
| Map、关联数组、键值遍历、有序映射 | `maps.md` | 处理字符串键映射时优先使用 |
| 字符串拼接、批量构造文本、可变字符串 | `mutable-string.md` | 大量拼接文本时优先检查 |
| 静态字符串方法、常见字符串工具 | `static-string.md` | 来自 ZenUtils |
| 字符串列表、字符串集合式处理 | `string-list.md` | 来自 ZenUtils |
| 模板字符串、反引号、`${expression}` 插值 | `template-strings.md` | 来自 ZenUtils |
| 文本颜色、样式、tooltip 格式化、聊天文本 | `text.md` | `format` 为全局字段 |
| 本地化、翻译键、多语言文本 | `i18n.md` | 来自 ZenUtils |
| 正则、模式匹配、提取和校验字符串 | `regex-matcher.md` | 来自 CTUtils |
| 数学计算、随机数、取整、三角函数、对数 | `math.md` | 基础数学入口 |
| 日期、时间、日历字段 | `date.md` | 来自 CraftTweaker Integration |
| UUID 生成、解析、比较 | `uuid.md` | 来自 ZenUtils |
| 十六进制转换 | `hex-helper.md` | 来自 ZenUtils |
| 打印原始日志、调试输出、记录测试数据 | `raw-logger.md` | 写入 `crafttweaker_raw.log` |
| 脚本顶部指令、加载优先级、`#modloaded`、`#loader`、重载控制 | `preprocessor.md` | 预处理器必须放在脚本最顶部 |
| 判空、可选链、空值合并 | `nullish-operators.md` | 来自 ZenUtils |
| 调用 Java 原生类、原生方法、MCP 名映射、向下转型 | `native-method-access.md` | 来自 ZenUtils |
| 自定义类、构造函数、字段和方法封装 | `zenclass.md` | 定义 `zenClass` 时使用 |
| 链式执行、延迟执行、持久化链式任务 | `catenation.md` | 来自 ZenUtils |
| 配方模式、类似 JSON 的配方构造 | `recipe-pattern.md` | 来自 CraftTweaker Integration |
| 区块坐标、`ChunkPos` 封装 | `ichunkpos.md` | 来自 Roids-Tweaker |
| 客户端渲染状态、矩阵/颜色/绘图状态 | `GlStateManager.md` | 来自 EventTweaker |
| 使用 ZenScript 编写 Mixin | `mixin.md` | 高风险能力，先确认用户目标 |

---

## 任务判断提示

- 如果用户说“配方里拼一段动态文本”“给物品加彩色 tooltip”，先看 `text.md`，必要时再看 `template-strings.md` 或 `mutable-string.md`。
- 如果用户说“按条件打印调试信息”“把数据落到日志里排错”，先看 `raw-logger.md`。
- 如果用户说“脚本只在某个模组加载时生效”“只在客户端执行”“支持 `/ct reload`”，先看 `preprocessor.md`。
- 如果用户说“直接调 Java 类”“读 Minecraft 原生对象的方法”，先看 `native-method-access.md`。
- 如果用户说“写个辅助类”“把逻辑封装成对象”，先看 `zenclass.md`。
- 如果用户说“判空简写”“可选链”“默认值回退”，先看 `nullish-operators.md`。
- 如果用户说“正则匹配名字”“检查字符串格式”，先看 `regex-matcher.md`。

---

## 常见组合

- 物品 NBT + 文本输出：`data.md` + `text.md`
- 玩家持久化数据 + 判空：`data.md` + `nullish-operators.md`
- 动态 tooltip 或日志文本：`mutable-string.md` 或 `template-strings.md` + `text.md` 或 `raw-logger.md`
- 事件脚本 + 仅客户端执行：事件参考 + `preprocessor.md`
- 原生对象转换 + 自定义类封装：`native-method-access.md` + `zenclass.md`
