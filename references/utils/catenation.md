# Catenation（链式操作）

> 需安装 ZenUtils
> 导入: `import mods.zenutils.Catenation;`

Catenation 提供延迟执行和链式操作机制，通过 `game.catenation()` 创建。

---

## 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `game.catenation()` | 无 | Catenation | 创建新的链式操作 |
| `action(function)` | 函数 | Catenation | 添加执行动作 |
| `delay(int)` | int（tick数） | Catenation | 延迟指定 tick |
| `repeat(int)` | int（次数） | Catenation | 重复执行指定次数 |
| `then(function)` | 函数 | Catenation | 链式执行下一个动作 |
| `start()` | 无 | void | 启动链式操作 |
| `stop()` | 无 | void | 停止链式操作 |
