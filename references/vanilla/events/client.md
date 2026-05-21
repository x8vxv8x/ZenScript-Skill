# 客户端事件 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: EventTweaker
> 导入: `import mods.eventtweaker.event.*;`

客户端聊天、渲染覆盖层等客户端事件。

---

## API 列表

### ClientChatEvent（客户端聊天事件）

> `import mods.eventtweaker.event.ClientChatEvent;`

客户端收到聊天消息时触发。不可取消。

#### 事件注册

```zenscript
events.onClientChat(function(event as ClientChatEvent) {
    // 处理聊天消息
});
```

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `getMessage()` | `string` | 获取当前消息内容 |
| `getOriginalMessage()` | `string` | 获取原始消息内容 |

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `setMessage(message)` | `string` | 设置消息内容 |

### RenderGameOverlayEvent（渲染覆盖层事件）

> `import mods.eventtweaker.event.RenderGameOverlayEvent;`

渲染屏幕覆盖层时触发。不可取消。

#### 事件注册

```zenscript
events.onRenderGameOverlay(function(event as RenderGameOverlayEvent) {
    // 处理渲染覆盖层
});
```

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `getPartialTicks()` | `float` | 获取部分刻（插值值） |
