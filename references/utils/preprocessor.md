# 预处理器

必须放在脚本最顶部（import 之前）。

| 预处理器 | 说明 |
|---------|------|
| `#priority <数字>` | 加载优先级（越大越先加载） |
| `#modloaded <modID>` | mod 加载时才执行（支持 `!` 取反） |
| `#loader <loaderName>` | 指定加载器（默认 `crafttweaker`） |
| `#sideonly <side>` | 只在 client 或 server 执行 |
| `#debug` | 输出编译的 class 文件 |
| `#ignoreBracketErrors` | 忽略尖括号错误 |
| `#norun` | 不执行脚本（仍检查语法） |
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
