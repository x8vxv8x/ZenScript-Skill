# 游戏内commands

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: 无需导入

Crafttweaker 内置的游戏内命令

---

## CT 命令

命令前缀：`/ct`

| 命令 | 用途 |
|------|------|
| `/ct help` | 查看指令帮助 |
| `/ct hand` | 打印手中物品 ID 和矿辞，复制到剪贴板 |
| `/ct syntax` | 检查脚本语法错误（不会应用更改，需重启） |
| `/ct conflict` | 打印冲突配方到日志（需客户端安装 JEI） |
| `/ct inventory` | 打印物品栏所有物品 ID 到日志 |
| `/ct liquids` | 打印所有流体信息到日志 |
| `/ct seeds` | 打印打草掉落物及权重到日志 |
| `/ct docs` / `/ct wiki` | 打开 CrT wiki |
| `/ct biomes` | 列出所有生物群系 |
| `/ct biomeTypes` | 列出所有生物群系类型 |
| `/ct blockinfo` | 激活/停用方块读取器（右键方块显示名称、Meta、TileEntity 数据） |
| `/ct blocks` | 输出所有方块到日志 |
| `/ct bugs` | 打开 GitHub 问题追踪器 |
| `/ct discord` | 打开 Discord 服务器链接 |
| `/ct dumpzs` | 输出 ZenScript dump 到 minecraft 目录（支持 log/html/json） |
| `/ct entities` | 输出所有实体到日志 |
| `/ct give <item>` | 给予物品（支持 CrT 括号语法和 `.withTag()`） |
| `/ct json` / `/ct json escaped` | 打印手中物品 NBT 为 JSON（可点击复制） |
| `/ct log` | 发送可点击链接打开 crafttweaker.log |
| `/ct mods` | 输出所有 mod 及版本到日志和聊天 |
| `/ct names [category]` | 输出所有物品到日志（可选 category：burntime/creativetabs/damageable/display/enchantability/foodvalue/maxdamage/maxstack/maxuse/modid/rarity/repairable/repaircost/saturationvalue/unloc） |
| `/ct nbt` | 输出所看方块或手持物品的 NBT 到日志 |
| `/ct oredict [name]` | 输出所有矿辞条目到日志（指定名称则输出该矿辞的物品） |
| `/ct potions` | 输出所有药水到日志 |
| `/ct recipeNames [modid]` | 输出所有配方名到日志（可选 modid 过滤） |
| `/ct recipes` | 输出所有工作台配方到日志 |
| `/ct recipes hand` | 输出手中物品的所有配方到日志 |
| `/ct recipes furnace` | 输出所有熔炉配方到日志 |
| `/ct scripts` | 发送可点击链接打开脚本目录 |
| `/ct zslint` | 启动 zslint socket |

---