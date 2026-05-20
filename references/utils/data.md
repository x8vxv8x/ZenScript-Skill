# Data CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.data.IData;`

IData 通用数据接口，用于操作 NBT 等数据。

---

## API 列表

### IData（通用数据接口）

> `import crafttweaker.data.IData;`

IData 是通用数据接口，用于操作 NBT 等数据。所有基本类型（short、double、string、int 等）以及某些数组都可以转换为 IData。

注意：IData 及其子类与原始类型**不是同一类型**，它们被称为数据类型（如 DataBool、DataInt 等）。

#### 基本类型转 IData

```zenscript
val data = "hello" as IData;
val num = 42 as IData;
val list = [1, 2, 3] as IData;
```

#### 类型转换

```zenscript
data.asInt();
data.asLong();
data.asDouble();
data.asFloat();
data.asBool();
data.asString();
data.asList();
data.asMap();
```

也可通过 IData 转换类型：`("1" as IData).asInt()`

#### 二元运算符支持

| 子类 | `+` | `-` | `*` | `/` | `%` | `&` | `\|` | `^` | `in` | `==` | `<, >, <=, >=` |
|------|-----|-----|-----|-----|-----|-----|------|------|------|------|----------------|
| DataBool | - | - | - | - | - | Y | Y | Y | Y | Y | - |
| DataByte | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| DataDouble | Y | Y | Y | Y | Y | - | - | - | Y | Y | Y |
| DataFloat | Y | Y | Y | Y | Y | - | - | - | Y | Y | Y |
| DataInt | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| DataLong | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| DataShort | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y | Y |
| DataString | Y | - | - | - | - | - | - | - | Y | Y | Y |
| DataMap | Y | Y | - | - | - | - | - | - | Y | Y | - |
| DataList | Y | - | - | - | - | - | - | - | Y | Y | - |

#### 索引和成员访问

| 子类 | `[i]` | `.member` | `.length` | `.immutable` | `.update(v)` |
|------|-------|-----------|-----------|--------------|--------------|
| DataBool | - | - | 返回 0 | Y | Y |
| DataInt/Long/Short/Byte/Float/Double | - | - | 返回 0 | Y | Y |
| DataString | Y | - | Y | Y | Y |
| DataList | Y | - | Y | Y | Y |
| DataMap | - | Y | Y | Y | Y |

#### 一元运算符

| 子类 | `-`（取反） | `!`（非） |
|------|------------|----------|
| DataBool | - | Y |
| DataInt/Long/Short/Byte | Y | Y |
| DataFloat/Double | Y | - |

### DataMap（关联数组）

> `import crafttweaker.data.IData;`

DataMap 是一种关联数组（Map），扩展了 IData。键为 String，值为 IData。

#### 创建

```zenscript
val myMap = {key1: "value1", key2: "value2", key3: 3} as IData;

// 嵌套
val nestedMap = {key1: {key1: "hello"}} as IData;
```

#### 访问成员

```zenscript
var k1 = myMap.key1 as IData;              // 点号访问
var k2 = myMap.memberGet("key2") as IData;  // 方法访问
```

#### 修改

创建的 Map 是不可变的，但可以通过加减运算创建新 Map：

```zenscript
val map1 = {key1: "hello", key3: "test"} as IData;
val map2 = {key2: "bye", key3: "override"} as IData;

// 合并（后面的覆盖前面的）
(map1 + map2).asString();  // {key1: "hello", key2: "bye", key3: "override"}

// 移除键
(map1 - "key1").asString();  // {key3: "test"}

// 移除另一个 Map 中的所有键
(map1 - map2).asString();  // {key1: "hello"}
```

---

## NBT 标签构造

```zenscript
// 基本结构
{key: value}

// 嵌套
{display: {Name: "名字", Lore: ["第一行", "第二行"]}}

// 数字
{Unbreakable: 1, HideFlags: 63}

// 列表
{Items: [{Slot: 0, id: "minecraft:diamond", Count: 1}]}

// 更新现有 NBT（不覆盖）
item.updateTag({Unbreakable: 1});

// 替换 NBT
item.withTag({Unbreakable: 1});

// 移除单个键
item.removeTag("display");
```

---

## 玩家数据持久化

### 写入数据

```zenscript
events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if (event.player.world.remote) return;
    // 写入到 ForgeData（死亡时清空）
    event.player.update({custom: 1 as byte});
    // 写入到 PlayerPersisted（死亡后保留）
    event.player.update({PlayerPersisted: {custom: 1}});
});
```

### 读取数据

```zenscript
events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if (event.player.world.remote) return;
    var data = event.player.data;
    if (!isNull(data.PlayerPersisted.custom)) {
        val value = data.PlayerPersisted.custom.asInt();
        print(value);
    }
});
```

### 修改数据

```zenscript
// 不能直接赋值：event.player.data.PlayerPersisted.custom = 10; // 错误！
// 需要用 update 覆盖
event.player.update({PlayerPersisted: {custom: 10}});
```

---

## ZenUtils 扩展（需安装 ZenUtils）

> `import mods.zenutils.DataUpdateOperation;`

### IData.deepUpdate（深度更新）

@since 1.14.0

`IData.update` 会覆盖子数据，而 `deepUpdate` 会递归更新子数据，保留未覆盖的字段。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.deepUpdate(IData toUpdate)` | IData | 深度更新，默认 OVERWRITE 行为 |
| `.deepUpdate(IData toUpdate, IData updateOperation)` | IData | 指定更新操作方式 |

#### DataUpdateOperation（更新操作）

> `import mods.zenutils.DataUpdateOperation;`

| 操作 | 说明 |
|------|------|
| `OVERWRITE` | 覆盖旧数据（默认行为，等同于 `update`） |
| `APPEND` | 列表/数组：新数据追加到旧数据之后；Map：新数据合并到旧数据中 |
| `MERGE` | 列表/数组：旧数据中不存在的新元素才追加；Map：等同于 APPEND |
| `REMOVE` | 移除指定元素；若更新数据为空则清空原数据 |
| `BUMP` | 将更新数据列表作为单个元素处理（可与其他操作组合） |

#### 使用示例

```zenscript
import crafttweaker.data.IData;
import mods.zenutils.DataUpdateOperation.OVERWRITE;
import mods.zenutils.DataUpdateOperation.APPEND;
import mods.zenutils.DataUpdateOperation.MERGE;
import mods.zenutils.DataUpdateOperation.REMOVE;
import mods.zenutils.DataUpdateOperation.BUMP;

val a as IData = {foo: {bar: 0}, baz: 5};
val b as IData = {foo: {abc: 1}};

// OVERWRITE: {foo: {abc: 1}} - bar 被覆盖
print(a.deepUpdate(b, OVERWRITE));

// 列表操作
val listA as IData = ["a", "b", "c", "d"];
val listB as IData = ["d", "e", "f", "g"];

// APPEND: ["a", "b", "c", "d", "d", "e", "f", "g"]
print(listA.deepUpdate(listB, APPEND));

// MERGE: ["a", "b", "c", "d", "e", "f", "g"] - 重复的 d 不添加
print(listA.deepUpdate(listB, MERGE));

// REMOVE: ["a", "b", "c"] - d 被移除
print(listA.deepUpdate(listB, REMOVE));

// BUMP | APPEND: ["a", "b", "c", "d", ["d", "e", "f", "g"]] - 整个列表作为单个元素
print(listA.deepUpdate(listB, BUMP | APPEND));

// 按键指定操作
val treeA as IData = {foo: {bar: 0}, baz: 5};
val treeB as IData = {foo: {abc: 1}};
// {baz: 5, foo: {abc: 1}} - 只对 foo 使用 OVERWRITE
print(treeA.deepUpdate(treeB, {foo: OVERWRITE}));

// 按索引指定操作
val nestedA as IData = [[1, 2], [3, 4], [5, 6]];
val nestedB as IData = [[3, 4], [4, 5], [5, 7]];
// [[3, 4], [3, 4, 5], [5, 6, 7]] - 索引0用OVERWRITE，索引1用MERGE，索引2沿用MERGE
print(nestedA.deepUpdate(nestedB, [OVERWRITE, MERGE]));
```
