# 预处理器 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: 无需导入

预处理器指令，必须放在脚本最顶部（import 之前）。

---

## 预处理器列表

### CraftTweaker 预处理器

| 预处理器 | 说明 |
|---------|------|
| `#priority <数字>` | 加载优先级（越大越先加载） |
| `#modloaded <modID>` | mod 加载时才执行（支持 `!` 取反） |
| `#loader <loaderName>` | 指定加载器（默认 `crafttweaker`） |
| `#sideonly <side>` | 只在 client 或 server 执行 |
| `#debug` | 输出编译的 class 文件 |
| `#ignoreBracketErrors` | 忽略尖括号错误 |
| `#norun` | 不执行脚本（仍检查语法） |
| `#nowarn` | 警告只写日志（不影响错误） |
| `#ikwid` | 警告和错误只写日志 |
| `#profile` | 日志打印配方修改耗时 |
| `#disable_search_tree` | 禁用配方表重算（加速加载） |

```zenscript
#priority 100
#modloaded thermalfoundation
#modloaded !ic2
import crafttweaker.item.IItemStack;
// ...
```

### ZenUtils 预处理器（需安装 ZenUtils）

#### #suppress

> 版本要求: 1.5.0+

| 指令 | 说明 |
|------|------|
| `#suppress warning` / `#suppress warnings` | 抑制当前脚本的警告 |
| `#suppress error` / `#suppress errors` / `#suppress all` | 抑制当前脚本的警告和错误 |

解析错误仍会显示，错误仍会记录到 `crafttweaker.log`。使用后 `#ikwid` 和 `#nowarn` 失效。

#### #hardfail

> 版本要求: 1.6.6+

| 指令 | 说明 |
|------|------|
| `#hardfail` | 脚本产生未被 `#suppress` 抑制的错误时使游戏崩溃 |
