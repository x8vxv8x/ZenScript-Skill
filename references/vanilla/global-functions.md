# Global Functions

全局函数是无需 import 即可直接使用的函数。

## 函数列表

### print

```zenscript
print("Hello World!");
```

将字符串打印到 CraftTweaker 日志。无返回值。

### isNull

```zenscript
isNull(<minecraft:dirt>);
```

检查给定对象是否为 null。返回 bool。不适用于基本类型。

注意：如果不起作用，尝试将对象转换为 bool：`<minecraft:dirt> as bool`

### instanceof

```zenscript
entity instanceof IEntity;
```

检查对象是否为指定类型的实例。返回 bool。

### max

```zenscript
max(10, 11);  // 返回 11
```

返回两个 int 中较大的数。

### min

```zenscript
min(10, 11);  // 返回 10
```

返回两个 int 中较小的数。

### pow

```zenscript
pow(2.0, 4.0);  // 返回 16.0
```

计算幂运算。返回 double。

### totalActions

```zenscript
totalActions();
```

返回已注册的全局函数数量。返回 int。

### enableDebug

```zenscript
enableDebug();
```

启用调试模式。推荐使用 Debug 预处理器替代。

## 全局字段

以下字段无需 import 即可直接使用：

| 字段 | 类型 | 说明 |
|------|------|------|
| `recipes` | IRecipeManager | 工作台配方管理 |
| `furnace` | IFurnaceManager | 熔炉配方管理 |
| `brewing` | IBrewingManager | 酿造台管理 |
| `game` | IGame | 游戏相关函数 |
| `server` | IServer | 服务器相关 |
| `client` | IClient | 客户端相关（仅客户端可用） |
| `events` | IEventManager | 事件管理 |
| `format` | IFormatter | 格式化处理 |
| `itemUtils` | IItemUtils | 物品工具 |
| `loadedMods` | ILoadedMods | 已加载 mod 列表 |
| `logger` | ILogger | 日志工具 |
| `oreDict` | IOreDict | 矿物词典管理 |
| `vanilla` | IVanilla | 原版函数（如 seeds） |
