# Blood Arsenal CraftTweaker API 参考

> Mod ID: `bloodarsenal`
> 前置条件: MoreTweaker
> 导入: `import moretweaker.bloodarsenal.*;`

## API 列表

### Sanguine（血之祭坛）

> `import moretweaker.bloodarsenal.Sanguine;`

#### 配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, int lpCost, IItemStack catalyst, IIngredient[] inputs)` | void | 添加灌注配方。`lpCost` 为 LP 消耗，`catalyst` 为催化剂 |
| `.removeRecipe(IIngredient output)` | void | 按输出移除配方 |
| `.addModifier(String modifier, int lpCost, IIngredient[] inputs)` | void | 添加修饰符。输入材料数量会乘以应用的等级 |
| `.removeModifier(String modifier)` | void | 移除修饰符 |
| `.removeAll()` | void | 移除所有配方和修饰符 |

#### 修饰符字段

修饰符名称存储在 `Sanguine` 类的字段中：

| 字段 | 说明 |
|------|------|
| `Sanguine.BAD_POTION` | 负面药水 |
| `Sanguine.BLOOD_LUST` | 嗜血 |
| `Sanguine.FLAME` | 火焰 |
| `Sanguine.SHARPNESS` | 锋利 |
| `Sanguine.FORTUNATE` | 时运 |
| `Sanguine.LOOTING` | 抢夺 |
| `Sanguine.SILKY` | 精准采集 |
| `Sanguine.SMELTING` | 熔炼 |
| `Sanguine.EXPERIENCED` | 经验 |
| `Sanguine.BENEFICIAL_POTION` | 正面药水 |
| `Sanguine.QUICK_DRAW` | 快速拉弓 |
| `Sanguine.SHADOW_TOOL` | 暗影工具 |
| `Sanguine.AOD` | AOD |
| `Sanguine.SIGIL` | 印记 |
