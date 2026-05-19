# CompatSkills CraftTweaker API 参考

> Mod ID: `compatskills`
> 前置条件: Reskillable
> 导入: `import mods.compatskills.*;`

CompatSkills 是 Reskillable 的兼容插件，提供技能和需求系统。

---

## API 列表

### Requirement（需求系统）

> `import mods.compatskills.Requirement;`

需求系统用于限制物品使用、维度进入等。

#### 添加需求

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRequirement(item as IItemStack, requirements as string...)` | void | 为物品添加需求 |

#### 需求类型语法

**技能需求**:
```
reskillable:技能名|等级
```

**特性需求**:
```
trait|reskillable:特性名
```

**成就需求**:
```
adv|minecraft:成就路径
```

**游戏阶段需求**:
```
stage|阶段名
```

**维度需求**:
```
dim|维度ID
```

**物品需求**:
```
stack|modid:item:meta
stack|modid:item:meta|NBT
```

**矿辞需求**:
```
ore|矿辞名
```

**工具等级需求**:
```
harvest|等级
```

### PlayerExpansion（玩家扩展）

> `import mods.compatskills.PlayerExpansion;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `skillData` | CTPlayerData | 玩家技能数据 |

### CTPlayerData（玩家技能数据）

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getSkillInfo(skill as CTSkill)` | CTPlayerSkillInfo | 获取技能信息 |
| `.getHasAnyAbilities()` | bool | 是否有任何能力 |

### CTPlayerSkillInfo（玩家技能信息）

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getLevel()` | int | 获取技能等级 |
| `.getSkillPoints()` | int | 获取技能点数 |
| `.getLevelUpCost()` | int | 获取升级消耗 |
| `.getRank()` | string | 获取技能等级名称 |
| `.getSkill()` | CTSkill | 获取技能对象 |
| `.levelUp()` | void | 升级技能 |
| `.respec()` | void | 重置技能 |
| `.unlock(ctUnlockable as CTUnlockable, player as IPlayer)` | void | 解锁特性 |

### 技能和特性列表

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

### 逻辑运算符

**NOT 运算符**:
```
not|需求
```

**AND 运算符**:
```
and|[需求1]~[需求2]
```

**OR 运算符**:
```
or|[需求1]~[需求2]
```

**NAND 运算符**:
```
nand|[需求1]~[需求2]
```

**NOR 运算符**:
```
nor|[需求1]~[需求2]
```

**XOR 运算符**:
```
xor|[需求1]~[需求2]
```

**XNOR 运算符**:
```
xnor|[需求1]~[需求2]
```

### 模组支持

#### Immersive Engineering

> `import mods.compatskills.IEMultiBlockGate;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGate(multiBlockName as string, failureMessage as string, requirements as string...)` | void | 添加多方块结构需求 |

#### Magneticraft

> `import mods.compatskills.MagMultiBlockGates;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGate(multiBlockName as string, failureMessage as string, requirements as string...)` | void | 添加多方块结构需求 |

#### GameStages

> `import mods.compatskills.GameStagesLock;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGameStageLock(gameStage as string, requirements as string...)` | void | 添加游戏阶段锁定 |

#### Blood Magic

> `import mods.compatskills.BindingSupport;`
> `import mods.compatskills.RitualSupport;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addBindingLock(recipe as IItemStack, requirements as string...)` | void | 添加绑定锁定 |
| `.addRitualLock(ritual as string, requirements as string...)` | void | 添加仪式锁定 |

---

## 注意事项

- 需要 Reskillable 模组支持
- 需求语法区分大小写
- 逻辑运算符可以嵌套使用
