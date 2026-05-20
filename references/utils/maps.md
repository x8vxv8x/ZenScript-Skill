# 映射（关联数组）CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: 无需导入

映射（关联数组）基础语法。

---

## 声明

使用 `{}` 和 `:` 声明映射。格式为 `as ValueType[KeyType]`。

```zenscript
val myMap = {
    dirt : <minecraft:dirt>,
    gold : <minecraft:gold_ingot>
} as IItemStack[string];
```

- 初始声明中，键的纯文本会被解释为字符串
- 几乎所有 ZenScript 类型都可用作键或值

## 访问元素

```zenscript
val assocArray = {
    <minecraft:dirt> : "This is me"
} as string[IItemStack];

// 标准索引访问
print(assocArray[<minecraft:dirt>]);

// 使用变量（类型须匹配）
val dirt = <minecraft:dirt>;
print(assocArray[dirt]);
```

### 字符串键的成员访问

当键为字符串时，可用点号访问。

```zenscript
val assocWithStrings = {
    one : "1",
    two : "2"
} as string[string];

print(assocWithStrings.one);       // 点号访问
print(assocWithStrings["two"]);    // 标准索引访问
```

## 修改与添加

映射大小不固定，向未设置的索引赋值即添加新条目。

```zenscript
val changingArray = {
    <minecraft:dirt> : "this is me",
    <minecraft:gold_ingot> : "and I hate it"
} as string[IItemStack];

val gg = <minecraft:gold>;

// 修改已有条目
changingArray[gg] = "and I love it";

// 添加新条目
changingArray[<minecraft:grass>] = "Power!";
```

## 属性

| 属性 | 返回 | 说明 |
|------|------|------|
| `.keys` / `.keySet` | 数组 | 所有键 |
| `.values` / `.valueSet` | 数组 | 所有值 |
| `.entrySet` | Entry 数组 | 所有键值对 |

---

## 遍历

```zenscript
import crafttweaker.item.IItemStack;
import crafttweaker.item.IIngredient;

val recipeMapShaped = {
    <minecraft:grass> : [[<minecraft:dirt>, <minecraft:dirt>, <minecraft:dirt>],
                         [<minecraft:dirt>, <minecraft:dirt>, <minecraft:dirt>],
                         [<minecraft:dirt>, <minecraft:dirt>, <minecraft:dirt>]],
} as IIngredient[][][IItemStack];

// 键遍历
for key in recipeMapShaped {
    recipes.addShaped(key, recipeMapShaped[key]);
}

// 键值遍历
for key, value in recipeMapShaped {
    recipes.addShaped(key, value);
}
```

---

## ZenType Entry

通过 `entrySet` 获取的 Entry 对象，包含 `.key` 和 `.value` 属性。

```zenscript
val myEntry = map.entrySet[0];
myEntry.key;    // Entry 的键
myEntry.value;  // Entry 的值
```

---

## ZenUtils 扩展（需安装 ZenUtils 1.13.0+）

### OrderlyMap（有序映射）

普通 Map 的迭代顺序不可预测。ZenUtils 提供 `$orderly` 后缀声明有序映射，迭代顺序与插入顺序一致。

```zenscript
// 普通映射 - 迭代顺序不可预测
val map as string[string] = {
    "test": "abc",
    "foo": "bar",
    "mine": "craft"
};

// 有序映射 - 迭代顺序与声明顺序一致
val orderlyMap as string[string]$orderly = {
    "test": "abc",
    "foo": "bar",
    "mine": "craft"
};

for key, value in orderlyMap {
    print(key ~ ": " ~ value);
}
// 输出:
// test: abc
// foo: bar
// mine: craft
```
