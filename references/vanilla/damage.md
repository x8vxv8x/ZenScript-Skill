# Damage CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.damage.IDamageSource;`

伤害来源 API，用于创建和操作伤害来源。

---

## API 列表

### IDamageSource（伤害来源）

> `import crafttweaker.damage.IDamageSource;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 伤害来源名称 |
| `commandString` | string | 命令字符串 |
| `damageType` | string | 伤害类型 |
| `isUnblockable` | bool | 是否不可格挡 |
| `isDamageAbsolute` | bool | 是否绝对伤害 |
| `isDifficultyScaled` | bool | 是否随难度缩放 |
| `isFireDamage` | bool | 是否火焰伤害 |
| `isMagicDamage` | bool | 是否魔法伤害 |
| `isExplosion` | bool | 是否爆炸伤害 |
| `isProjectile` | bool | 是否弹射物伤害 |
| `isFallDamage` | bool | 是否摔落伤害 |
| `isCreativePlayer` | bool | 是否创造模式玩家 |
| `hungerDamage` | float | 饥饿伤害 |
| `creativePlayer` | IPlayer | 创造模式玩家 |
| `immediateSource` | IEntity | 直接来源实体 |
| `trueSource` | IEntity | 真正来源实体 |
| `damageEntity` | IEntity | 造成伤害的实体 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setDamageBypassesArmor()` | IDamageSource | 设置伤害无视护甲 |
| `.setDamageIsAbsolute()` | IDamageSource | 设置绝对伤害 |
| `.setDamageAllowedInCreativeMode()` | IDamageSource | 设置允许在创造模式造成伤害 |
| `.setDifficultyScaled()` | IDamageSource | 设置随难度缩放 |
| `.setExplosion()` | IDamageSource | 设置为爆炸伤害 |
| `.setFireDamage()` | IDamageSource | 设置为火焰伤害 |
| `.setMagicDamage()` | IDamageSource | 设置为魔法伤害 |
| `.setProjectile()` | IDamageSource | 设置为弹射物伤害 |
| `.setFallDamage()` | IDamageSource | 设置为摔落伤害 |

### 预定义伤害来源

```zenscript
<damageSource:MAGIC>                 // 魔法伤害
<damageSource:GENERIC>               // 通用伤害
<damageSource:IN_FIRE>               // 火焰伤害
<damageSource:LAVA>                  // 岩浆伤害
<damageSource:IN_WALL>               // 窒息伤害
<damageSource:STARVE>                // 饥饿伤害
<damageSource:OUT_OF_WORLD>          // 虚空伤害
<damageSource:FALL>                  // 摔落伤害
<damageSource:CRAMMING>              // 挤压伤害
<damageSource:DROWN>                 // 溺水伤害
<damageSource:LIGHTNING_BOLT>        // 闪电伤害
```

---

## 使用示例

### 造成伤害

```zenscript
// 对实体造成伤害
entity.attackEntityFrom(<damageSource:MAGIC>, 5.0f);

// 对玩家造成伤害
player.attackEntityFrom(<damageSource:MAGIC>, 5.0f);

// 条件伤害（合成后扣血）
recipes.addShapeless("hurt_recipe", <minecraft:sapling>,
    [<minecraft:stick>, <minecraft:leaves>],
    function(out, ins, info) {
        return info.player.health > 5 ? out : null;  // 血量 > 5 才能合成
    },
    function(out, info, player) {
        player.attackEntityFrom(<damageSource:MAGIC>, 5.0f);  // 扣 5 血
    }
);
```
