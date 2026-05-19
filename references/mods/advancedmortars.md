# Advanced Mortars CraftTweaker API 参考

> Mod ID: `advancedmortars`
> 前置条件: 无
> 导入: `import mods.advancedmortars.Mortar;`

## API 列表

### Mortar

> `import mods.advancedmortars.Mortar;`

#### 添加配方方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(String[] mortarTypes, IItemStack output, int duration, IIngredient[] inputs)` | void | 添加研磨配方 |

**参数说明：**
- `mortarTypes`：研磨器类型数组，可选值：`"wood"`, `"stone"`, `"iron"`, `"diamond"`
- `output`：输出物品
- `duration`：研磨所需次数/时间
- `inputs`：输入材料数组

## 使用示例

### 示例一：粉碎配方

```zenscript
import mods.advancedmortars.Mortar;

// 骨头研磨成骨粉
Mortar.addRecipe(["wood", "stone", "iron", "diamond"], <minecraft:dye:15> * 4, 8, [<minecraft:bone>]);

// 花朵研磨成染料
Mortar.addRecipe(["wood", "stone", "iron", "diamond"], <minecraft:dye:10> * 2, 8, [<botania:flower:5>]);
```

### 示例二：混合配方

```zenscript
import mods.advancedmortars.Mortar;

// 混合染料
Mortar.addRecipe(["wood", "stone", "iron", "diamond"], <minecraft:dye:7> * 2, 4, [<ore:dyeBlack>, <ore:dyeWhite>]);
Mortar.addRecipe(["wood", "stone", "iron", "diamond"], <minecraft:dye:5> * 2, 4, [<ore:dyeRed>, <ore:dyeBlue>]);
```

## 注意事项

- 支持的研磨器类型：木制（wood）、石制（stone）、铁制（iron）、钻石（diamond）
- 输入参数使用数组形式，支持多个输入材料
- 支持矿辞（ore dictionary）作为输入
