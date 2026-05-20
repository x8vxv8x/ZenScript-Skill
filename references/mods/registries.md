# Registries CraftTweaker API 参考

> Mod ID: `roidtweaker`
> 前置条件: Roids-Tweaker
> 导入: `import mods.roidtweaker.forge.Registries;`
> 配置要求: `mixin category.allowRemovingRegistries=true`

## API 列表

### Registries

> `import mods.roidtweaker.forge.Registries;`

允许黑名单注册表对象。改编自 StellarCore。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.disable(String registryName)` | void | 阻止 Forge 注册表注册指定 registryName 的条目 |

**注意事项：**
- 只能阻止注册条目添加，仅对加载后添加的条目生效
- 建议在 `#loader preinit` 或 `#loader contenttweaker` 中使用
- 谨慎使用，注意日志中的错误/崩溃
