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

---

## ZenUtils 扩展（需安装 ZenUtils 1.24.0+）

ZenUtils 为数组和列表添加了更多操作。

**重要区别**：数组（`E[]`）返回新数组，列表（`[E]`）修改并返回自身。

```zenscript
val array = [1, 2, 3] as int[];
val list = [1, 2, 3] as [int];

val newArray = array.add(4);  // array 不变，返回新数组 [1, 2, 3, 4]
val listItself = list.add(4); // list 变为 [1, 2, 3, 4]，返回自身
```

### 切片语法

`arrayOrList[start .. end]` 从 startIndex（含）到 endIndex（不含）切片。数组切片是克隆的，列表切片共享内存。

```zenscript
val list = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] as [int];
list[2 .. 6].reverse();  // 列表切片共享内存，原列表也被修改
print(toString(list));   // [0, 1, 5, 4, 3, 2, 6, 7, 8, 9]
```

### 数组操作（E[]）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(E)` | E[] | 追加元素，返回新数组 |
| `.addAll(E...)` | E[] | 追加多个元素，返回新数组 |
| `.clone()` | E[] | 浅拷贝 |
| `.indexOf(E)` | int | 查找首次出现的索引，未找到返回 -1 |
| `.indexOf(E, int)` | int | 从指定索引开始查找 |
| `.isEmpty()` | bool | 是否为空（`.length == 0`） |
| `.isNotEmpty()` | bool | 是否非空 |
| `.isSorted()` | bool | 是否按自然顺序排序 |
| `.isSorted(function(E, E)int)` | bool | 是否按自定义比较器排序（E 不能是原始类型） |
| `.lastIndexOf(E)` | int | 查找最后出现的索引 |
| `.lastIndexOf(E, int)` | int | 从指定索引向前查找 |
| `.remove(int)` | E[] | 移除指定索引元素，返回新数组 |
| `.removeAll(int...)` | E[] | 移除多个索引的元素，返回新数组 |
| `.removeElement(E)` | E[] | 移除首次出现的指定元素 |
| `.removeElements(E...)` | E[] | 移除首次出现的多个指定元素 |
| `.removeAllOccurences(E)` | E[] | 移除所有出现的指定元素（注意拼写：单 r） |
| `.reverse()` | void | 反转数组 |
| `.shift(int)` | void | 循环移位 |
| `.shift(int, int, int)` | void | 在指定范围内循环移位 |
| `.sort()` | void | 按自然顺序排序 |
| `.sort(function(E, E)int)` | void | 按自定义比较器排序（E 不能是原始类型） |
| `.swap(int, int)` | void | 交换两个元素 |

### 列表操作（[E]）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(E)` | [E] | 追加元素，返回自身 |
| `.addAll(E...)` | [E] | 追加多个元素，返回自身 |
| `.clone()` | [E] | 浅拷贝 |
| `.clear()` | [E] | 清空列表，返回自身 |
| `.indexOf(E)` | int | 查找首次出现的索引，未找到返回 -1 |
| `.isEmpty()` | bool | 是否为空 |
| `.isNotEmpty()` | bool | 是否非空 |
| `.isSorted()` | bool | 是否按自然顺序排序 |
| `.isSorted(function(E, E)int)` | bool | 是否按自定义比较器排序（E 可以是原始类型） |
| `.lastIndexOf(E)` | int | 查找最后出现的索引 |
| `.removeByIndex(int...)` | [E] | 移除指定索引的元素，返回自身 |
| `.remove(E)` | void | 移除首次出现的指定元素 |
| `.removeAll(E...)` | [E] | 移除首次出现的多个指定元素 |
| `.removeAllOccurrences(E)` | [E] | 移除所有出现的指定元素（注意拼写：双 r） |
| `.reverse()` | [E] | 反转列表，返回自身 |
| `.shift(int)` | [E] | 循环移位，返回自身 |
| `.sort()` | [E] | 按自然顺序排序，返回自身 |
| `.sort(function(E, E)int)` | [E] | 按自定义比较器排序（E 可以是原始类型） |
| `.swap(int, int)` | [E] | 交换两个元素，返回自身 |

### 注意事项

- 数组的 `removeAllOccurences` 拼写为**单 r**，列表的 `removeAllOccurrences` 拼写为**双 r**
- 数组的 `remove`/`removeAll` 按**索引**移除，列表的 `remove` 按**元素**移除
- 列表用 `removeByIndex` 按索引移除
