# Arcane Archives CraftTweaker API 参考

> Mod ID: `arcanearchives`
> 前置条件: 无
> 导入: `import mods.arcanearchives.GCT;`

## API 列表

### GCT（宝石切割台）

> `import mods.arcanearchives.GCT;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String name, IItemStack output, IIngredient[] inputs)` | void | 添加 GCT 配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方（数量必须匹配） |
| `.replaceRecipe(String name, IItemStack output, IIngredient[] inputs)` | void | 替换已有配方（不打乱 GCT 界面顺序） |

**参数说明：**
- `name`：配方名称（必须已存在）
- `output`：输出物品
- `inputs`：输入材料数组

## 使用示例

### 示例一：GCT 配方操作

```zenscript
import mods.arcanearchives.GCT;

// 移除光辉粉尘配方
GCT.removeRecipe(<arcanearchives:radiant_dust> * 2);

// 添加新配方：燧石 + 原始石英 = 光辉粉尘
GCT.addRecipe("radiant_dust", <arcanearchives:radiant_dust> * 2, [<minecraft:flint>, <arcanearchives:raw_quartz>]);

// 替换已有配方（不打乱界面顺序）
GCT.replaceRecipe("shaped_quartz", <arcanearchives:shaped_quartz>, [<arcanearchives:raw_quartz> * 10]);
```

## 注意事项

- `removeRecipe` 的输出物品数量必须与原配方完全匹配
- `replaceRecipe` 用于替换已有配方，不会打乱 GCT 界面中的配方顺序
- 配方名称在 `addRecipe` 和 `replaceRecipe` 中用于标识配方
