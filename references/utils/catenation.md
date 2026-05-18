# Catenation（链式操作）CraftTweaker API 参考

> Mod ID: 无
> 前置条件: ZenUtils
> 导入: `import mods.zenutils.Catenation;`

Catenation 提供延迟执行和链式操作机制，通过 `game.catenation()` 创建。

---

## API 列表

### Catenation（链式操作）

> `import mods.zenutils.Catenation;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `game.catenation()` | Catenation | 创建新的链式操作 |
| `action(function)` | Catenation | 添加执行动作 |
| `delay(int)` | Catenation | 延迟指定 tick |
| `repeat(int)` | Catenation | 重复执行指定次数 |
| `then(function)` | Catenation | 链式执行下一个动作 |
| `start()` | void | 启动链式操作 |
| `stop()` | void | 停止链式操作 |
