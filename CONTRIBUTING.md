# 贡献指南

感谢你愿意为 CraftTweaker ZenScript Skill 贡献模组扩展参考！

## 什么是模组扩展？

本 skill 的核心是防止 AI agent 自造方法。原版 CraftTweaker API 已经覆盖，但每个模组有自己的 CraftTweaker 集成（如热力基础的熔炉配方、工业的机器配方等）。我们需要为每个常用模组创建一份 API 参考文件，让 agent 也能正确使用这些模组的 CraftTweaker 方法。

## 贡献方式

### 方式一：用 AI 生成（推荐）

你可以用 Claude 或其他 AI 工具，根据模组的文档自动生成参考文件。步骤如下：

1. **找到模组的 CraftTweaker 文档**
   - 官方 Wiki：`https://docs.blamejared.com/1.12/en/Mods/<ModName>`
   - MCMOD Wiki：`https://www.mcmod.cn/class/<id>.html`
   - 模组 GitHub 仓库的 CraftTweaker 集成代码
   - 任何包含 CraftTweaker 方法说明的网页或文件

2. **使用下方的 Prompt 模板**
   将 prompt 和文档内容一起发给 AI，它会生成符合格式的参考文件。

3. **提交生成的文件**
   将生成的 `.md` 文件放入 `references/mods/` 目录，提交 PR。

### 方式二：手动编写

复制 `references/mods/_template.md`，按照模板格式填写模组的 CraftTweaker API。


## 贡献规范

### 文件命名

- 文件名使用模组的 Mod ID，全小写：`thermalfoundation.md`、`mekanism.md`、`tconstruct.md`
- 放在 `references/mods/` 目录下

### 内容质量

- **准确性第一**：只记录真实存在的 API，不要猜测
- **实用为主**：优先记录最常用的操作（添加/移除配方）
- **示例可运行**：代码示例必须使用正确的语法
- **中文说明**：说明和注释用中文，API 名保持英文

### 提交 PR

1. Fork 本仓库
2. 在 `references/mods/` 下创建 `<modid>.md` 文件
3. 在 `SKILL.md` 的参考文件索引表中添加一行
4. 提交 PR，标题格式：`[Mod] 添加 <模组名> API 参考`

### 更新已有参考

如果发现已有参考文件有错误或遗漏：
1. 直接修改文件
2. 提交 PR，标题格式：`[Mod] 修正 <模组名> <具体内容>`