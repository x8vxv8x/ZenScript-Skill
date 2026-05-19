# Chisel CraftTweaker API 参考

> Mod ID: `chisel`
> 前置条件: Modtweaker
> 导入: `import mods.chisel.Carving;`

## API 列表

### Carving（雕刻）

> `import mods.chisel.Carving;`

#### 配方添加方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGroup(String name)` | void | 创建新的雕刻变体组 |
| `.addVariation(String groupName, IItemStack stack)` | void | 向指定组添加变体方块 |

#### 配方移除方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeGroup(String name)` | void | 移除整个雕刻变体组 |
| `.removeVariation(String groupName, IItemStack stack)` | void | 从指定组移除变体方块 |

## 使用示例

### 添加雕刻变体组

```zenscript
import mods.chisel.Carving;

// 创建新组并添加变体
Carving.addGroup("test");
Carving.addVariation("test", <minecraft:stone>);
```

### 移除雕刻变体

```zenscript
import mods.chisel.Carving;

// 获取组名可运行 /ct chiselGroups
Carving.removeVariation("test", <minecraft:stone>);
```

## 注意事项

- 可通过 `/ct chiselGroups` 命令查看所有已注册的雕刻组名
