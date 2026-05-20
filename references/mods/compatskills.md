# CompatSkills CraftTweaker API 参考

> Mod ID: `compatskills`
> 前置条件: Reskillable
> 导入: `import mods.compatskills.*;`

CompatSkills 是 Reskillable 的兼容插件，为物品、方块、维度、实体等添加技能/需求锁定系统。

---

## API 列表

### Requirement（需求锁定）

> `import mods.compatskills.Requirement;`

为物品添加使用需求，不满足需求时物品将被禁用。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRequirement(item as IItemStack, requirements as string...)` | void | 为指定物品添加需求锁定 |

### SkillLocks（技能等级锁定）

> `import mods.compatskills.SkillLocks;`

锁定技能升级到指定等级所需的条件。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addLevelLock(skill as CTSkill, level as int, requirements as string...)` | void | 锁定技能升级到指定等级 |

### ModLock（模组锁定）

> `import mods.compatskills.ModLock;`

锁定指定模组的所有物品。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addModLock(modId as string, requirements as string...)` | void | 锁定指定模组的所有物品 |

### NBTLock（NBT 锁定）

> `import mods.compatskills.NBTLock;`

根据 NBT 标签锁定物品，可锁定附魔、匠魂材料/强化等。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGenericNBTLock(tag as IData, requirements as string...)` | void | 全局 NBT 锁定，影响所有含该 NBT 的物品 |
| `.addModNBTLock(modId as string, tag as IData, requirements as string...)` | void | 模组范围 NBT 锁定，只影响指定模组中含该 NBT 的物品 |

### VisibilityLock（技能可见性锁定）

> `import mods.compatskills.VisibilityLock;`

隐藏技能直到满足条件。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addVisibilityLock(skill as CTSkill, requirements as string...)` | void | 隐藏技能直到满足需求 |

### SkillChange（技能变化命令）

> `import mods.compatskills.SkillChange;`

在玩家升级技能或解锁/锁定特性时执行命令。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addLevelUpCommands(skill as CTSkill, level as int, commands as string...)` | void | 升级到指定等级时执行命令 |
| `.addUnlockableUnlockCommands(unlockable as CTUnlockable, commands as string...)` | void | 解锁特性时执行命令 |
| `.addUnlockableLockCommands(unlockable as CTUnlockable, commands as string...)` | void | 锁定特性时执行命令 |

### SkillCreator（自定义技能）

> `import mods.compatskills.SkillCreator;`

创建自定义技能。

#### 创建方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createSkill(name as string, backGroundLocation as string)` | CrTSkill | 创建技能（自动使用 compatskills 作为 ModID） |
| `.createNewSkill(nameLocation as string, backGroundLocation as string)` | CrTSkill | 创建技能（自定义 ResourceLocation） |

#### CrTSkill 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 技能名称（硬编码后无法通过 .lang 本地化） |

#### CrTSkill @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `.getLevelCap` | int | 获取等级上限 |
| `.getEnabled` | bool | 是否启用 |
| `.getBaseLevelCost` | int | 获取基础升级消耗 |
| `.getName` | string | 获取本地化名称 |
| `.getLevelStaggering` | string[] | 获取等级消耗阶梯 |
| `.isHidden` | bool | 是否隐藏 |

#### CrTSkill @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `.setLevelCap(cap as int)` | void | 设置等级上限 |
| `.setEnabled(enabled as bool)` | void | 设置启用状态 |
| `.setSkillPointInterval(interval as int)` | void | 设置技能点间隔 |
| `.setBaseLevelCost(cost as int)` | void | 设置基础升级消耗 |
| `.setLevelStaggering(stagger as string[])` | void | 设置等级消耗阶梯 |
| `.setHidden(hidden as bool)` | void | 设置隐藏状态 |
| `.setRankIcon(rank as int, location as string)` | void | 设置指定等级的图标 |

### TraitCreator（自定义特性）

> `import mods.compatskills.TraitCreator;`

创建自定义特性（可绑定事件）。

#### 创建方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createTrait(traitName as string, x as int, y as int, skillLocation as string, cost as int, @Optional requirements as string...)` | CrTTrait | 创建特性（自动使用 compatskills 作为 ModID） |
| `.createTrait(traitName as string, x as int, y as int, parentSkill as CrTSkill, cost as int, @Optional requirements as string...)` | CrTTrait | 创建特性（使用技能对象作为父技能） |
| `.createNewTrait(traitLocation as string, x as int, y as int, skillLocation as string, cost as int, @Optional requirements as string...)` | CrTTrait | 创建特性（自定义 ResourceLocation） |
| `.createNewTrait(traitLocation as string, x as int, y as int, parentSkill as CrTSkill, cost as int, @Optional requirements as string...)` | CrTTrait | 创建特性（自定义 ResourceLocation + 技能对象） |

#### CrTTrait 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 特性名称（硬编码后无法通过 .lang 本地化） |
| `description` | string | 特性描述（硬编码后无法通过 .lang 本地化） |

#### CrTTrait @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `.getEnabled` | bool | 是否启用 |
| `.getName` | string | 获取本地化名称 |
| `.getDescription` | string | 获取本地化描述 |
| `.retrieveIcon` | string | 获取图标 ResourceLocation |

#### CrTTrait @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `.setEnabled(enabled as bool)` | void | 设置启用状态 |
| `.changeIcon(location as string)` | void | 设置图标 |

#### CrTTrait 事件

| 事件 | 事件类型 | 说明 |
|------|----------|------|
| `onAttackMob` | EntityLivingHurtEvent | 攻击生物时触发 |
| `onBlockDrops` | BlockHarvestDropsEvent | 方块掉落时触发 |
| `onBreakSpeed` | PlayerBreakSpeedEvent | 破坏速度变化时触发 |
| `onEnderTeleport` | EnderTeleportEvent | 末影传送时触发 |
| `onHurt` | EntityLivingHurtEvent | 受伤时触发 |
| `onKillMob` | EntityLivingDeathEvent | 击杀生物时触发 |
| `onMobDrops` | EntityLivingDeathDropsEvent | 生物死亡掉落时触发 |
| `onPlayerTick` | PlayerTickEvent | 玩家 Tick 时触发 |
| `onRightClickBlock` | PlayerInteractBlockEvent | 右键方块时触发 |

**事件回调属性（onBlockDrops）**:

| 属性 | 类型 | 读/写 | 说明 |
|------|------|-------|------|
| `dropChance` | float | 读写 | 掉落几率 |
| `fortuneLevel` | int | 只读 | 时运等级 |
| `drops` | IItemStack[] | 读写 | 掉落物列表 |
| `silkTouch` | bool | 只读 | 是否精准采集 |
| `isPlayer` | bool | 只读 | 是否玩家 |
| `player` | IPlayer | 只读 | 玩家对象 |

方法: `.addItem(item as IItemStack)` — 添加掉落物

**事件回调属性（onBreakSpeed）**:

| 属性 | 类型 | 读/写 | 说明 |
|------|------|-------|------|
| `blockState` | IBlockState | 只读 | 方块状态 |
| `block` | IBlock | 只读 | 方块 |
| `originalSpeed` | float | 只读 | 原始速度 |
| `newSpeed` | float | 读写 | 新速度 |

**事件回调属性（onEnderTeleport）**:

| 属性 | 类型 | 读/写 | 说明 |
|------|------|-------|------|
| `targetX` | double | 读写 | 目标 X 坐标 |
| `targetY` | double | 读写 | 目标 Y 坐标 |
| `targetZ` | double | 读写 | 目标 Z 坐标 |
| `attackDamage` | float | 读写 | 攻击伤害 |

**事件回调属性（onAttackMob / onHurt）**:

| 属性 | 类型 | 读/写 | 说明 |
|------|------|-------|------|
| `damageSource` | IDamageSource | 只读 | 伤害来源 |
| `amount` | float | 只读 | 伤害值 |

**事件回调属性（onKillMob）**:

| 属性 | 类型 | 读/写 | 说明 |
|------|------|-------|------|
| `damageSource` | IDamageSource | 只读 | 伤害来源 |

**事件回调属性（onMobDrops）**:

| 属性 | 类型 | 读/写 | 说明 |
|------|------|-------|------|
| `damageSource` | IDamageSource | 只读 | 伤害来源 |
| `lootingLevel` | int | 只读 | 抢夺等级 |
| `isRecentlyHit` | bool | 只读 | 是否最近被攻击 |
| `drops` | IEntityItem[] | 读写 | 掉落物列表 |

方法: `.addItem(item as IItemStack)` / `.addItem(entityItem as IEntityItem)` — 添加掉落物

**事件回调属性（onRightClickBlock）**:

| 属性 | 类型 | 读/写 | 说明 |
|------|------|-------|------|
| `hitVector` | IVector3d | 只读 | 命中向量 |
| `useBlock` | string | 读写 | 使用方块行为 |
| `useItem` | string | 读写 | 使用物品行为 |

### GameStageUnlockable（游戏阶段可解锁项）

> `import mods.compatskills.GameStageUnlockable;`

创建"虚拟特性"，解锁后自动解锁对应游戏阶段。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGameStageUnlockable(gamestage as string, name as string, x as int, y as int, skillName as string, cost as int, @Optional requirements as string...)` | void | 创建可解锁的游戏阶段 |

### GameStageLocks（游戏阶段锁定）

> `import mods.compatskills.GameStageLocks;`

锁定游戏阶段的解锁条件。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGameStageLock(gamestage as string, requirements as string...)` | void | 锁定游戏阶段 |

### DimensionLock（维度锁定）

> `import mods.compatskills.DimensionLock;`

锁定维度进入条件。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addDimensionLock(dimension as int, requirements as string...)` | void | 锁定维度进入 |

### HarvestLock（挖掘等级锁定）

> `import mods.compatskills.HarvestLock;`

锁定方块/工具的挖掘等级。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addBlockLevelLock(level as int, requirements as string...)` | void | 锁定指定挖掘等级的方块 |
| `.addToolLevelLock(level as int, requirements as string...)` | void | 锁定指定挖掘等级的所有工具 |
| `.addToolLevelLock(type as string, level as int, requirements as string...)` | void | 锁定指定类型和挖掘等级的工具（如 "pickaxe"） |

### ArmorLock（护甲值锁定）

> `import mods.compatskills.ArmorLock;`

锁定护甲值达到指定值的装备。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addArmorLock(armor as double, requirements as string...)` | void | 锁定护甲值 >= 指定值的装备 |

### DamageLock（攻击力锁定）

> `import mods.compatskills.DamageLock;`

锁定攻击力达到指定值的武器/工具。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addDamageLock(damage as double, requirements as string...)` | void | 锁定攻击力 >= 指定值的武器 |

### EntityDamageLock（实体伤害锁定）

> `import mods.compatskills.EntityDamageLock;`

锁定对指定实体的攻击。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addEntityLock(definition as IEntityDefinition, requirements as string...)` | void | 锁定对指定实体的攻击 |

### FoodTweaker（食物锁定）

> `import mods.compatskills.FoodTweaker;`

锁定食物的饥饿值/饱和度。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addHungerLock(level as int, requirements as string...)` | void | 锁定饥饿值 >= 指定值的食物 |
| `.addSaturationLock(level as float, requirements as string...)` | void | 锁定饱和度 >= 指定值的食物 |

### AnimalTameLock（骑乘/驯服锁定）

> `import mods.compatskills.AnimalTameLock;`

锁定骑乘和驯服指定实体。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addTameLock(definition as IEntityDefinition, requirements as string...)` | void | 锁定骑乘/驯服指定实体 |

### TileEntityLock（方块实体锁定）

> `import mods.compatskills.TileEntityLock;`

锁定与指定方块实体的交互。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addTileEntityLock(tileName as string, requirements as string...)` | void | 锁定与指定方块实体的交互 |

### OreDictLock（矿辞锁定）

> `import mods.compatskills.OreDictLock;`

锁定矿辞下的所有物品。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addOreDictLock(entry as IOreDictEntry, requirements as string...)` | void | 锁定矿辞下的所有物品 |
| `.addNBTOreDictLock(entry as IOreDictEntry, tag as IData, requirements as string...)` | void | 锁定矿辞下匹配 NBT 的物品 |

### EMCLock（EMC 锁定）

> `import mods.compatskills.EMCLock;`

锁定 ProjectE 中 EMC 值 >= 指定值的物品的转化学习和复制。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addEMCLock(emc as int, requirements as string...)` | void | 锁定 EMC >= 指定值的物品 |

---

## 模组支持

### Blood Magic

> `import mods.compatskills.BindHandler;`
> `import mods.compatskills.RitualHandler;`

#### BindHandler（绑定锁定，1.4.0 前）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addBindLock(failureMessage as string, stack as IItemStack, requirements as string...)` | void | 锁定物品绑定（1.4.0 后改用 Requirement.addRequirement） |

#### RitualHandler（仪式锁定）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRitualLock(ritual as string, requirements as string...)` | void | 锁定仪式激活 |
| `.addRitualCostLock(activationCost as int, requirements as string...)` | void | 锁定仪式激活消耗 |
| `.addRitualCrystalLock(crystalLevel as int, requirements as string...)` | void | 锁定仪式水晶等级 |

命令: `/ct ritualDump` — 输出所有仪式字符串

### Immersive Engineering

> `import mods.compatskills.IEMultiBlockGate;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGate(multiBlockName as string, failureMessage as string, requirements as string...)` | void | 锁定 IE 多方块结构 |

命令: `/ct ieMultiBlocks` — 输出所有 IE 多方块名称

### Magneticraft

> `import mods.compatskills.MagMultiBlockGates;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGate(multiBlockName as string, failureMessage as string, requirements as string...)` | void | 锁定 Magneticraft 多方块结构 |

命令: `/ct magMultiBlocks` — 输出所有 Magneticraft 多方块名称

### Tinkers' Construct

> `import mods.compatskills.MaterialLock;`
> `import mods.compatskills.ModifierLock;`

#### MaterialLock（材料锁定）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addMaterialLock(identifier as string, requirements as string...)` | void | 锁定匠魂材料（影响工具制作、部件制作、部件替换） |

#### ModifierLock（强化锁定）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addModifierLock(identifier as string, requirements as string...)` | void | 锁定匠魂强化 |

命令: `/ct tinkermaterials` — 输出所有材料 | `/ct tinkermodifiers` — 输出所有强化

### Thaumcraft

> `import mods.compatskills.Thaumcraft;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addKnowledgeLock(categoryName as string, knowledgeType as string, requirements as string...)` | void | 锁定神秘学知识获取（O=观察, T=理论） |
| `.addResearchLock(researchKey as string, requirements as string...)` | void | 锁定神秘学研究获取 |

### ProjectE

> `import mods.compatskills.EMCLock;`

见上方 EMCLock 章节。

### Transmutations（嬗变系统）

> `import mods.compatskills.transmutations.additions;`
> `import mods.compatskills.transmutations.removals;`
> `import mods.compatskills.transmutations.clears;`

#### additions（添加嬗变）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addEntryToReagent(reagent as IItemStack, startState as IItemStack, endState as IItemStack)` | void | 为试剂添加方块状态嬗变 |
| `.addEntryToReagent(reagent as IItemStack, state1 as IBlockState, state2 as IBlockState)` | void | 为试剂添加方块状态嬗变 |
| `.addEntryToReagentAgnostic(startState as IItemStack, endState as IItemStack)` | void | 为所有试剂添加方块状态嬗变 |
| `.addEntryToReagentAgnostic(state1 as IBlockState, state2 as IBlockState)` | void | 为所有试剂添加方块状态嬗变 |

#### removals（移除嬗变）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeStartStateFromReagent(reagent as IItemStack, startState as IItemStack)` | void | 从指定试剂移除起始状态嬗变 |
| `.removeStartStateFromReagent(reagent as IItemStack, state as IBlockState)` | void | 从指定试剂移除起始状态嬗变 |
| `.removeStartStateReagentAgnostic(state as IItemStack)` | void | 从所有试剂移除起始状态嬗变 |
| `.removeStartStateReagentAgnostic(state as IBlockState)` | void | 从所有试剂移除起始状态嬗变 |
| `.removeEndStateFromReagent(reagent as IItemStack, state as IItemStack)` | void | 从指定试剂移除结果状态嬗变 |
| `.removeEndStateFromReagent(reagent as IItemStack, state as IBlockState)` | void | 从指定试剂移除结果状态嬗变 |
| `.removeEndStateReagentAgnostic(state as IItemStack)` | void | 从所有试剂移除结果状态嬗变 |
| `.removeEndStateReagentAgnostic(state as IBlockState)` | void | 从所有试剂移除结果状态嬗变 |

#### clears（清空嬗变）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.clearMapOfReagent(stack as IItemStack)` | void | 清空指定试剂的所有嬗变 |
| `.clearReagentOfEntries(stack as IItemStack)` | void | 清空试剂的嬗变条目 |
| `.clearReagentMap()` | void | 清空整个嬗变表 |

---

## Bracket Handlers（括号处理器）

| 括号 | 返回 | 说明 |
|------|------|------|
| `<skill:reskillable:agility>` | CTSkill | 技能括号 |
| `<trait:reskillable:sidestep>` | CTUnlockable | 特性括号 |

---

## 需求语法

### 基础需求类型

| 类型 | 语法 | 示例 |
|------|------|------|
| 技能 | `reskillable:技能名\|等级` | `reskillable:building\|15` |
| 特性 | `trait\|reskillable:特性名` | `trait\|reskillable:battle_spirit` |
| 成就 | `adv\|成就路径` | `adv\|minecraft:husbandry/plant_seed` |
| 游戏阶段 | `stage\|阶段名` | `stage\|test` |
| 维度 | `dim\|维度ID` | `dim\|0` |
| 矿辞 | `ore\|矿辞名` | `ore\|ingotIron` |
| 工具等级 | `harvest\|等级` | `harvest\|3` |

### 物品需求语法

| 语法 | 说明 |
|------|------|
| `stack\|modid` | 持有该模组任意物品 |
| `stack\|modid:item` | 持有指定物品（meta=0） |
| `stack\|modid:item:meta` | 持有指定物品和 meta（*为通配） |
| `stack\|\|NBT` | 持有匹配 NBT 的任意物品 |
| `stack\|modid\|NBT` | 持有该模组匹配 NBT 的物品 |
| `stack\|modid:item\|NBT` | 持有指定物品匹配 NBT |
| `stack\|modid:item:meta\|NBT` | 持有指定物品、meta 和 NBT |

### 逻辑运算符

| 运算符 | 语法 | 说明 |
|--------|------|------|
| NOT | `not\|需求` | 取反 |
| AND | `and\|[需求1]~[需求2]` | 两者都满足 |
| OR | `or\|[需求1]~[需求2]` | 满足其一 |
| NAND | `nand\|[需求1]~[需求2]` | 不同时满足 |
| NOR | `nor\|[需求1]~[需求2]` | 都不满足 |
| XOR | `xor\|[需求1]~[需求2]` | 只满足一个 |
| XNOR | `xnor\|[需求1]~[需求2]` | 同时满足或同时不满足 |

支持嵌套: `"or|[reskillable:mining|20]~[and|[reskillable:gathering|25]~[reskillable:mining|15]]"`

---

## 技能和特性列表

**技能**:

| 技能 | ResourceLocation |
|------|------------------|
| Agility | reskillable:agility |
| Attack | reskillable:attack |
| Building | reskillable:building |
| Defense | reskillable:defense |
| Farming | reskillable:farming |
| Gathering | reskillable:gathering |
| Magic | reskillable:magic |
| Mining | reskillable:mining |

**特性**:

| 父技能 | 特性 | ResourceLocation |
|--------|------|------------------|
| Agility | Road Walk | reskillable:roadwalk |
| Agility | Sidestep | reskillable:sidestep |
| Attack | Battle Spirit | reskillable:battle_spirit |
| Attack | Neutralissse | reskillable:neutralissse |
| Building | Chorus Transmutation | reskillable:chorus_transmute |
| Building | Perfect Recovery | reskillable:perfect_recover |
| Defense | Effect Twist | reskillable:effect_twist |
| Defense | Undershirt | reskillable:undershirt |
| Farming | Green Thumb | reskillable:green_thumb |
| Farming | More Wheat | reskillable:more_wheat |
| Gathering | Drop Guarantee | reskillable:drop_guarantee |
| Gathering | Lucky Fisherman | reskillable:lucky_fisherman |
| Magic | Golden Osmosis | reskillable:golden_osmosis |
| Magic | Safe Port | reskillable:safe_port |
| Mining | Fossil Digger | reskillable:fossil_digger |
| Mining | Obsidian Smasher | reskillable:obsidian_smasher |

---

## 使用示例

### 物品需求锁定

```zenscript
import mods.compatskills.Requirement.addRequirement;

// 钻石镐需要挖掘4级
addRequirement(<minecraft:diamond_pickaxe:*>, "reskillable:mining|4");

// 附魔钻石镐需要更高等级
addRequirement(<minecraft:diamond_pickaxe:*>.withTag({ench: [{lvl: 5 as short, id: 32 as short}]}), "reskillable:mining|5", "reskillable:magic|7");
```

### 自定义技能和特性

```zenscript
import mods.compatskills.SkillCreator.createSkill;
import mods.compatskills.Skill;

// 创建自定义技能
val smithing = createSkill("smithing", "mekanism:textures/blocks/steelblock.png");
smithing.name = "Smithing";
smithing.setEnabled(true);
smithing.setBaseLevelCost(0);
smithing.setLevelCap(256);
smithing.setSkillPointInterval(4);
smithing.setRankIcon(0, "minecraft:textures/items/iron_ingot.png");

// 创建自定义特性
var test = mods.compatskills.TraitCreator.createTrait("test", 2, 3, "compatskills:smithing", 1, "compatskills:smithing|5");
test.name = "Test";
test.description = "A test trait";

// 绑定事件
test.onBlockDrops = function(event as crafttweaker.event.BlockHarvestDropsEvent) {
    event.setDropChance(1.0);
};
```

### 游戏阶段锁定

```zenscript
import mods.compatskills.GameStageLocks.addGameStageLock;
import mods.compatskills.GameStageUnlockable.addGameStageUnlockable;

addGameStageLock("i", "reskillable:agility|10");
addGameStageUnlockable("a", "a", 0, 0, "reskillable:gathering", 3, "stage|test");
```

### 逻辑运算符

```zenscript
import mods.compatskills.Requirement.addRequirement;

// 只允许在末地之外攻击僵尸猪人
mods.compatskills.EntityDamageLock.addEntityLock(<entity:minecraft:zombie_pigman>, "not|dim|-1");

// 攻击或防御15级可进入下界
mods.compatskills.DimensionLock.addDimensionLock(-1, "or|[reskillable:attack|15]~[reskillable:defense|15]");

// 防御24且敏捷24后不能使用皮革甲
addRequirement(<minecraft:leather_helmet:*>, "nand|[reskillable:defense|24]~[reskillable:agility|24]");
```
