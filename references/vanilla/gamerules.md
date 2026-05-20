# Gamerules CraftTweaker API 参考

> Mod ID: `ctutils`
> 前置条件: 无
> 导入: `import mods.ctutils.world.IGameRules;`

游戏规则操作。IGameRules 对象包含所有游戏规则信息。

## API 列表

### IGameRules

> `import mods.ctutils.world.IGameRules;`

通过 `IWorld.getGameRules()` 获取。

#### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getBoolean(String name)` | name | bool | 获取布尔游戏规则 |
| `.getString(String name)` | name | string | 获取字符串游戏规则 |
| `.getInt(String name)` | name | int | 获取整数游戏规则 |
| `.hasRule(String name)` | name | bool | 检查规则是否存在 |
| `.getRules()` | 无 | List | 获取所有规则名称 |
| `.addGameRule(String key, String value, String type)` | key, value, type | void | 添加游戏规则 |
| `.setOrCreateGameRule(String key, String value)` | key, value | void | 设置规则值，不存在则创建（类型为 any） |
