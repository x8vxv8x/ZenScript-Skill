# Brackets API

## 尖括号语法

尖括号 `<...>` 是 ZenScript 中最常用的获取游戏对象的方式。

### 物品

```zenscript
<minecraft:apple>                    // 物品
<minecraft:stone:3>                  // 带 Meta 的物品
<minecraft:wool:*>                   // 任意 Meta（通配符）
<minecraft:wool:0>                   // Meta 0
```

### 矿物词典

```zenscript
<ore:ingotIron>                      // 矿辞
<ore:ingotGold>                      // 矿辞
<ore:dirt>                           // 矿辞
```

### 流体

```zenscript
<liquid:water>                       // 流体
<liquid:lava>                        // 流体
<liquid:lava> * 1000                 // 带数量的流体
```

### 实体

```zenscript
<entity:minecraft:sheep>             // 实体定义
<entity:minecraft:creeper>           // 实体定义
```

### 方块

```zenscript
<block:minecraft:stone>              // 方块定义
<block:minecraft:dirt>               // 方块定义
```

### 附魔

```zenscript
<enchantment:fortune>                // 附魔定义
<enchantment:fortune> * 3            // 附魔等级 3
<enchantment:sharpness>              // 附魔定义
```

### 药水效果

```zenscript
<potion:minecraft:speed>             // 药水效果
<potion:minecraft:slowness>          // 药水效果
```

### 伤害来源

```zenscript
<damageSource:MAGIC>                 // 魔法伤害
<damageSource:GENERIC>               // 通用伤害
<damageSource:IN_FIRE>               // 火焰伤害
<damageSource:LAVA>                  // 岩浆伤害
<damageSource:OUT_OF_WORLD>          // 虚空伤害
```

### 生物群系

```zenscript
<biome:minecraft:plains>             // 生物群系
<biome:minecraft:desert>             // 生物群系
```

---

## 获取对象的其他方式

```zenscript
// 从物品定义获取
<minecraft:wool>.definition.makeStack(3)

// 从矿辞获取
<ore:ingotIron>.items                // 所有物品列表
<ore:ingotIron>.firstItem            // 第一个物品

// 从 mod 获取
loadedMods["minecraft"].items        // mod 所有物品

// 从游戏对象获取
game.getBlock("minecraft:stone")     // 方块
game.getItem("minecraft:apple")      // 物品
game.getEntity("minecraft:sheep")    // 实体定义
game.getPotion("minecraft:speed")    // 药水效果
game.getBiome("minecraft:plains")    // 生物群系
```
