# EverlastingAbilities CraftTweaker API 参考

> Mod ID: `everlastingabilities`
> 前置条件: EverlastingAbilities
> 导入: 见各章节

EverlastingAbilities 能力系统 API，用于自定义和管理玩家能力。

---

## CraftTweakerAdditions 扩展（需安装 CraftTweakerAdditions）

> `import mods.crtadd.everlastingabilities.AbilityTypeRegistry;`（EverlastingAbilities 原生 API）

### Functions（回调接口）

> `import mods.crtadd.everlastingabilities.onTick;`
> `import mods.crtadd.everlastingabilities.onChangedLevel;`

#### onTick 回调
```zenscript
import mods.crtadd.everlastingabilities.onTick;
function onPlayerTick(player as IPlayer, level as int) {
    // 玩家每 tick 的能力回调
}
```

#### onChangedLevel 回调
```zenscript
import mods.crtadd.everlastingabilities.onChangedLevel;
function onLevelChanged(player as IPlayer, oldLevel as int, newLevel as int) {
    // 玩家能力等级变化时的回调
}
```

---

### AbilitiesBuilder（能力构建器）

> `import mods.crtadd.everlastingabilities.AbilitiesBuilder;`

#### @ZenProperty
| 属性 | 类型 | 说明 |
|------|------|------|
| `translationKey` | string | 能力的翻译键（必填，如 "ability.abilities.everlastingabilities.speed.name" 可简写为 "speed"） |
| `unlocalizedDescription` | string | 能力的描述文本 |
| `rarity` | int | 能力的稀有度（数值越高越稀有） |
| `maxLevel` | int | 能力的最大等级 |
| `baseXpPerLevel` | int | 每级所需的基础经验值 |
| `onTick` | onTick | 每 tick 回调函数 |
| `onChangedLevel` | onChangedLevel | 等级变化回调函数 |

#### 能力构建方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(String translationKey)` | AbilitiesBuilder | 创建能力构建器实例 |
| `.register()` | void | 注册能力到 EverlastingAbilities |

---

### IPlayerAbilites（IPlayer 扩展）

#### @ZenGetter
| 属性 | 类型 | 说明 |
|------|------|------|
| `getPlayerAbiliteCount` | int | 获取玩家拥有的能力总数 |

#### 能力管理方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.hasAbilites(String abilitesname)` | bool | 检查玩家是否拥有指定能力（能力名不带前缀，如 "speed"） |
| `.getAbilitesLevel(String abilitesname)` | int | 获取玩家指定能力的等级，未拥有则返回 0 |
| `.addAbilites(String abilitesname, int level, boolean modifyXp)` | void | 向玩家添加能力，modifyXp 为是否修改经验值 |
| `.removeAbilites(String abilitesname, int level, boolean modifyXp)` | void | 移除玩家指定能力，modifyXp 为是否修改经验值 |

---

## 使用示例

```zenscript
import mods.crtadd.everlastingabilities.AbilitiesBuilder;
import mods.crtadd.everlastingabilities.onChangedLevel;

// 创建自定义能力
val myAbility = AbilitiesBuilder.create("mymod.myability");
myAbility.rarity = 1;
myAbility.maxLevel = 5;
myAbility.baseXpPerLevel = 100;
myAbility.unlocalizedDescription = "我的自定义能力";
myAbility.onChangedLevel = function(player as IPlayer, oldLevel as int, newLevel as int) {
    print(player.name ~ " 的能力从 " ~ oldLevel ~ " 级提升到 " ~ newLevel ~ " 级！");
};
myAbility.register();

// 为玩家添加能力
player.addAbilites("mymod.myability", 3, false);

// 检查能力等级
if (player.hasAbilites("mymod.myability")) {
    val level = player.getAbilitesLevel("mymod.myability");
    print("当前等级: " ~ level);
}
```

---

## 常见错误

| 错误 | 原因 | 修复 |
|------|------|------|
| 能力名称找不到 | 使用了完整的能力名称（如带 "ability.abilities.everlastingabilities." 前缀） | 使用简化名称，如 "speed" 而不是 "ability.abilities.everlastingabilities.speed.name" |
| `AbilitiesBuilder.register()` 无效 | 能力 ID 格式不正确或已存在同名能力 | 使用唯一的 translationKey，检查是否与其他能力冲突 |

---

## 注意事项

- **能力 ID 格式**：EverlastingAbilities 的能力名称不带前缀，直接使用简化名称（如 "speed"、"jump"）
- **经验值参数**：`addAbilites` 和 `removeAbilites` 的 `modifyXp` 参数控制是否同时修改玩家的经验值池
