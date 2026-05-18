# Mixin 支持 CraftTweaker API 参考

> Mod ID: 无
> 前置条件: ZenUtils
> 导入: `import mixin.*;`

ZenUtils 支持通过 ZenScript 编写 Mixin，实现 Java 字节码级别的类修改。

---

## API 列表

### 可用类型

| 类型 | 说明 |
|------|------|
| `CallbackInfo` | 回调信息，用于 Inject 钩子 |
| `CallbackInfoReturnable` | 带返回值的回调信息。`getReturnValue()` 返回 `java.lang.Object`，需要强转 |
| `Operation` | 用于 WrapOperation 钩子。`call` 方法接受 `Object...` 并返回 `Object` |

### 内置变量

| 变量 | 说明 |
|------|------|
| `this0` | 目标类实例的引用（当只有一个目标类时）。可访问私有和受保护成员，不处理静态成员 |

### 预处理器指令

| 指令 | 说明 |
|------|------|
| `#loader mixin` | 加载为 mixin loader（脚本不可重载） |
| `#mixin NAME` | Mixin 注解头（如 `Mixin`、`ModifyConstant`、`Shadow`、`Static`） |
| `#mixin` (v1.21.2+) | 当注解为 `Mixin` 时的简写 |
| `#{...}` | JSON 注解体，每行需以 `#` 开头 |
| `#sideonly client` | 仅客户端加载 |
| `#mixin Static` | 标记为静态方法 |
| `#mixin Shadow` | Shadow 目标类字段 |
| `#mixin Local` | 本地变量捕获注解。支持 `parameter`、`ordinal`、`index`、`name`、`ref` 参数 |
| `#mixin Share` | 共享本地变量注解 |
| `#mixin Cancellable` | 可取消钩子注解 |

参数索引约定：`0`=第一个，`1`=第二个，`-1`=最后一个，`-2`=倒数第二个。

无注解的函数会被直接注入到目标类中，可添加新方法或暴露私有成员。

---

## 注意事项

- Mixin 脚本中只能使用原生类型（因为 mixin 脚本在 CraftTweaker 注册类型之前加载）
- SRG 名称必须用于注入点，MCP 名称不可在注解中使用但可在函数体中使用
- Mixin 脚本不可重载（使用 `#loader mixin` 时）
