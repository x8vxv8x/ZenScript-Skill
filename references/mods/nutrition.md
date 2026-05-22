# Nutrition CraftTweaker API 参考

> Mod ID: `nutrition`
> 前置条件: Nutrition
> 导入: 无（使用扩展方法，无需 import）

Nutrition 营养系统 API，用于查询和设置玩家营养值。

---

## CraftTweakerAdditions 扩展（需安装 CraftTweakerAdditions）

### IPlayerNutrition（IPlayer 扩展）

> 无需额外 import，通过 `player.方法()` 调用

#### 营养值方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.getNutrition(String nutritionname)` | float | 获取玩家指定营养的值（营养名由 Nutrition 模组定义），仅客户端有效 |
| `.setNutrition(String nutritionname, float nutritionfloat)` | void | 设置玩家指定营养的值，仅客户端有效 |

---

### IPlayerNutrition（IPlayer 扩展）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getNutrition(String nutritionname)` | float | 获取玩家指定营养的值（营养名由 Nutrition 模组定义），仅客户端有效 |
| `.setNutrition(String nutritionname, float nutritionfloat)` | void | 设置玩家指定营养的值，仅客户端有效 |

---

## 使用示例

```zenscript
// 获取营养值
val fruits = player.getNutrition("fruits");
print("水果营养值: " ~ fruits);

// 设置营养值
player.setNutrition("fruits", 10.0);
```
---

## 注意事项

- **客户端限制**：营养值操作仅在客户端有效，在服务器端脚本中使用会无效或返回默认值
