# Regex Matcher CraftTweaker API 参考

> Mod ID: `ctutils`
> 前置条件: 无
> 导入: `import mods.ctutils.utils.RegexMatcher;`

正则表达式匹配工具。

## API 列表

### RegexMatcher

> `import mods.ctutils.utils.RegexMatcher;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.find(String input, String regex, @Optional int options)` | bool | 检查输入是否匹配正则表达式 |
| `.getCamelCaseParameter()` | int | 获取所有可用参数 |

#### options 参数

使用 `|`（位或）组合多个选项。

| 参数 | 说明 |
|------|------|
| `CANON_EQ` | 规范等价 |
| `CASE_INSENSITIVE` | 不区分大小写 |
| `COMMENTS` | 允许注释和空白 |
| `DOTALL` | 点号匹配所有模式 |
| `LITERAL` | 字面解析 |
| `MULTILINE` | 多行模式 |
| `UNICODE_CASE` | Unicode 大小写 |
| `UNICODE_CHARACTER_CLASS` | Unicode 字符类 |
| `UNIX_LINES` | Unix 行模式 |
