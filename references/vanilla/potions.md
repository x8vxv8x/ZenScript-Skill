# Potions API

## IPotion

> `import crafttweaker.potions.IPotion;`

通过 `<potion:...>` 获取。

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 药水效果内部名称 |
| `liquidColor` | int | 液体颜色 |
| `liquidColour` | int | 液体颜色（同上，英式拼写） |
| `badEffect` | bool | 是否负面效果 |
| `beneficial` | bool | 是否正面效果 |
| `isInstant` | bool | 是否即时效果 |
| `hasStatusIcon` | bool | 是否有状态图标 |
| `curativeItems` | List\<IItemStack\> | 治愈物品列表 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.makePotionEffect(int, int)` | int, int | IPotionEffect | 创建药水效果（持续时间 ticks，等级） |
| `.makePotionEffect(int, int, bool, bool)` | int, int, bool, bool | IPotionEffect | 创建药水效果（持续时间，等级，是否环境效果，是否显示粒子） |

---

## IPotionEffect

> `import crafttweaker.potions.IPotionEffect;`

IPotionEffect 是带有持续时间和等级的药水效果。

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `potion` | IPotion | 药水效果 |
| `duration` | int | 持续时间（ticks） |
| `amplifier` | int | 等级 |
| `isAmbient` | bool | 是否环境效果 |
| `doesShowParticles` | bool | 是否显示粒子 |
| `isPotionDurationMax` | bool | 是否最大持续时间（可读写） |
| `curativeItems` | List\<IItemStack\> | 治愈物品列表 |
| `effectName` | string | 效果名称 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.isCurativeItem(IItemStack)` | IItemStack | bool | 指定物品是否可治愈此效果 |
| `.performEffect(IEntity)` | IEntity | void | 对实体执行效果 |

---

## IPotionType

> `import crafttweaker.potions.IPotionType;`

IPotionType 代表一种药水类型（如力量药水、治疗药水等），通过 `<potiontype:...>` 获取。

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `effects` | List\<IPotionEffect\> | 此药水类型包含的效果列表 |

### 静态方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `IPotionType.fromString(string)` | string | IPotionType | 从字符串获取药水类型（等同于括号处理器） |

---

## 获取药水效果

```zenscript
// 通过游戏对象获取
val speed = game.getPotion("minecraft:speed");
val slowness = game.getPotion("minecraft:slowness");

// 创建药水效果
val speedEffect = speed.makePotionEffect(600, 1);  // 30秒，等级1
```

---

## 遍历所有药水效果

```zenscript
for potion in game.potions {
    print(potion.name ~ ": " ~ potion.displayName);
}
```
