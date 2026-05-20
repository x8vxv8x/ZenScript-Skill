# Date CraftTweaker API 参考

> Mod ID: `ctintegration`
> 前置条件: CraftTweaker Integration
> 导入: 见各章节

## API 列表

### DateUtil

> `import mods.ctintegration.date.DateUtil;`

IDate 工具类。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.now()` | IDate | 获取当前时间 |
| `.fromTimeInMillis(long timeInMillis)` | IDate | 从毫秒时间戳创建 |
| `.parse(String format, String dateString)` | IDate | 从格式化字符串解析。format 为 SimpleDateFormat 格式。格式错误返回 null |

#### 字段常量

以下常量用于 `IDate.getField()` 和 `IDate.setField()`。

| 常量 | 说明 |
|------|------|
| `.ERA()` | 纪元 |
| `.YEAR()` | 年 |
| `.MONTH()` | 月 |
| `.WEEK_OF_YEAR()` | 年中第几周 |
| `.WEEK_OF_MONTH()` | 月中第几周 |
| `.DATE()` | 日 |
| `.DAY_OF_MONTH()` | 月中第几天 |
| `.DAY_OF_YEAR()` | 年中第几天 |
| `.DAY_OF_WEEK()` | 周中第几天 |
| `.DAY_OF_WEEK_IN_MONTH()` | 月中第几个周几 |
| `.AM_PM()` | 上午/下午 |
| `.HOUR()` | 小时（12h） |
| `.HOUR_OF_DAY()` | 小时（24h） |
| `.MINUTE()` | 分钟 |
| `.SECOND()` | 秒 |
| `.MILLISECOND()` | 毫秒 |
| `.ZONE_OFFSET()` | 时区偏移 |
| `.DST_OFFSET()` | 夏令时偏移 |
| `.FIELD_COUNT()` | 字段总数 |

#### 星期常量（用于 DAY_OF_WEEK 字段）

| 常量 | 说明 |
|------|------|
| `.SUNDAY()` | 周日 |
| `.MONDAY()` | 周一 |
| `.TUESDAY()` | 周二 |
| `.WEDNESDAY()` | 周三 |
| `.THURSDAY()` | 周四 |
| `.FRIDAY()` | 周五 |
| `.SATURDAY()` | 周六 |

#### 月份常量（用于 MONTH 字段）

| 常量 | 说明 |
|------|------|
| `.JANUARY()` 至 `.DECEMBER()` | 1-12 月 |
| `.UNDECIMBER()` | 第 13 月 |

#### AM/PM 常量

| 常量 | 说明 |
|------|------|
| `.AM()` | 上午 |
| `.PM()` | 下午 |

### IDate

> `import mods.ctintegration.date.IDate;`

日期时间接口，内部使用 java.util.Calendar 实现。通过 DateUtil 获取实例。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `timeInMillis` | long | 1970/1/1 以来的毫秒数 |
| `year` | int | 年 |
| `month` | int | 月 |
| `day` | int | 日 |
| `dayInWeek` | int | 星期几 |
| `hour` | int | 小时（1天=24小时） |
| `minute` | int | 分钟 |
| `second` | int | 秒 |
| `milliSecond` | int | 毫秒 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getField(int field)` | int | 获取字段值（字段常量从 DateUtil 获取） |
| `.setField(int field, int value)` | void | 设置字段值 |
| `.toString()` | string | 格式化为 `yyyy-MM-dd HH:mm:ss` |
| `.format(String formatString)` | string | 自定义格式化（SimpleDateFormat） |

#### 比较运算符

两个 IDate 实例可用 `<`、`>`、`<=`、`>=`、`==`、`!=` 比较。
