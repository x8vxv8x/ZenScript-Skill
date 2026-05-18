# KeyBindingTweaker CraftTweaker API 参考

> Mod ID: `keybindingtweaker`
> 前置条件: 无
> 导入: `import kbtwkr.keybinding.*;`、`import kbtwkr.event.*;`

KeyBindingTweaker 允许通过脚本注册自定义按键绑定，并检测按键状态。KeyBinding 类在客户端和服务端均可加载。

---

## API 列表

### 按键检测

> `import kbtwkr.keybinding.KeyBinding;`

对 `crafttweaker.player.IPlayer` 的扩展，用于在服务端检测按键绑定状态。仅对可同步（`createSyncable`）的按键绑定有效。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getPressedTimeServer(KeyBinding binding)` | `int` | 获取可同步按键绑定在服务端已按住的时间（tick） |
| `.isKeyDownServer(KeyBinding binding)` | `bool` | 检测可同步按键绑定在服务端是否被按住 |

### ConflictContext（冲突上下文）

> `import kbtwkr.keybinding.ConflictContext;`

定义按键绑定的使用上下文，绑定在其指定上下文之外不会触发。

#### 常量

| 常量 | 类型 | 说明 |
|------|------|------|
| `UNIVERSAL` | `IConflictContext` | 所有上下文均可触发 |
| `IN_GAME` | `IConflictContext` | 无 GUI 打开时可触发 |
| `GUI` | `IConflictContext` | 有 GUI 打开时可触发 |

---

### Modifier（修饰键）

> `import kbtwkr.keybinding.Modifier;`

定义按键绑定的修饰键。

#### 常量

| 常量 | 类型 | 说明 |
|------|------|------|
| `CONTROL` | `IModifier` | Ctrl 键 |
| `SHIFT` | `IModifier` | Shift 键 |
| `ALT` | `IModifier` | Alt 键 |
| `NONE` | `IModifier` | 无修饰键 |

---

### KeyBinding（按键绑定）

> `import kbtwkr.keybinding.KeyBinding;`

按键绑定类，与原版不同，此类在服务端也可加载。

#### 工厂方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `KeyBinding.createNormal(string descKey, IConflictContext ctx, IModifier mod, int keyCode, string categoryKey)` | `KeyBinding` | 创建普通按键绑定（不同步到服务端） |
| `KeyBinding.createSyncable(string descKey, IConflictContext ctx, IModifier mod, int keyCode, string categoryKey)` | `KeyBinding` | 创建可同步按键绑定（自动同步到服务端） |

参数说明：
- `descKey` — 按键描述的本地化键
- `ctx` — 冲突上下文（`ConflictContext`）
- `mod` — 修饰键（`Modifier`）
- `keyCode` — 按键码（参见 `Keys` 类）
- `categoryKey` — 分类的本地化键

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `shouldSync()` | `bool` | 是否应同步到服务端 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.isKeyDown()` | `bool` | 按键是否被按住（仅客户端有效，服务端始终返回 false） |
| `.isPressed()` | `bool` | 按键是否被按下（仅客户端有效，服务端始终返回 false） |

---

### KeyBindingRegisterEvent（按键绑定注册事件）

> `import kbtwkr.event.KeyBindingRegisterEvent;`

用于注册按键绑定的事件。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addKeyBinding(KeyBinding binding)` | `void` | 注册一个按键绑定实例 |

---

### EventManager（事件管理器）

> `import kbtwkr.event.EventManager;`

KeyBindingTweaker 的事件管理类。

#### 工厂方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `EventManager.getInstance()` | `EventManager` | 获取单例实例 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.onKeyBindingRegister(function<KeyBindingRegisterEvent> event)` | `void` | 添加按键绑定注册事件监听器 |
| `.clear()` | `void` | 清除所有事件监听器 |

---

### Keys（按键码常量）

> `import kbtwkr.keybinding.Keys;`

按键码参考类，所有常量类型为 `int`。

| 常量 | 常量 | 常量 |
|------|------|------|
| `KEY_NONE` | `KEY_ESCAPE` | `KEY_1` ~ `KEY_0` |
| `KEY_MINUS` | `KEY_EQUALS` | `KEY_BACK` |
| `KEY_TAB` | `KEY_Q` ~ `KEY_P` | `KEY_LBRACKET` |
| `KEY_RBRACKET` | `KEY_RETURN` | `KEY_LCONTROL` |
| `KEY_A` ~ `KEY_L` | `KEY_SEMICOLON` | `KEY_APOSTROPHE` |
| `KEY_GRAVE` | `KEY_LSHIFT` | `KEY_BACKSLASH` |
| `KEY_Z` ~ `KEY_M` | `KEY_COMMA` | `KEY_PERIOD` |
| `KEY_SLASH` | `KEY_RSHIFT` | `KEY_MULTIPLY` |
| `KEY_LMENU` / `KEY_LEFT_ALT` | `KEY_SPACE` | `KEY_CAPITAL` |
| `KEY_F1` ~ `KEY_F19` | `KEY_NUMLOCK` | `KEY_SCROLL` |
| `KEY_NUMPAD0` ~ `KEY_NUMPAD9` | `KEY_SUBTRACT` | `KEY_ADD` |
| `KEY_DECIMAL` | `KEY_NUMPADENTER` | `KEY_RCONTROL` |
| `KEY_DIVIDE` | `KEY_SYSRQ` | `KEY_RMENU` / `KEY_RIGHT_ALT` |
| `KEY_FUNCTION` | `KEY_PAUSE` | `KEY_HOME` |
| `KEY_UP` | `KEY_PRIOR` | `KEY_LEFT` |
| `KEY_RIGHT` | `KEY_END` | `KEY_DOWN` |
| `KEY_NEXT` | `KEY_INSERT` | `KEY_DELETE` |
| `KEY_CLEAR` | `KEY_LMETA` / `KEY_LWIN` | `KEY_RMETA` / `KEY_RWIN` |
| `KEY_APPS` | `KEY_POWER` | `KEY_SLEEP` |

---

## 使用示例

### 注册可同步按键绑定并检测

```zenscript
import kbtwkr.event.EventManager;
import kbtwkr.event.KeyBindingRegisterEvent;
import kbtwkr.keybinding.KeyBinding;
import kbtwkr.keybinding.ConflictContext;
import kbtwkr.keybinding.Modifier;
import kbtwkr.keybinding.Keys;

import crafttweaker.events.IEventManager;
import crafttweaker.event.PlayerTickEvent;
import crafttweaker.player.IPlayer;

// 创建可同步到服务端的按键绑定：Shift+X
val testKeyBinding as KeyBinding = KeyBinding.createSyncable(
    "test.key", ConflictContext.UNIVERSAL, Modifier.SHIFT, Keys.KEY_X, "test.category");

// 注册按键绑定
val manager as EventManager = EventManager.getInstance();
manager.onKeyBindingRegister(function(event as KeyBindingRegisterEvent) {
    event.addKeyBinding(testKeyBinding);
});

// 在玩家 Tick 中检测按键状态
events.onPlayerTick(function(event as PlayerTickEvent) {
    if (event.phase != "START") return;
    val player as IPlayer = event.player;
    if (event.side == "SERVER") {
        // 服务端检测（仅对可同步按键绑定有效）
        if (player.isKeyDownServer(testKeyBinding))
            player.sendChat("按键已按住 " ~ player.getPressedTimeServer(testKeyBinding) ~ " tick");
    } else {
        // 客户端检测
        if (testKeyBinding.isKeyDown())
            player.sendChat("按键在客户端被按住");
    }
});
```
