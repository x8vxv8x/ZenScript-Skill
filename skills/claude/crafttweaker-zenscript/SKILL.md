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
2. **不确定时，先查阅参考文件再写代码。** 参考文件路径见下方索引。
3. **物品 ID 不确定时，提示用户在游戏中输入 `/ct hand` 获取准确 ID。**
4. **写完脚本后，提示用户运行 `/ct syntax` 检查语法错误。**
5. **不要猜测模组专属 API。** 如果用户要求修改某个模组的配方但你不确定 API，查阅 `references/mods/` 下是否有对应文件，没有则告知用户需要手动查证。

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

## 配方操作速查

### 添加配方

```zenscript
// 有序合成
recipes.addShaped("recipe_name", <输出>, [
    [输入1, 输入2, 输入3],
    [输入4, null, 输入5],
    [输入6, 输入7, 输入8]
]);
// 无序合成
recipes.addShapeless("recipe_name", <输出>, [输入1, 输入2, 输入3]);
// 可翻转有序（像弓那样）
recipes.addShapedMirrored("recipe_name", <输出>, [...]);
// JEI 中隐藏
recipes.addHiddenShaped("recipe_name", <输出>, [...]);
recipes.addHiddenShapeless("recipe_name", <输出>, [...]);
```

- 输出数量：`<minecraft:stick> * 4`
- 空槽位用 `null`
- recipe_name 不能重复，省略则自动生成哈希名

### 移除配方

```zenscript
recipes.remove(<物品>);                          // 删除该物品的所有配方
recipes.removeShaped(<物品>, [...]);              // 删除特定有序配方（输入框可省略）
recipes.removeShapeless(<物品>, [...]);           // 删除特定无序配方
recipes.removeByRecipeName("minecraft:book");     // 按配方 ID 删除
recipes.removeByRegex("minecraft:.*_sword");      // 按正则匹配配方 ID
recipes.removeByMod("modid");                     // 删除某 mod 所有配方
recipes.removeAll();                              // 删除所有配方
```

### 熔炉

```zenscript
furnace.addRecipe(<输出>, <输入>, 经验值);        // 添加熔炉配方
furnace.remove(<输出>, <输入>);                   // 移除（输入可省略）
furnace.setFuel(<燃料>, 燃烧时间ticks);           // 设置燃料（0 = 移除燃料）
```

## IItemStack 常用 API

```zenscript
import crafttweaker.item.IItemStack;

// 属性（ZenGetter）
<minecraft:apple>.displayName;      // 显示名称
<minecraft:apple>.maxStackSize;     // 最大堆叠数
<minecraft:apple>.damage;           // 耐久损耗值
<minecraft:apple>.maxDamage;        // 最大耐久
<minecraft:apple>.metadata;         // Meta 值
<minecraft:apple>.hasTag;           // 是否有 NBT
<minecraft:apple>.tag;              // NBT 数据
<minecraft:apple>.ores;             // 所属矿辞列表
<minecraft:apple>.isEmpty;          // 是否为空

// 设置属性（ZenSetter）
<minecraft:apple>.displayName = "红苹果";
<minecraft:apple>.maxStackSize = 16;

// 方法
<minecraft:apple>.withAmount(3);          // 设置数量
<minecraft:apple>.withDamage(10);         // 设置耐久
<minecraft:apple>.withTag({display: {Name: "test"}});  // 设置 NBT
<minecraft:apple>.withEmptyTag();         // 空 NBT
<minecraft:apple>.withDisplayName("名字"); // 设置显示名（仅单物品）
<minecraft:apple>.withLore(["第一行","第二行"]);  // 设置 Lore
<minecraft:apple>.anyDamage();            // 任意耐久（配方输入用）
<minecraft:apple>.anyAmount();            // 任意数量
<minecraft:apple>.addTooltip("提示");      // 添加提示
<minecraft:apple>.addShiftTooltip("Shift提示"); // Shift 显示
```

## 参考文件索引

### 原版参考（固定）

| 场景 | 文件路径 |
|------|---------|
| IItemStack 完整方法/属性 | `${CLAUDE_SKILL_DIR}/references/vanilla/iitemstack-api.md` |
| 配方系统完整参考 | `${CLAUDE_SKILL_DIR}/references/vanilla/recipe-system.md` |
| 类型系统与 IData | `${CLAUDE_SKILL_DIR}/references/vanilla/type-system.md` |
| 全局函数/Math/格式化 | `${CLAUDE_SKILL_DIR}/references/vanilla/global-api.md` |
| 常见模式与错误排查 | `${CLAUDE_SKILL_DIR}/references/vanilla/common-patterns.md` |

### 模组参考（动态查找）

模组参考文件存放在 `${CLAUDE_SKILL_DIR}/references/mods/` 目录下，按需查找：

1. 用户提到某个模组时，用 Glob 搜索 `${CLAUDE_SKILL_DIR}/references/mods/<modid>.md`
2. **找到** → 读取文件内容，使用其中记录的 API
3. **未找到** → 告知用户该模组的 CraftTweaker API 参考尚未收录，可以参考项目中的 `generate-mod-reference.md` prompt 模板自行生成

### 模糊需求查找策略

当用户提出模糊目标（如"矿石翻倍"、"自定义机器配方"）而未指定模组时：

1. 先用 Glob 列出 `${CLAUDE_SKILL_DIR}/references` 下所有 `.md` 文件
2. 根据文件名判断哪些可能相关（如矿石处理 → mekanism、thermalfoundation、ic2 等）
3. 读取相关文件，确认其 API 是否支持该操作
4. 如果找到可用 API，向用户推荐并说明用法
5. 如果没有相关模组文件，告知用户需要先确认整合包中安装了哪些模组，或提示用户在游戏中运行 `/ct hand` 查看物品归属模组

## 常见陷阱

```zenscript
// 连接字符串用 ~ 不是 +
"hello" ~ " world";    // 正确
"hello" + " world";    // 可能报 NumberFormatException

// val 不可重新赋值，var 可以
val a = 1;  // a = 2; // 错误！
var b = 1;  // b = 2; // 正确

// import 必须在脚本最顶部
import crafttweaker.item.IItemStack;  // 放在文件开头

// null 安全检查
if (!isNull(item)) { ... }

// 条件加载 mod
#modloaded thermalfoundation
#modloaded !thermalfoundation  // mod 未加载时

// 加载优先级（数字越大越先加载）
#priority 100
```

## 脚本文件约定

- 文件位置：`.minecraft/scripts/` 目录，支持子目录
- 文件扩展名：`.zs`
- 编码：UTF-8（无 BOM）
- 标点：英文标点
- 建议按 mod 分文件：`Vanilla.zs`、`ic2.zs`、`thermal.zs` 等
