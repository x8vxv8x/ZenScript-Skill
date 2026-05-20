# Catenation（链式操作）CraftTweaker API 参考

> Mod ID: 无
> 前置条件: ZenUtils（版本要求: 1.11.0+）
> 导入: `import mods.zenutils.Catenation;`、`import mods.zenutils.CatenationContext;`、`import mods.zenutils.CatenationStatus;`、`import mods.zenutils.ICatenationBuilder;`

Catenation 提供延迟执行和链式操作机制，通过 `world.catenation()` 创建。Catenation 不会被序列化，服务器停止时所有 catenation 会终止。

---

## API 列表

### ICatenationBuilder（链式构建器）

> `import mods.zenutils.ICatenationBuilder;`

通过 `world.catenation()` 创建。所有方法返回构建器本身以支持链式调用。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.run(IWorldFunction)` | ICatenationBuilder | 立即执行函数 |
| `.sleep(long ticks)` | ICatenationBuilder | 等待指定 tick |
| `.sleepUntil(IWorldCondition)` | ICatenationBuilder | 等待直到条件满足 |
| `.stopWhen(IWorldCondition)` | ICatenationBuilder | 条件满足时停止（后续任务不再执行） |
| `.then(IWorldFunction)` | ICatenationBuilder | 等同于 `run`，链式执行下一个动作 |
| `.onStop(IWorldFunction)` | ICatenationBuilder | 停止时执行的回调（@since 1.12.7） |
| `.start()` | Catenation | 构建并启动 catenation |

### Catenation（链式操作对象）

> `import mods.zenutils.Catenation;`

由 `ICatenationBuilder.start()` 返回。可保存到变量手动控制。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `stopped` | bool | 是否已停止 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.stop()` | void | 停止 catenation |
| `.isStopped()` | bool | 检查是否已停止 |
| `.pause()` | void | 暂停 catenation（@since 1.12.8） |
| `.play()` | void | 恢复已暂停的 catenation（@since 1.12.8） |

### CatenationContext（上下文数据）

> `import mods.zenutils.CatenationContext;`

catenation 任务间共享的数据持有者。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `data` | IData | 共享数据（可读写） |
| `status` | CatenationStatus | 当前状态 |
| `catenation` | Catenation | 关联的 catenation 对象 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getData()` | IData | 获取共享数据 |
| `.setData(IData)` | void | 设置共享数据 |
| `.hasData()` | bool | 检查是否有自定义数据 |
| `.stop()` | void | 停止 catenation |

### CatenationStatus（状态枚举）

> `import mods.zenutils.CatenationStatus;`

@since 1.12.7

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | String | 状态名（全大写） |
| `isStop` | bool | 是否为停止状态 |

#### 枚举值

| 方法 | 说明 |
|------|------|
| `CatenationStatus.working()` | 正在运行 |
| `CatenationStatus.pause()` | 已暂停 |
| `CatenationStatus.finish()` | 所有任务完成 |
| `CatenationStatus.stopManual()` | 被 `stop()` 手动停止 |
| `CatenationStatus.stopInternal()` | 被 `stopWhen` 函数停止 |
| `CatenationStatus.error()` | 任务或 stopWhen 函数抛出异常 |
| `CatenationStatus.unload()` | 关联世界卸载（如服务器关闭） |
| `CatenationStatus.serial()` | 等待序列化（@since 1.13.0） |

支持 `==` 运算符比较。

### 函数式接口

#### IWorldFunction

> `import mods.zenutils.IWorldFunction;`

catenation 任务函数，参数依次为：
- `IWorld world`：执行 catenation 的世界
- `CatenationContext context`：共享数据持有者

无返回值。

#### IWorldCondition

> `import mods.zenutils.IWorldCondition;`

catenation 条件函数，参数与 IWorldFunction 相同，返回 `bool`。

---

## 使用示例

### 基础链式操作

```zenscript
events.onPlayerLoggedIn(function(event as PlayerLoggedInEvent) {
    val player as IPlayer = event.player;
    if (event.player.world.remote) return;
    event.player.world.catenation()
        .run(function(world, context) {
            print("catenation 开始");
            context.data = world.time;
        })
        .sleep(200)
        .then(function(world, context) {
            player.sendMessage("登录后 10 秒显示此消息");
            player.sendMessage("登录时世界时间: " ~ context.data.asString());
        })
        .sleepUntil(function(world, context) {
            return world.raining;
        })
        .then(function(world, context) {
            player.sendMessage("下雨了！");
        })
        .stopWhen(function(world, context) {
            return !player.alive;
        })
        .onStop(function(world, context) {
            print(context.status.name);
        })
        .start();
});
```

### 手动控制

```zenscript
val catenation = world.catenation()
    .sleep(100)
    .then(function(world, context) {
        print("完成");
    })
    .start();

// 手动停止
catenation.stop();

// 检查状态
print(catenation.stopped);
```

---

## PersistedCatenation（持久化链式操作）

> `import mods.zenutils.CatenationPersistence;`

@since 1.13.0

持久化 catenation 可被序列化，服务器重启后自动恢复。

### 创建持久化 catenation

在脚本加载阶段调用（可重载）：

```zenscript
mods.zenutils.CatenationPersistence.registerPersistedCatenation("sendMessage")
    .setCatenationFactory(function(world) {
        return world.catenation()
            .sleep(200)
            .then(function(world, context) {
                context.getPlayer().sendMessage(context.getPersistedData().asString());
            })
            .start();
    })
    .addPlayerHolder()
    .addDataHolder()
    .register();
```

### 启动持久化 catenation

在事件中调用：

```zenscript
events.onPlayerLoggedIn(function(event as PlayerLoggedInEvent) {
    val world = event.player.world;
    if (!world.remote) {
        mods.zenutils.CatenationPersistence.startPersistedCatenation("sendMessage", world)
            .withPlayer(event.player)
            .withData("test")
            .start();
    }
});
```

或使用 world 扩展方法：`world.persistedCatenation(String key)`

### 可序列化对象

| 类型 | 构建器方法 | 上下文访问 | 启动器方法 | 就绪条件 | 默认键名 |
|------|-----------|-----------|-----------|---------|---------|
| IPlayer | `addPlayerHolder(key)` | `getPlayer(key)` | `withPlayer(player, key)` | 玩家在世界中 | `"player"` |
| IEntity | `addEntityHolder(key)` | `getEntity(key)` | `withEntity(entity, key)` | 实体存活 | `"entity"` |
| IBlockPos | `addPositionHolder(key)` | `getPosition(key)` | `withPosition(pos, key)` | 位置所在区块已加载 | `"pos"` |
| IData | `addDataHolder(key)` | `getPersistedData(key)` | `withData(data, key)` | 始终就绪 | `"data"` |
