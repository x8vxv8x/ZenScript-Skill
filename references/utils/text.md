# Text CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: 无需导入，`format` 为全局字段

文本格式化 API，支持 `§` 颜色代码。

---

## API 列表

### Format（格式化）

`format` 全局字段提供文本格式化方法，支持 `§` 颜色代码。

#### 颜色

| 方法 | 颜色 |
|------|------|
| `format.black()` | 黑色 |
| `format.darkBlue()` | 深蓝 |
| `format.darkGreen()` | 深绿 |
| `format.darkAqua()` | 深青 |
| `format.darkRed()` | 深红 |
| `format.darkPurple()` | 紫色 |
| `format.gold()` | 金色 |
| `format.gray()` | 灰色 |
| `format.darkGray()` | 深灰 |
| `format.blue()` | 蓝色 |
| `format.green()` | 绿色 |
| `format.aqua()` | 青色 |
| `format.red()` | 红色 |
| `format.lightPurple()` | 粉红 |
| `format.yellow()` | 黄色 |
| `format.white()` | 白色 |

#### 样式

| 方法 | 效果 |
|------|------|
| `format.obfuscated()` | 乱码 |
| `format.bold()` | 粗体 |
| `format.strikethrough()` | 删除线 |
| `format.underline()` | 下划线 |
| `format.italic()` | 斜体 |

---

## 使用示例

```zenscript
<minecraft:stick>.addTooltip(format.green("这不是绳子"));
<minecraft:stick>.addTooltip(format.green(format.italic("绿色斜体")));
<minecraft:stick>.addTooltip(format.red(format.bold("红色粗体")) ~ " 普通文本");
```
