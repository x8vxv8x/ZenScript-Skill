# 常见模式与错误排查

## 配方模式

### 批量修改配方（循环）

```zenscript
import crafttweaker.item.IItemStack;

var logs as IItemStack[] = [
    <minecraft:log>, <minecraft:log:1>, <minecraft:log:2>,
    <minecraft:log:3>, <minecraft:log:4>, <minecraft:log:5>
];
var planks as IItemStack[] = [
    <minecraft:planks>, <minecraft:planks:1>, <minecraft:planks:2>,
    <minecraft:planks:3>, <minecraft:planks:4>, <minecraft:planks:5>
];

for i, log in logs {
    var plank = planks[i];
    recipes.removeShapeless(plank, [log]);
    recipes.addShapeless(plank * 2, [log]);
}
```

### 用 IItemDefinition 批量操作

```zenscript
import crafttweaker.item.IItemDefinition;
val woolDef as IItemDefinition = <minecraft:wool>.definition;

for i in 0 to 16 {
    recipes.remove(woolDef.makeStack(i));
}
```

### NBT 物品配方

```zenscript
// 带 NBT 的输出
recipes.addShapeless("soap", <minecraft:iron_ingot>.withTag({display: {Name: "肥皂"}}),
    [<ore:dirt>, <ore:dirt>, <minecraft:clay_ball>]);

// 带 NBT 的输入（精确匹配）
recipes.addShaped("nbt_recipe", <minecraft:diamond>, [
    [<minecraft:iron_ingot>.withTag({Unbreakable: 1}), null, null],
    [null, null, null],
    [null, null, null]
]);
```

### 条件加载（多 mod 兼容）

```zenscript
#modloaded thermalfoundation
#priority 10
import crafttweaker.item.IItemStack;

// 只有热力基础加载时才执行
recipes.remove(<thermalfoundation:material:128>);
recipes.addShaped("copper_ingot", <thermalfoundation:material:128>, [
    [<ore:oreCopper>]
]);
```

### 物品转换器组合

```zenscript
// 工具不消耗 + 掉耐久
recipes.addShapeless("plank_axe", <minecraft:planks> * 6, [
    <minecraft:iron_axe>.reuse().transformDamage(), <minecraft:log>
]);

// 物品转换：牛奶桶 → 空桶
recipes.addShapeless("cake", <minecraft:cake>, [
    <minecraft:milk_bucket>.transformReplace(<minecraft:bucket>),
    <minecraft:sugar>, <minecraft:wheat>, <minecraft:egg>
]);
```

---

## NBT 标签构造

```zenscript
// 基本结构
{key: value}

// 嵌套
{display: {Name: "名字", Lore: ["第一行", "第二行"]}}

// 数字
{Unbreakable: 1, HideFlags: 63}

// 列表
{Items: [{Slot: 0, id: "minecraft:diamond", Count: 1}]}

// 更新现有 NBT（不覆盖）
item.updateTag({Unbreakable: 1});

// 替换 NBT
item.withTag({Unbreakable: 1});

// 移除单个键
item.removeTag("display");
```

---

## 常见错误及原因

### 编译时错误

| 错误信息 | 原因 | 修复 |
|---------|------|------|
| `unexpected end of file - ; expected` | 缺少分号 | 补上 `;` |
| `No such member: xxx` | import 路径错误 | 检查 import 拼写 |
| `could not find type XXX` | 忘记 import | 在文件顶部添加 import |
| `import must be at top` | import 不在文件开头 | 移到最顶部 |
| `No such member in IItemStack: xxx` | 方法不存在 | **查阅 API 文档，不要自造方法** |
| `Could not resolve <xxx:yyy>` | 物品 ID 错误 | 用 `/ct hand` 获取正确 ID |
| `value cannot be changed` | 对 val 重新赋值 | 改用 var |
| `not a valid lvalue` | 对函数参数赋值 | 创建新变量接收 |
| `2 methods available but none matches` | 参数类型错误 | 检查输入类型（输出必须 IItemStack） |

### 运行时错误

| 错误信息 | 原因 | 修复 |
|---------|------|------|
| `NumberFormatException` | 用 `+` 连接字符串和数字 | 改用 `~` |
| `ArrayIndexOutOfBoundsException` | 数组越界 | 检查循环范围 |
| `NullPointerException` | 空指针 | 用 `isNull()` 检查 |

### Null 安全模式

```zenscript
// 错误：直接访问可能为 null 的对象
var offItem as IItemStack = player.offHandHeldItem;
if (offItem.definition.id == "minecraft:sand") { ... }  // NPE!

// 正确：先检查 null
if (!isNull(offItem) && offItem.definition.id == "minecraft:sand") { ... }

// && 短路：第一个为 false 时第二个不会执行
```

---

## 作用域规则

```zenscript
import crafttweaker.item.IItemStack;

global a as int = 450;                        // 全局作用域
static b as int = 100;                        // 全局作用域
val item as IItemStack = <minecraft:apple>;   // 脚本作用域

for i in 0 .. 10 {                            // i = 参数作用域
    val j as int = i * 5;                     // j = 局部作用域
    // val i as int = 233;  // 错误：i 已在参数作用域
    // val item = ...;      // 错误：item 已在脚本作用域
    if (i < 4) {
        val k as int = i + 1;                 // k = if 块内局部
        print(k);
    }
    // print(k);  // 错误：k 不在此作用域
}
// print(i);  // 错误：i 只在 for 循环内
```

---

## CT 命令速查

| 命令 | 用途 |
|------|------|
| `/ct hand` | 打印手中物品 ID 和矿辞，复制到剪贴板 |
| `/ct syntax` | 检查脚本语法错误 |
| `/ct conflict` | 打印冲突配方到日志 |
| `/ct inventory` | 打印物品栏所有物品 ID 到日志 |
| `/ct liquids` | 打印所有流体信息到日志 |
| `/ct seeds` | 打印打草掉落物及权重到日志 |
| `/ct docs` | 打开 CrT wiki |
| `/ct help` | 查看指令帮助 |
