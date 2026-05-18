# 模板字符串

> 需安装 ZenUtils
> 版本要求: 1.18.0+

使用反引号 `` ` `` 定义模板字符串，支持 `${expression}` 嵌入表达式。

---

## 用法

```zenscript
val name as string = "world";
print(`hello, ${name}!`);

// 动态矿辞查询
function getIngot(type as string) as IItemStack {
    return <ore:ingot${type}>.firstItem;
}

// 动态元数据物品
for i in 0 .. 16 {
    print(<item:minecraft:wool:${i}>.displayName);
}
```
