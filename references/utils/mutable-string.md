# Mutable String CraftTweaker API 参考

> Mod ID: `ctintegration`
> 前置条件: CraftTweaker Integration
> 导入: `import mods.ctintegration.util.MutableString;`

可变字符串，封装 StringBuilder。大量字符串拼接时比 CraftTweaker 的 `+` 运算更高效，代码也更简洁。

## API 列表

### MutableString

> `import mods.ctintegration.util.MutableString;`

#### 创建方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.create()` | 无 | MutableString | 创建空字符串 |
| `.create(String starting)` | starting | MutableString | 从初始字符串创建 |
| `.format(String starting, Object[] arguments)` | starting, arguments | MutableString | 从格式化字符串创建（调用 String.format） |

#### 操作方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.append(String s)` | s | MutableString | 追加字符串到末尾 |
| `.insert(int offset, String s)` | offset, s | MutableString | 在指定位置插入字符串 |
| `.delete(int start, int end)` | start, end | MutableString | 删除 start 到 end 之间的字符 |
| `.deleteCharAt(int pos)` | pos | MutableString | 删除指定位置的单个字符 |
| `.reverse()` | 无 | MutableString | 反转字符串 |
| `.getLength()` | 无 | int | 获取字符长度 |
| `.indexOf(String character)` | character | int | 查找字符位置（长度不必为 1） |
| `.build()` | 无 | string | 构建最终字符串 |

**注意：** 使用前必须调用 `.build()` 转换为字符串！
