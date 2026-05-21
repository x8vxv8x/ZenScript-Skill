# Data CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.data.IData;`

IData 通用数据接口，用于操作 NBT 等数据。

---

## IData（通用数据接口）

IData 是通用数据接口，所有基本类型（short、double、string、int 等）以及某些数组都可以转换为 IData。IData 及其子类与原始类型**不是同一类型**（如 DataBool、DataInt 等）。

```zenscript
val data = "hello" as IData;
val num = 42 as IData;
val list = [1, 2, 3] as IData;
```

### 类型转换

```zenscript
data.asInt();    data.asLong();   data.asDouble(); data.asFloat();
data.asBool();   data.asString(); data.asList();   data.asMap();
// 也可：("1" as IData).asInt()
```

### 二元运算符支持

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

### 索引和成员访问

| 子类 | `[i]` | `.member` | `.length` | `.immutable` | `.update(v)` |
|------|-------|-----------|-----------|--------------|--------------|
| DataBool | - | - | 返回 0 | Y | Y |
| DataInt/Long/Short/Byte/Float/Double | - | - | 返回 0 | Y | Y |
| DataString | Y | - | Y | Y | Y |
| DataList | Y | - | Y | Y | Y |
| DataMap | - | Y | Y | Y | Y |

### 一元运算符

| 子类 | `-`（取反） | `!`（非） |
|------|------------|----------|
| DataBool | - | Y |
| DataInt/Long/Short/Byte | Y | Y |
| DataFloat/Double | Y | - |

---

## DataMap（关联数组）

键为 String，值为 IData。创建的 Map 不可通过直接赋值修改，需通过加减运算创建新 Map。

```zenscript
val map1 = {key1: "hello", key3: "test"} as IData;
val map2 = {key2: "bye", key3: "override"} as IData;

// 访问
var k1 = map1.key1 as IData;              // 点号
var k2 = map1.memberGet("key2") as IData;  // 方法

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
{key: value}                                                         // 基本结构
{display: {Name: "名字", Lore: ["第一行", "第二行"]}}                   // 嵌套
{Unbreakable: 1, HideFlags: 63}                                      // 数字
{Items: [{Slot: 0, id: "minecraft:diamond", Count: 1}]}              // 列表
item.updateTag({Unbreakable: 1});                                    // 更新现有 NBT（不覆盖）
item.withTag({Unbreakable: 1});                                      // 替换 NBT
item.removeTag("display");                                           // 移除单个键
```
---

## 玩家数据持久化

```zenscript
// 写入（ForgeData 死亡时清空，PlayerPersisted 死亡后保留）
events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if (event.player.world.remote) return;
    event.player.update({custom: 1 as byte});                    // ForgeData
    event.player.update({PlayerPersisted: {custom: 1}});         // PlayerPersisted
});

// 读取
events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if (event.player.world.remote) return;
    var data = event.player.data;
    if (!isNull(data.PlayerPersisted.custom)) {
        val value = data.PlayerPersisted.custom.asInt();
    }
});

// 修改（不能直接赋值，需用 update 覆盖）
event.player.update({PlayerPersisted: {custom: 10}});
```
---

## ZenUtils 扩展（需安装 ZenUtils）

> `import mods.zenutils.DataUpdateOperation;`

### IData.deepUpdate（深度更新）

`IData.update` 会覆盖子数据，`deepUpdate` 递归更新子数据，保留未覆盖的字段。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.deepUpdate(IData toUpdate)` | IData | 深度更新，默认 OVERWRITE 行为 |
| `.deepUpdate(IData toUpdate, IData updateOperation)` | IData | 指定更新操作方式 |

### DataUpdateOperation（更新操作）

> `import mods.zenutils.DataUpdateOperation;`

| 操作 | 说明 |
|------|------|
| `OVERWRITE` | 覆盖旧数据（默认行为，等同于 `update`） |
| `APPEND` | 列表/数组：新数据追加到旧数据之后；Map：新数据合并到旧数据中 |
| `MERGE` | 列表/数组：旧数据中不存在的新元素才追加；Map：等同于 APPEND |
| `REMOVE` | 移除指定元素；若更新数据为空则清空原数据 |
| `BUMP` | 将更新数据列表作为单个元素处理（可与其他操作组合） |

### 使用示例

```zenscript
import mods.zenutils.DataUpdateOperation.*;

// Map 深度更新
val a as IData = {foo: {bar: 0}, baz: 5};
print(a.deepUpdate({foo: {abc: 1}}, OVERWRITE));  // {foo: {abc: 1}} - bar 被覆盖

// 列表操作
val list as IData = ["a", "b", "c", "d"];
print(list.deepUpdate(["d", "e", "f", "g"], APPEND));           // ["a","b","c","d","d","e","f","g"]
print(list.deepUpdate(["d", "e", "f", "g"], MERGE));            // ["a","b","c","d","e","f","g"] - 重复不添加
print(list.deepUpdate(["d", "e", "f", "g"], REMOVE));           // ["a","b","c"] - d 被移除
print(list.deepUpdate(["d", "e", "f", "g"], BUMP | APPEND));    // ["a","b","c","d",["d","e","f","g"]]

// 按键指定操作
print(a.deepUpdate({foo: {abc: 1}}, {foo: OVERWRITE}));         // {baz: 5, foo: {abc: 1}}

// 按索引指定操作
val nested as IData = [[1, 2], [3, 4], [5, 6]];
print(nested.deepUpdate([[3, 4], [4, 5], [5, 7]], [OVERWRITE, MERGE]));  // [[3,4],[3,4,5],[5,6,7]]
```
---

## Roids-Tweaker 扩展（需安装 CraftTweaker Integration）

### DataUtil

> `import mods.ctintegration.data.DataUtil;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.fromJSON(String json)` | json | IData | 将 JSON 字符串或 NBT 字符串转换为 IData，错误返回 null |
| `.parse(String json)` | json | IData | 同 `fromJSON`，不同方法名 |
| `.toNBTString(IData data)` | data | string | 转换为 NBT 字符串表示 |
| `.getRawString(IData data)` | data | string | 舍弃类型定义，输出基本类型的 String.valueOf() 结果 |
| `.toJson(IData data)` | data | string | 转换为 JSON（可能丢失类型定义等属性） |
| `.read(String filePath)` | filePath | IData | 读取 JSON 文件。路径相对于实例目录，需包含 .json |
| `.write(String filePath, IData data)` | filePath, data | void | 写入数据到文件，不存在则创建 |

**性能提示：** 文件操作开销较大，重复使用的文件应保存到变量。读取器支持 pretty JSON（包括 json5 注释），写入器始终输出单行。两者都支持 null。

### IData 扩展

可在任何 IData 上调用。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.toNBTString()` | string | 转换为 NBT 字符串 |
| `.getRawString()` | string | 获取原始字符串 |
| `.toJson()` | string | 转换为 JSON |