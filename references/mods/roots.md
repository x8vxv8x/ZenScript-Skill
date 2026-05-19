# Roots 3 CraftTweaker API 参考

> Mod ID: `roots`
> 前置条件: 无
> 导入: `import mods.roots.<ClassName>;`

## API 列表

### Rituals（仪式管理器）

> `import mods.roots.Rituals;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.modifyRitual(string name, IIngredient[] inputs)` | void | 修改指定仪式的材料（必须恰好 5 个） |
| `.getRitual(string ritualName)` | Ritual | 获取仪式对象以修改其属性（名称不以 `ritual_` 开头时会自动添加） |

```zenscript
import mods.roots.Rituals;

// 修改风墙仪式的材料
Rituals.modifyRitual("ritual_windwall", [<minecraft:feather>, <minecraft:flint_and_steel>.anyDamage().transformDamage(1), <roots:cloud_berry>, <roots:cloud_berry>, <minecraft:web>]);
```

### Ritual（仪式属性）

> `import mods.roots.Ritual;`

用于修改仪式的属性值。所有设置方法返回 Ritual 对象，支持链式调用。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setDouble(string propertyName, double value)` | Ritual | 设置 double 类型属性 |
| `.setFloat(string propertyName, float value)` | Ritual | 设置 float 类型属性 |
| `.setInteger(string propertyName, int value)` | Ritual | 设置 int 类型属性 |
| `.setDuration(int value)` | Ritual | 设置仪式持续时间（等同于 `setInteger("duration", value)`） |
| `.setString(string propertyName, string value)` | Ritual | 设置 string 类型属性 |

```zenscript
import mods.roots.Rituals;
import mods.roots.Ritual;

var animal_harvest = Rituals.getRitual("animal_harvest") as Ritual;
animal_harvest.setInteger("count", 10);          // 每次操作 10 次收割（默认 5）
animal_harvest.setInteger("interval", 220);       // 间隔 220 tick（默认 110）
animal_harvest.setFloat("looting_chance", 1);     // 掠夺概率 100%（默认 0.16）
animal_harvest.setInteger("radius_x", 30);
animal_harvest.setInteger("radius_z", 30);
animal_harvest.setInteger("radius_y", 30);        // 半径设为 30
```

- 使用 `/roots rituals` 命令查看所有仪式属性及其默认值（输出到 `roots.log`）

### Spells（法术管理器）

> `import mods.roots.Spells;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getSpell(string spellName)` | Spell | 获取法术对象以修改其属性（名称不以 `spell_` 开头时会自动添加） |

### Spell（法术属性）

> `import mods.roots.Spell;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setDouble(string propertyName, double value)` | Spell | 设置 double 类型属性 |
| `.setFloat(string propertyName, float value)` | Spell | 设置 float 类型属性 |
| `.setInteger(string propertyName, int value)` | Spell | 设置 int 类型属性 |
| `.setString(string propertyName, string value)` | Spell | 设置 string 类型属性 |
| `.setCooldown(int value)` | Spell | 设置法术冷却时间（tick） |
| `.setDamage(float value)` | Spell | 设置法术伤害（法术必须有 damage 属性） |
| `.setCost(Herb herb, double amount)` | Spell | 修改指定草药的消耗（只能修改已有消耗） |
| `.setModifierCost(Cost cost, Herb herb, double amount)` | Spell | 修改修饰器的消耗（只能修改已有消耗） |

```zenscript
import mods.roots.Spells;
import mods.roots.Spell;
import mods.roots.Costs;
import mods.roots.Herbs;

var harvest = Spells.getSpell("harvest") as Spell;
harvest.setCooldown(800);                         // 冷却 40 秒
harvest.setCost(Herbs.wildewheet, 1.25);          // 增加野麦草消耗
harvest.setModifierCost(Costs.additional_cost, Herbs.wildroot, 0.9);  // 增加修饰器消耗
harvest.setInteger("radius_x", 20);
harvest.setInteger("radius_z", 20);
harvest.setInteger("radius_y", 20);               // 半径设为 20
```

- 使用 `/roots spells` 命令查看所有法术属性及其默认值（输出到 `roots.log`）

### Herbs（草药常量）

> `import mods.roots.Herbs;`

#### 静态属性

| 属性 | 说明 |
|------|------|
| `Herbs.wildroot` | 野根草 |
| `Herbs.terra_moss` | 大地苔藓 |
| `Herbs.infernal_bulb` | 地狱球茎 |
| `Herbs.dewgonia` | 露水藻 |
| `Herbs.stalicripe` | 石笋草 |
| `Herbs.cloud_berry` | 云莓 |
| `Herbs.baffle_cap` | 迷惑菇 |
| `Herbs.pereskia` | 仙人掌花 |
| `Herbs.spirit_herb` | 灵魂草 |
| `Herbs.wildewheet` | 野麦草 |
| `Herbs.moonglow_leaf` | 月光叶 |

- 用于 `Spell.setCost()` 的参数

### Costs（消耗类型常量）

> `import mods.roots.Costs;`

#### 静态属性

| 属性 | 说明 |
|------|------|
| `Costs.no_cost` | 无消耗 |
| `Costs.additional_cost` | 额外消耗 |
| `Costs.all_cost_multiplier` | 修改所有现有消耗的倍率 |
| `Costs.specific_cost_adjustment` | 调整特定消耗 |
| `Costs.specific_cost_multiplier` | 乘以特定消耗的倍率 |

- 用于 `Spell.setModifierCost()` 的参数

### Pyre（柴堆）

> `import mods.roots.Pyre;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(string name, IItemStack output, IIngredient[] inputs)` | void | 添加合成配方（5 个材料） |
| `.addRecipe(string name, IItemStack output, IIngredient[] inputs, int xp)` | void | 添加合成配方（带经验值奖励） |
| `.removeRecipe(IItemStack output)` | void | 根据输出移除配方（不比较数量） |

- 替换已有配方时，确保使用相同的名称以保持 Patchouli 兼容

```zenscript
import mods.roots.Pyre;

Pyre.removeRecipe(<roots:stalicripe>);

Pyre.addRecipe("stalicripe", <roots:stalicripe> * 64, [<minecraft:diamond_block>, <minecraft:flint_and_steel>.anyDamage().transformDamage(1), <minecraft:iron_block>, <minecraft:emerald_block>, <minecraft:deadbush>]);

Pyre.addRecipe("stalicripe2", <roots:stalicripe> * 64, [<minecraft:diamond_block>, <minecraft:gold_block>, <minecraft:iron_block>, <minecraft:emerald_block>, <minecraft:deadbush>], 30);
```

### Fey（精灵工匠台）

> `import mods.roots.Fey;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(string name, IItemStack output, IIngredient[] inputs)` | void | 添加合成配方（5 个材料） |
| `.addRecipe(string name, IItemStack output, IIngredient[] inputs, int xp)` | void | 添加合成配方（带经验值奖励） |
| `.removeRecipe(IItemStack output)` | void | 根据输出移除配方 |

- 替换已有配方时，确保使用相同的名称以保持 Patchouli 兼容

```zenscript
import mods.roots.Fey;

Fey.addRecipe("tnt", <minecraft:tnt>, [<minecraft:gunpowder>, <minecraft:gunpowder>, <minecraft:gunpowder>, <minecraft:gunpowder>, <minecraft:wool:14>]);

Fey.removeRecipe(<roots:living_axe>);

Fey.addRecipe("living_axe", <roots:living_axe>, [<minecraft:sand>, <minecraft:dirt>, <minecraft:stone>, <minecraft:glass>, <minecraft:stone_axe>]);
```

### Mortar（研钵合成）

> `import mods.roots.Mortar;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(string name, IItemStack output, IIngredient[] inputs)` | void | 添加研钵配方。数组长度为 5 时生成单个配方；长度为 1 时自动生成 5 个递增配方 |
| `.changeSpell(string spellName, IIngredient[] inputs)` | void | 修改法术的研钵配方（必须 5 个材料） |
| `.removeRecipe(IItemStack output)` | void | 根据输出移除配方（不比较数量，包括多材料配方） |

```zenscript
import mods.roots.Mortar;

// 单材料配方：自动生成 5 个递增版本
Mortar.addRecipe("gunpowder_from_flint", <minecraft:gunpowder>, [<minecraft:flint>]);

// 五材料配方
Mortar.addRecipe("bed_from_wool_planks", <minecraft:bed>, [<minecraft:wool>, <minecraft:wool>, <minecraft:planks>, <minecraft:planks>, <minecraft:planks>]);

Mortar.removeRecipe(<roots:flour>);

Mortar.changeSpell("spell_harvest", [<minecraft:flint_and_steel>.anyDamage().transformDamage(1), <minecraft:sugar>, <minecraft:sugar>, <minecraft:sugar>, <minecraft:sugar>]);
```

### Modifiers（修饰器）

> `import mods.roots.Modifiers;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.disableModifier(string modifierName)` | void | 禁用指定修饰器 |

```zenscript
import mods.roots.Modifiers;

Modifiers.disableModifier("roots:radius_boost");
```

### Chrysopoeia（点金术/嬗变术）

> `import mods.roots.Chrysopoeia;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(string name, IIngredient ingredient, IItemStack output)` | void | 添加嬗变配方（支持变换器） |
| `.removeRecipeByOutput(IItemStack output)` | void | 根据输出移除配方（不比较数量） |
| `.removeRecipe(IItemStack input)` | void | 根据精确输入移除配方（包括数量、标签等） |

```zenscript
import mods.roots.Chrysopoeia;

Chrysopoeia.addRecipe("ghast_tear", <ore:gunpowder> * 5, <minecraft:ghast_tear>);

Chrysopoeia.addRecipe("magma_cream", <minecraft:flint_and_steel>.transformDamage(1), <minecraft:magma_cream>);

Chrysopoeia.removeRecipeByOutput(<minecraft:iron_ingot>);

Chrysopoeia.removeRecipe(<mysticalworld:silver_ingot> * 2);
```

### Transmutation（自然嬗变仪式）

> `import mods.roots.Transmutation;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(string name)` | void | 根据名称移除嬗变配方 |
| `.addStateToStateRecipe(string name, IPredicate start, IBlockState result, IWorldPredicate condition)` | void | 添加方块状态→方块状态的嬗变配方（condition 可为 null） |
| `.addStateToItemRecipe(string name, IPredicate start, IItemStack result, IWorldPredicate condition)` | void | 添加方块状态→物品的嬗变配方（condition 可为 null） |

```zenscript
import crafttweaker.block.IBlockState;
import mods.roots.predicates.Predicates;
import mods.roots.predicates.BlockStateBelow;
import mods.roots.predicates.PropertyPredicate;
import mods.roots.Transmutation;

// 云杉木下方为树叶时转化为萤石
Transmutation.addStateToStateRecipe("spruce_to_glowstone", PropertyPredicate.create(<blockstate:minecraft:log:variant=spruce> as IBlockState, "variant"), <blockstate:minecraft:glowstone>, BlockStateBelow.create(Predicates.Leaves));

// 金合欢木下方为水时转化为圆石物品
Transmutation.addStateToItemRecipe("acacia_to_cobblestone", PropertyPredicate.create(<blockstate:minecraft:log2:variant=acacia> as IBlockState, "variant"), <minecraft:cobblestone>, BlockStateBelow.create(Predicates.Water));

Transmutation.removeRecipe("pumpkin_to_melon");
```

### Bark（树皮）

> `import mods.roots.Bark;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(string name, IItemStack woodLog, IItemStack bark)` | void | 添加树皮配方，woodLog 必须是物品方块 |
| `.removeRecipe(IItemStack bark)` | void | 根据输出树皮移除配方（不比较数量） |

```zenscript
import mods.roots.Bark;

Bark.addRecipe("melon", <minecraft:melon_block>, <minecraft:sand> * 2);

Bark.removeRecipe(<roots:bark_wildwood>);
```

### AnimalHarvest（动物采收仪式）

> `import mods.roots.AnimalHarvest;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addEntity(IEntityDefinition entity)` | void | 将实体添加到动物收割仪式列表 |
| `.removeEntity(IEntityDefinition entity)` | void | 从动物收割仪式列表中移除实体 |
| `.addFish(string name, IItemStack fish, int weight)` | void | 添加鱼类掉落（weight 为权重） |
| `.removeFish(IItemStack fish)` | void | 移除鱼类掉落 |

```zenscript
import mods.roots.AnimalHarvest;

AnimalHarvest.addEntity(<entity:minecraft:enderman>);
AnimalHarvest.removeEntity(<entity:minecraft:cow>);
AnimalHarvest.addFish("magma_cream", <minecraft:magma_cream>, 20);
AnimalHarvest.removeFish(<minecraft:fish:3>);
```

### FlowerGrowth（繁花争艳仪式）

> `import mods.roots.FlowerGrowth;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(string name)` | void | 根据名称移除花卉生长配方 |
| `.addRecipeBlockState(string name, IBlockState state)` | void | 通过方块状态添加花卉生长配方 |
| `.addRecipeBlock(string name, IBlock block, int meta)` | void | 通过方块+meta 添加花卉生长配方 |
| `.addRecipeItem(string name, IItemStack stack)` | void | 通过物品方块添加花卉生长配方 |
| `.addRecipeItemOnSoils(string name, IItemStack stack, List allowedSoils)` | void | 添加仅在指定土壤上生长的配方（支持矿辞） |

```zenscript
import mods.roots.FlowerGrowth;

FlowerGrowth.removeRecipe("dandelion");
FlowerGrowth.addRecipeBlockState("mystical_white_flower", <blockstate:botania:flower:color=white>);
FlowerGrowth.addRecipeBlock("mystical_green_flower", <botania:flower>.asBlock(), 2);
```

### SummonCreatures（召唤生物仪式）

> `import mods.roots.SummonCreatures;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addEntity(IEntityDefinition entity, IIngredient[] ingredients)` | void | 添加召唤配方 |
| `.removeEntity(IEntityDefinition entity)` | void | 移除召唤配方 |
| `.addLifeEssence(IEntityDefinition entity)` | void | 添加生命精华掉落能力 |
| `.removeLifeEssence(IEntityDefinition entity)` | void | 移除生命精华掉落能力 |
| `.clearLifeEssence()` | void | 清除所有自动生成的生命精华条目 |

```zenscript
import mods.roots.SummonCreatures;

SummonCreatures.clearLifeEssence();
SummonCreatures.addEntity(<entity:minecraft:chicken>, [<minecraft:wheat_seeds>, <minecraft:wheat>, <ore:ingotIron>]);
SummonCreatures.removeLifeEssence(<entity:minecraft:enderman>);
SummonCreatures.addLifeEssence(<entity:minecraft:ender_dragon>);
SummonCreatures.removeEntity(<entity:minecraft:cow>);
```

### Pacifist（和平主义者）

> `import mods.roots.Pacifist;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addEntity(IEntityDefinition entity)` | void | 添加实体到和平主义者列表（击杀后触发成就） |
| `.removeEntity(IEntityDefinition entity)` | void | 从和平主义者列表中移除实体 |

```zenscript
import mods.roots.Pacifist;

Pacifist.addEntity(<entity:minecraft:enderman>);
Pacifist.removeEntity(<entity:minecraft:cow>);
```

### RunicShears（符文剪刀）

> `import mods.roots.RunicShears;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(string name, IItemStack outputDrop, IPredicate inputState, IBlockState replacementState, IItemStack displayItem)` | void | 添加方块剪切配方 |
| `.addRecipeViaItem(string name, IItemStack outputDrop, IItemStack inputBlock, IItemStack replacementBlock, IItemStack displayItem)` | void | 通过物品方块添加方块剪切配方 |
| `.addEntityRecipe(string name, IItemStack outputDrop, IEntityDefinition entity, int cooldown)` | void | 添加实体剪切配方，cooldown 为冷却 tick 数 |
| `.removeRecipe(IItemStack output)` | void | 移除匹配输出的配方（包括方块和实体配方） |
| `.removeEntityRecipe(IEntityDefinition entity)` | void | 移除指定实体的所有配方 |

```zenscript
import mods.roots.RunicShears;

RunicShears.addRecipe("nether_wart_block", <minecraft:nether_wart> * 2, StatePredicate.create(<blockstate:minecraft:red_nether_brick>), <blockstate:minecraft:nether_brick>, <minecraft:red_nether_brick>);

RunicShears.removeEntityRecipe(<entity:minecraft:chicken>);

RunicShears.addEntityRecipe("egg_from_chicken", <minecraft:egg> * 2, <entity:minecraft:chicken>, 120 * 20);

RunicShears.removeRecipe(<roots:fey_leather>);
```

### Predicates（谓词工具）

> `import mods.roots.predicates.Predicates;`

#### 静态属性

| 属性 | 说明 |
|------|------|
| `Predicates.Lava` | 匹配岩浆和流动岩浆 |
| `Predicates.Water` | 匹配水和流水 |
| `Predicates.Leaves` | 匹配所有类型的树叶 |

### PropertyPredicate（属性谓词）

> `import mods.roots.predicates.PropertyPredicate;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(IBlockState state, string properties)` | PropertyPredicate | 创建匹配指定属性的谓词 |
| `.create(IBlockState state, string[] properties)` | PropertyPredicate | 创建匹配多个属性的谓词 |

### StatePredicate（状态谓词）

> `import mods.roots.predicates.StatePredicate;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(IBlockState state)` | StatePredicate | 创建仅匹配方块类型（忽略属性值）的谓词 |

### BlockStateAbove（上方方块条件）

> `import mods.roots.predicates.BlockStateAbove;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(IPredicate predicate)` | BlockStateAbove | 创建检测上方方块的世界条件 |

### BlockStateBelow（下方方块条件）

> `import mods.roots.predicates.BlockStateBelow;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(IPredicate predicate)` | BlockStateBelow | 创建检测下方方块的世界条件 |