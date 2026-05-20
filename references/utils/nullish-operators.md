# 空值运算符 CraftTweaker API 参考

> Mod ID: 无
> 前置条件: ZenUtils（版本要求: 1.23.0+）
> 导入: 无需导入

空值运算符提供 `if (isNull(a))` 的简写形式。不适用于原始类型（int、double 等）。

---

## 运算符列表

### ??（空值合并）

左表达式为 null 时返回右表达式，否则返回左表达式。

```zenscript
// getA() ?? getB()
// 等价于:
// val a = getA();
// isNull(a) ? getB() : a;

val data as IData = {};
// data.foo 为 null，返回 100
val value = data.foo?.asInt() ?? 100;
```

### ?=（空值合并赋值）

左操作数为 null 时才赋值。

```zenscript
var a as string;
a ?= "foo";  // a 为 null，赋值为 "foo"
a ?= "bar";  // a 已有值，不赋值

// 等价于:
// if (isNull(a)) { a = "foo"; }
```

适用范围与其他赋值运算符一致：

```zenscript
var a as string;
a += "foo";   // 合法
a ?= "foo";   // 合法

zenClass Foo {
    var bar as string;
    zenConstructor(bar as string) { this.bar = bar; }
}
var foo as Foo;
foo.bar += "baz";   // 合法
foo.bar ?= "baz";   // 合法
```

注意：其他赋值运算符返回修改后的值，但 `?=` 始终返回 void。

### ?.（可选链）

对象为 null 时短路返回 null，不抛出异常。

```zenscript
val data as IData = {};

// data.foo 为 null 时会抛出 NullPointerException
// data.foo.asInt();

// data.foo 为 null 时返回 null
data.foo?.asInt();

// 结合 ?? 提供默认值
data.foo?.asInt() ?? 100;  // 返回 100
```

若成员返回原始类型，`?.` 返回其可空包装类型，可用 `??` 解包。

---

## 使用示例

```zenscript
// 安全访问嵌套数据
val playerData as IData = {};
val level = playerData.PlayerPersisted?.xpLevel?.asInt() ?? 0;

// 安全调用链
val item as IItemStack = null;
val name = item?.displayName ?? "无物品";
```
