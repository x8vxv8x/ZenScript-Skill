# Biomes CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.world.IBiome;`

生物群系属性 API，用于获取和修改生物群系属性。

---

## API 列表

### IBiome（生物群系）

> `import crafttweaker.world.IBiome;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 生物群系名称 |
| `id` | int | ID |
| `temperature` | float | 温度 |
| `rainfall` | float | 降雨量 |
| `humidity` | float | 湿度 |
| `canRain` | bool | 是否可以下雨 |
| `isSnowyBiome` | bool | 是否雪地 |
| `highHumidity` | bool | 是否高湿度（湿度 > 0.85） |
| `isHumid` | bool | 是否潮湿 |
| `ignorePlayerSpawnSuitability` | bool | 是否忽略玩家生成适应性 |
| `waterColorMultiplier` | int | 水颜色倍增器 |
| `spawningChance` | float | 生物生成概率 |
| `minHeight` | float | 最小高度 |
| `maxHeight` | float | 最大高度 |
| `baseHeight` | float | 基础高度 |
| `heightVariation` | float | 高度变化 |
| `enableRain` | bool | 是否启用雨 |
| `enableSnow` | bool | 是否启用雪 |
| `types` | List\<IBiomeType\> | 此生物群系所属的生物群系类型列表 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.canRain()` | bool | 是否可以下雨 |
| `.isSnowyBiome()` | bool | 是否雪地 |
| `.setTemperature(float)` | void | 设置温度 |
| `.setRainfall(float)` | void | 设置降雨量 |
| `.setWaterColorMultiplier(int)` | void | 设置水颜色倍增器 |
| `.setEnableRain(bool)` | void | 设置是否启用雨 |
| `.setEnableSnow(bool)` | void | 设置是否启用雪 |
| `.setMinHeight(float)` | void | 设置最小高度 |
| `.setMaxHeight(float)` | void | 设置最大高度 |
| `.setBaseHeight(float)` | void | 设置基础高度 |
| `.setHeightVariation(float)` | void | 设置高度变化 |

### IBiomeType（生物群系类型）

> `import crafttweaker.world.IBiomeType;`

IBiomeType 代表一种生物群系类型（如森林、沙漠等），通过 `biome.types` 获取。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 生物群系类型名称 |
| `biomes` | List\<IBiome\> | 此类型包含的生物群系列表 |

---

## 使用示例

### 获取生物群系

```zenscript
// 从世界获取
val biome = world.getBiome(blockPos);

// 从游戏对象获取
val biome = game.getBiome("minecraft:plains");

// 获取所有生物群系
for biome in game.biomes {
    print(biome.name);
}
```

### 生物群系属性修改

```zenscript
// 修改温度
biome.setTemperature(0.8f);

// 修改降雨量
biome.setRainfall(0.4f);

// 修改水颜色
biome.setWaterColorMultiplier(0x3F76E4);

// 启用/禁用雨
biome.setEnableRain(true);

// 启用/禁用雪
biome.setEnableSnow(false);
```
