# CraftTweaker ZenScript Skill for AI Agent

为 AI Agent 提供 CraftTweaker 1.12.2 ZenScript 的正确 API 参考，防止 AI agent 自造方法。

## 功能

- **反幻觉**：agent 写 ZenScript 代码时只使用文档中记录的真实 API
- **自动激活**：编辑 `.zs` 文件或提到 CraftTweaker 时自动加载
- **双层参考**：常用 API 内嵌在 SKILL.md 中，完整 API 按需查阅参考文件
- **中文为主**：说明和注释用中文，API 名保持英文

## 安装

将 `.claude/skills/crafttweaker-zenscript/` 目录复制到你的整合包项目的 `.claude/skills/` 下。
其他Agent参照其官方安装skill的教程

```
你的整合包/
├── .claude/
│   └── skills/
│       └── crafttweaker-zenscript/
│           ├── SKILL.md
│           └── references/
│               ├── vanilla/
│               └── mods/
├── scripts/
│   └── *.zs
└── ...
```

## 使用

无需手动调用。当你在项目中编辑 `.zs` 文件或与 Claude 讨论 CraftTweaker 相关内容时，skill 会自动激活。

你也可以手动调用：在 Claude Code 中输入 `/crafttweaker-zenscript`。

## 包含的 API 参考

### 原版（references/vanilla/）

- `iitemstack-api.md` — IItemStack、IIngredient、IItemDefinition、IOreDictEntry 完整 API
- `recipe-system.md` — 配方添加/移除、熔炉、矿物词典、物品条件/转换器
- `type-system.md` — 类型系统、IData、变量、作用域
- `global-api.md` — 全局函数、Math 包、格式化、运算符、控制流、预处理器
- `common-patterns.md` — 常见模式、NBT、错误排查、CT 命令

### 模组（references/mods/）

- `dropt.md` — Dropt 掉落系统完整 API
- `loottweaker.md` — LootTweaker 战利品表 API
- `_template.md` — 模组 API 参考模板（用于扩展）

## 贡献模组扩展

本项目欢迎社区贡献！你可以为任何有 CraftTweaker 集成的模组添加 API 参考。

### 快速贡献（用 AI 生成）

1. 找到模组的 CraftTweaker 文档（官方 Wiki、MCMOD、GitHub 等）
2. 复制 `generate-mod-reference.md` 中的 prompt
3. 将 prompt 和文档一起发给 AI，生成参考文件
4. 将生成的文件放入 `references/mods/`，提交 PR

详细说明见 [CONTRIBUTING.md](CONTRIBUTING.md)。
