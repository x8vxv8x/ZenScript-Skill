# ZenClass（自定义类）

ZenScript 支持自定义类，本质上是 Java 类。

---

## 关键字

| 关键字 | 说明 |
|--------|------|
| `zenClass` | 声明类 |
| `zenConstructor` | 构造函数 |
| `val` / `var` | 字段（val 不可变，var 可变） |
| `static` | 静态字段 |
| `function` | 方法 |
| `this` | 当前对象 |

## 示例

```zenscript
zenClass MyClass {
    zenConstructor(arg as string, arg1 as int) {
        myValue = arg;
        myValueTwo = arg1;
    }

    zenConstructor(arg as string) {
        myValue = arg;
        myValueTwo = 25;
    }

    val myValue as string;
    val myValueTwo as int;
    var myValueThree as int;
    static myStaticValue as int = 233;

    function getMyValue() as string {
        return this.myValue;
    }

    function setMyValueThree(arg as int) as MyClass {
        this.myValueThree = arg;
        return this;  // 返回自身支持链式调用
    }
}
```

## 使用

```zenscript
import scripts.Class.MyClass;  // 导入

val obj = MyClass("abc", 1);   // 构造
print(obj.getMyValue());       // 调用方法
print(obj.myValueTwo);         // 访问字段
print(MyClass.myStaticValue);  // 访问静态字段
```