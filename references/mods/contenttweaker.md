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

## API 列表

### MaterialSystem（材料系统）

> `import mods.contenttweaker.MaterialSystem;`

允许批量添加金属的不同部件（齿轮、板、锭等）。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getMaterialBuilder()` | MaterialBuilder | 获取材料构建器 |
| `.getPartBuilder()` | PartBuilder | 获取部件构建器 |
| `.getPartType(string name)` | PartType | 获取部件类型 |

### MaterialBuilder（材料构建器）

> `import mods.contenttweaker.MaterialBuilder;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setName(string name)` | MaterialBuilder | 设置材料 ID |
| `.setColor(int color)` | MaterialBuilder | 设置 RGB 颜色 |
| `.setHasEffect(bool hasEffect)` | MaterialBuilder | 设置是否有附魔光芒 |
| `.build()` | Material | 构建 Material 对象 |

### Material（材料）

> 由 `MaterialBuilder.build()` 获取。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerParts(string[] parts)` | void | 注册多个部件 |
| `.registerPart(string part)` | void | 注册单个部件 |

### PartBuilder（部件构建器）

> `import mods.contenttweaker.PartBuilder;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setName(string name)` | PartBuilder | 设置部件 ID |
| `.setPartType(PartType type)` | PartBuilder | 设置部件类型 |
| `.setOreDictName(string name)` | PartBuilder | 设置矿辞前缀 |
| `.setHasOverlay(bool hasOverlay)` | PartBuilder | 设置是否有覆盖层 |
| `.build()` | Part | 构建 Part 对象 |

### 预设部件类型

**物品**: beam, bolt, casing, clump, crystal, crushed_ore, dense_plate, dirty_dust, dust, gear, ingot, nugget, plate, rod, shard

**方块**: block

**矿石**: ore, dense_ore, poor_ore

**流体**: molten

**护甲**: armor (head, chest, legs, feet)

### MaterialPartData（材料部件数据）

> `import mods.contenttweaker.MaterialPartData;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getData()` | 未说明 | 获取数据对象 |
| `.addDataValue(string name, string value)` | void | 添加数据字段 |

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

---

## 注意事项

- CoT 脚本必须以 `#loader contenttweaker` 开头
- 物品/方块 ID 必须全小写，字母开头，可含数字和下划线
- 注册后不可再修改属性
- 材质文件需放在 resources/contenttweaker/textures/ 对应目录
- 使用 `!world.remote` 确保事件只在服务端执行
