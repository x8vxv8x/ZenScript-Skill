# StringList（字符串列表）CraftTweaker API 参考

> Mod ID: 无
> 前置条件: ZenUtils
> 导入: `import mods.zenutils.StringList;`

字符串列表工具。

---

## API 列表

### StringList（字符串列表）

> `import mods.zenutils.StringList;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `StringList.create(Collection<?>)` | StringList | 从集合创建 |
| `StringList.create(Object[])` | StringList | 从数组创建 |
| `StringList.empty()` | StringList | 创建空列表 |
| `StringList.singletonList(Object)` | StringList | 创建只包含一个元素的列表 |

#### 实例方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.get(int)` | String | 获取指定索引的元素 |
| `.set(int, Object)` | String | 设置指定索引的元素，返回旧元素 |
| `.add(Object)` | bool | 添加元素 |
| `.add(String)` | bool | 添加字符串 |
| `.remove(Object)` | bool | 移除元素 |
| `.remove(String)` | bool | 移除字符串 |
| `.contains(Object)` | bool | 是否包含元素 |
| `.contains(String)` | bool | 是否包含字符串 |
| `.clear()` | void | 清空列表 |
| `.removeIf(StringPredicate)` | bool | 移除匹配谓词的所有字符串，返回是否有移除 |

支持 for 循环遍历。

```zenscript
import mods.zenutils.StringList;

val l = StringList.empty();
l.add("41");
l.add(6);
l.add(<ore:ingotIron>);

for s in l {
    print(s);
}
```
