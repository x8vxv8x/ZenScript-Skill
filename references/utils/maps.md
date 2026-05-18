# 映射（关联数组）CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: 无需导入

映射（关联数组）基础语法。

---

## 映射操作

```zenscript
var map as string[int] = {1: "一", 2: "二", 3: "三"};
map[1];           // 访问："一"
map[4] = "四";    // 添加
map[1] = "one";   // 修改

// 字符串键可用点号
var items as IItemStack[string] = {
    gold: <minecraft:gold_ingot>,
    iron: <minecraft:iron_ingot>
};
items.gold;       // 等同于 items["gold"]

// 遍历
for key in map { }                    // 键
for key, value in map { }             // 键值
for entry in map.entrySet { }         // Entry

// 属性
map.keys / map.keySet;     // 键集合
map.values / map.valueSet; // 值集合
map.entrySet;              // Entry 集合
```
