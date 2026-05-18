# ContentTweaker CraftTweaker API 参考

> Mod ID: `contenttweaker`
> 前置条件: CraftTweaker
> 导入: `import mods.contenttweaker.*;`

ContentTweaker (CoT) 允许用 ZenScript 为游戏添加自定义物品、方块、流体、创造标签等。

**重要**: CoT 脚本第一行必须为 `#loader contenttweaker`。

---

## 指令

| 指令 | 用途 |
|------|------|
| `/ct blockmaterial` | 打印所有 Block Material 至日志 |
| `/ct creativetab` | 打印所有创造标签至日志 |
| `/ct soundevent` | 打印所有 SoundEvent 至日志 |
| `/ct soundtype` | 打印所有 SoundType 至日志 |
| `/ct parts` | 打印所有已注册的材料部件至日志 |

---

## 材料系统

> `import mods.contenttweaker.MaterialSystem;`

允许批量添加金属的不同部件（齿轮、板、锭等）。

### MaterialBuilder（材料构建器）

> `import mods.contenttweaker.MaterialBuilder;`

| 方法 | 参数 | 说明 |
|------|------|------|
| `MaterialSystem.getMaterialBuilder()` | 无 | 获取构建器 |
| `.setName(string)` | 材料 ID | 设置名称 |
| `.setColor(int)` | RGB 颜色 | 设置颜色 |
| `.setHasEffect(bool)` | 是否有附魔光芒 | 设置效果 |
| `.build()` | 无 | 构建 Material 对象 |

### PartBuilder（部件构建器）

> `import mods.contenttweaker.PartBuilder;`

| 方法 | 参数 | 说明 |
|------|------|------|
| `MaterialSystem.getPartBuilder()` | 无 | 获取构建器 |
| `.setName(string)` | 部件 ID | 设置名称 |
| `.setPartType(PartType)` | 部件类型 | 设置类型 |
| `.setOreDictName(string)` | 矿辞前缀 | 设置矿辞名 |
| `.setHasOverlay(bool)` | 是否有 overlay | 设置覆盖层 |
| `.build()` | 无 | 构建 Part 对象 |

### 预设部件类型

**物品**: beam, bolt, casing, clump, crystal, crushed_ore, dense_plate, dirty_dust, dust, gear, ingot, nugget, plate, rod, shard

**方块**: block

**矿石**: ore, dense_ore, poor_ore

**流体**: molten

**护甲**: armor (head, chest, legs, feet)

### Material 方法

| 方法 | 说明 |
|------|------|
| `.registerParts(string[])` | 注册多个部件 |
| `.registerPart(string)` | 注册单个部件 |

### MaterialPartData（材料部件数据）

> `import mods.contenttweaker.MaterialPartData;`

| 方法 | 说明 |
|------|------|
| `.getData()` | 获取数据对象 |
| `.addDataValue(string name, string value)` | 添加数据字段 |

**物品字段**: burn (燃烧时间)

**盔甲字段**: durability, enchantability, reduction, toughness

**流体字段**: temperature, density, luminosity, viscosity, vaporize

**矿石字段**: drops, variants, hardness, resistance, harvestLevel, harvestTool

---

## 使用示例

### 批量创建材料部件

```zenscript
#loader contenttweaker
import mods.contenttweaker.MaterialSystem;

val copper as Material = MaterialSystem.getMaterialBuilder().setName("Copper").setColor(0xFF9933).build();
copper.registerParts(["gear", "casing", "rod"]); // 同时注册铜齿轮、铜外壳、铜杆

// 自定义部件
val denseIngotPart = MaterialSystem.getPartBuilder()
    .setName("dense_ingot")
    .setPartType(MaterialSystem.getPartType("item"))
    .setOreDictName("denseIngot")
    .build();
copper.registerPart(denseIngotPart); // 注册致密铜锭
```

---

## 常见错误

| 错误 | 原因 | 修复 |
|------|------|------|
| 脚本无效果 | 未添加 `#loader contenttweaker` | 在脚本第一行添加 |
| 物品/方块不显示 | 缺少材质文件 | 在 resources/contenttweaker/textures/ 下添加对应 png |
| 本地化名称不显示 | 缺少语言文件 | 添加 lang 文件或使用 displayName 赋值 |
| 材料部件不出现 | 未调用 addHeadMaterialStats 等方法 | 确保调用了对应的 add 方法 |

## 注意事项

- CoT 脚本必须以 `#loader contenttweaker` 开头
- 物品/方块 ID 必须全小写，字母开头，可含数字和下划线
- 注册后不可再修改属性
- 材质文件需放在 resources/contenttweaker/textures/ 对应目录
- 使用 `!world.remote` 确保事件只在服务端执行
