# 数组 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: 无需导入

数组基础语法。

---

## 数组操作

### 声明

使用 `[]` 声明数组。**必须初始化**，即使是空数组。

```zenscript
// 正确
var floatArray as float[] = [];

// 错误 — 不会报语法错误，但重载时会出错
// var floatArray as float[];
```

```zenscript
val stringArray = ["Hello", "World"] as string[];
val intArray = [1, 2, 3] as int[];
```

### 类型转换

声明数组时建议使用 `as` 指定类型，否则 ZenScript 可能推断错误。非基础类型（如 IItemStack）需要先 import。

```zenscript
import crafttweaker.item.IItemStack;

val IArray = [<minecraft:gold_ingot>, <minecraft:iron_ingot>] as IItemStack[];
```

### 嵌套数组

```zenscript
val stringArray1 = ["Hello", "World"] as string[];
val stringArray2 = ["I", "am"] as string[];
val stringArrayAll = [stringArray1, stringArray2, ["Butterfly", "!"]] as string[][];

// stringArrayAll[0][1] → "World"
print(stringArrayAll[0][1]);
```

### 访问元素

索引从 0 开始。嵌套数组需要多层索引。

```zenscript
val arr = ["Hello", "World", "I", "am"] as string[];
print(arr[0]);  // "Hello"
```

### 追加元素

使用 `+` 追加单个元素。只能追加单个对象，不能追加数组。

```zenscript
import crafttweaker.item.IItemStack;

val iron = <minecraft:iron_ingot>;
var array as IItemStack[] = [iron, iron, iron];
array += iron;
```

### 属性

| 属性 | 返回 | 说明 |
|------|------|------|
| `.length` | int | 数组长度 |

---

## 遍历

### for 循环

```zenscript
import crafttweaker.item.IItemStack;

val IArray = [<minecraft:dirt>, <minecraft:planks>, <minecraft:diamond>] as IItemStack[];

// 遍历元素
for item in IArray {
    recipes.remove(item);
}

// 带索引遍历
for i, item in IArray {
    print(i ~ ": " ~ item.displayName);
}

// 数字范围
for i in 0 to 10 { print(i); }     // 0 到 9
for i in 10 .. 20 { print(i); }    // 10 到 19

// 遍历模组物品
for item in loadedMods["minecraft"].items {
    recipes.remove(item);
}
```

### while 循环

```zenscript
var i = 0;
while i < 10 {
    print(i);
    i += 1;
}
```

### break

```zenscript
for i in 0 .. 10 {
    if (i == 5) break;
    print(i);
}
```
