# Raw Logger CraftTweaker API 参考

> Mod ID: `ctintegration`
> 前置条件: CraftTweaker Integration
> 导入: `import mods.ctintegration.util.RawLogger;`

将原始字符串写入日志文件，用于测试和文档记录。日志位于实例文件夹的 `crafttweaker_raw.log`，每次启动游戏时清空。

## API 列表

### RawLogger

> `import mods.ctintegration.util.RawLogger;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.logRaw(String message)` | void | 将字符串写入原始日志文件 |
