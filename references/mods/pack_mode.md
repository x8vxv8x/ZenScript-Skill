# Pack Mode CraftTweaker API 参考

> Mod ID: `packmode`
> 前置条件: 安装 packmode 模组
> 导入: 无需导入（使用预处理器指令）

## 预处理器

### #packmode

在脚本文件顶部添加 `#packmode` 预处理器指令，使该脚本仅在指定的包模式下执行。

#### 语法

```zenscript
#packmode <模式名称> [模式名称2] [模式名称3] ...
```

- 可以同时指定多个模式，用空格分隔
- 脚本仅在匹配的模式下执行
- 需要在 `packmode.cfg` 配置文件中设置当前模式
- **修改模式后需要完全重启游戏才能生效**

#### 使用示例

```zenscript
#packmode normal
import crafttweaker.items.IItemStack;

print("如果这条消息出现在 CT 日志中，说明当前模式为 normal！");
```

```zenscript
#packmode normal expert
// 此脚本在 normal 和 expert 模式下都会执行
```

## 命令

### /packmode

在游戏内切换包模式。

```
/packmode <新模式名称>
```

- 切换后需要重启游戏才能生效
