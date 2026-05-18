---
name: crafttweaker-zenscript
description: >
  CraftTweaker 1.12.2 ZenScript 编程辅助。当编写、编辑或调试 .zs 脚本文件时自动激活。
  触发场景：用户提到 CraftTweaker/ZenScript/crt、修改配方/合成表/熔炉、操作矿物词典、
  修改物品属性、编写整合包脚本、在 scripts/ 目录下工作。
  Provides correct API references for ZenScript to prevent hallucinated methods.
allowed-tools: Read Glob Grep
paths: "**/*.zs"
---

# CraftTweaker 1.12.2 ZenScript 参考

## 反幻觉规则（最高优先级）

**绝对禁止自造方法或属性。** 你必须严格遵守以下规则：

1. **只使用本文档和参考文件中列出的 API。** 如果一个方法不在文档中，它不存在。
2. **不确定时，先查阅参考文件再写代码。** 不确定使用什么方法或者不知道该方法如何使用时，先阅读参考文件，参考文件路径见下方索引。
3. **物品 ID 不确定时，提示用户在游戏中输入 `/ct hand` 获取准确 ID。**
4. **写完脚本后，提示用户运行 `/ct syntax` 检查语法错误。**
5. **不要猜测模组专属 API。** 如果用户要求修改某个模组的配方但你不确定 API，查阅 `references/mods/` 下是否有对应文件，没有则告知用户需要手动查证。
6. **如果有多个方法或API可以达到同样的效果，询问用户使用哪个方法**

## 类型层级

```
IIngredient（接口，配方输入槽接受的类型）
├── IItemStack（物品，如 <minecraft:apple>）
├── IOreDictEntry（矿辞，如 <ore:ingotIron>）
└── ILiquidStack（流体，如 <liquid:water>）
```

- 配方**输出**必须是 `IItemStack`
- 配方**输入**接受 `IIngredient`（即 IItemStack、IOreDictEntry、ILiquidStack 都可以）
- 导入：`import crafttweaker.item.IItemStack;` / `import crafttweaker.item.IIngredient;`

## 尖括号语法（Bracket Handlers）

```zenscript
<minecraft:apple>           // 物品 IItemStack（item: 前缀可省略）
<minecraft:wool:*>          // 所有子类型（通配符 meta）
<ore:ingotIron>             // 矿辞 IOreDictEntry
<entity:minecraft:creeper>  // 实体 IEntityDefinition
<liquid:water>              // 流体 ILiquidStack
<blockstate:minecraft:stone>// 方块状态 IBlockState
<potion:minecraft:speed>    // 药水效果 IPotion
```

## API/方法 类型

- @ZenGetter：只读属性，使用 `.{属性名}` 访问
- @ZenSetter：可写属性，使用 `.{属性名} = {值}`
- @ZenGetter / @ZenSetter：读写属性，使用 `.{属性名}` 访问，`.{属性名} = {值}` 修改
- 方法：使用 `.{方法签名}({参数})` 调用

## 快速索引(`${CLAUDE_SKILL_DIR}/references/`目录下)

### vanilla/ 原版/通用

| 需求 | 文件 | 关键内容 |
|------|------|---------|
| 物品/IItemStack | vanilla/items.md | 属性、方法、条件、转换器、CoT 自定义物品、ZenUtils 扩展物品 |
| 方块 | vanilla/blocks.md | IBlock/IBlockState/IBlockDefinition、CoT 自定义方块、ZenUtils 扩展方块 |
| 流体 | vanilla/liquids.md | ILiquidStack、CoT 自定义流体 |
| 创造标签页 | vanilla/creative-tabs.md | ICreativeTab、CoT 自定义标签页 |
| Tile Entity | vanilla/tile-entity.md | ITileEntity、ZenUtils TileEntity 扩展 |
| 合成配方 | vanilla/recipes/crafting.md | addShaped/Shapeless/remove |
| 熔炉/酿造 | vanilla/recipes/furnace-brewing.md | furnace/brewing/seeds |
| 实体(基础) | vanilla/entities/base.md | IEntity/IEntityLivingBase/IEntityLiving |
| 实体(高级) | vanilla/entities/specialized.md | IEntityDefinition/drops/属性系统 |
| 事件(使用方法和概述) | vanilla/events/overview.md | 接口、完整事件列表 |
| 事件(方块) | vanilla/events/block.md | BlockBreak/HarvestDrops 等 |
| 事件(实体) | vanilla/events/entity.md | EntityJoin/LivingDeath 等 |
| 事件(玩家) | vanilla/events/player.md | PlayerCrafted/Interact 等 |
| 事件(其他) | vanilla/events/other.md | Arrow/Tick/Explosion/ZenUtils |
| 世界 | vanilla/world.md | IWorld/IBlockPos/IFacing |
| 玩家 | vanilla/players.md | IPlayer/IFoodStats |
| 命令 | vanilla/commands.md | ICommandSender/ZenCommand |
| 附魔 | vanilla/enchantments.md | IEnchantment |
| 药水 | vanilla/potions.md | IPotion/IPotionEffect |
| 伤害 | vanilla/damage.md | IDamageSource |
| 生物群系 | vanilla/biomes.md | IBiome |
| 容器 | vanilla/container.md | IContainer/IInventorySlot |
| 矿物词典 | vanilla/ore-dictionary.md | IOreDict |
| 发射器 | vanilla/dispenser.md | IDispenser |
| 游戏全局 | vanilla/game.md | IGame/IServer/IClient |

### utils/ 工具函数

| 文件 | 关键内容 |
|------|---------|
| utils/data.md | IData 数据操作 |
| utils/text.md | 文本/格式化 |
| utils/math.md | 数学函数 |
| utils/arrays.md | 数组操作 |
| utils/maps.md | Map 操作 |
| utils/preprocessor.md | 预处理器指令（含 ZenUtils #suppress/#hardfail） |
| utils/mixin.md | Mixin 支持 |
| utils/catenation.md | Catenation 链式操作 |
| utils/template-strings.md | 模板字符串 |
| utils/hex-helper.md | HexHelper 十六进制工具 |
| utils/i18n.md | CrTI18n 国际化 |
| utils/uuid.md | CrTUUID 工具 |
| utils/static-string.md | StaticString 静态字符串 |
| utils/string-list.md | StringList 字符串列表 |

### 根目录文件

| 文件 | 关键内容 |
|------|---------|
| global-functions.md | 全局函数（含 ZenUtils 全局函数） |
| language-basics.md | 语言基础 |
| variable-types.md | 变量类型 |

### 模组参考（动态查找）

模组参考文件存放在 `${CLAUDE_SKILL_DIR}/references/mods/` 目录下，按需查找：

1. 用户提到某个模组时，搜索 `${CLAUDE_SKILL_DIR}/references/mods/<modid>.md`
2. **找到** → 读取文件内容，使用其中记录的 API
3. **未找到** → 告知用户该模组的 CraftTweaker API 参考尚未收录，可以参考项目中的 `generate-mod-reference.md` prompt 模板自行生成

### 模糊需求查找策略

当用户提出模糊目标（如"矿石翻倍"、"自定义机器配方"）而未指定模组时：

1. 列出 `${CLAUDE_SKILL_DIR}/references` 下所有 `.md` 文件
2. 根据文件名判断哪些可能相关（如矿石处理 → mekanism、thermalfoundation、ic2 等）
3. 读取相关文件，确认其 API 是否支持该操作
4. 如果找到可用 API，向用户推荐并说明用法
5. 如果没有相关模组文件，告知用户需要先确认整合包中安装了哪些模组，或提示用户在游戏中运行 `/ct hand` 查看物品归属模组

## 脚本文件约定

- 文件位置：`.minecraft/scripts/` 目录，支持子目录
- 文件扩展名：`.zs`