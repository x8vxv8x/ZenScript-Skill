# Immersive Petroleum CraftTweaker API 参考

> Mod ID: `immersivepetroleum`
> 前置条件: Immersive Engineering
> 导入: `import mods.immersivepetroleum.<ClassName>;`

Immersive Petroleum 是 Immersive Engineering 的轻量级内容扩展，引入石油开采和加工。

---

## API 列表

### Distillation（蒸馏）

> `import mods.immersivepetroleum.Distillation;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack[] fluidOutputs, IItemStack[] itemOutputs, ILiquidStack fluidInput, int energy, int time, float[] chance)` | void | 添加蒸馏配方。`chance` 数组对应 `itemOutputs`，值为 0-1（1=100%） |

---

### Motorboat（汽艇）

> `import mods.immersivepetroleum.Motorboat;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerMotorboatFuel(ILiquidStack fuelEntry, int mbPerTick)` | void | 注册汽艇燃料。`mbPerTick` 为每 tick 消耗量 |

---

### PortableGenerator（便携发电机）

> `import mods.immersivepetroleum.PortableGenerator;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerPortableGenFuel(ILiquidStack fuelEntry, int fluxPerTick, int mbPerTick)` | void | 注册便携发电机燃料。`fluxPerTick` 为每 tick 输出，`mbPerTick` 为每 tick 消耗 |

---

### Lubricant（润滑油）

> `import mods.immersivepetroleum.Lubricant;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerLubricant(ILiquidStack lubricantEntry, int amount)` | void | 注册润滑油。`amount` 为每 4 tick 消耗量（mB/4tick） |

---

### Reservoir（储层）

> `import mods.immersivepetroleum.Reservoir;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerReservoir(String name, ILiquidStack fluid, int minSize, int maxSize, int replenishRate, int weight)` | void | 注册流体储层。`weight` 为区块包含该储层的权重（X/总权重） |

---

## Roids-Tweaker 扩展（需安装 Roids-Tweaker）

### IWorld 扩展

> `import crafttweaker.world.IWorld;`

#### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getReservoir(IBlockPos pos)` | pos | IReservoir | 获取指定位置的储层 |
| `.setReservoir(IBlockPos pos, IReservoir reservoir)` | pos, reservoir | void | 设置指定位置的储层 |

### IReservoir（储层接口）

> `import mods.roidtweaker.immersivepetroleum.IReservoir;`

世界中的流体储层。只有 `current` 和 `capacity` 是实例独立的，修改其他属性会影响所有同类储层。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `capacity` | int | 储层总容量 |
| `current` | int | 当前剩余量 |
| `type` | string | 储层类型 |
| `name` | string | 储层名称 |
| `fluid` | string | 流体类型 |
| `minSize` | int | 最小生成量 |
| `maxSize` | int | 最大生成量 |
| `replenishRate` | int | 补充速率 |
| `dimensionWhitelist` | int[] | 维度白名单 |
| `dimensionBlacklist` | int[] | 维度黑名单 |
| `biomeWhitelist` | string[] | 生物群系白名单 |
| `biomeBlacklist` | string[] | 生物群系黑名单 |

### Reservoir 扩展

> `import mods.immersivepetroleum.Reservoir;`

#### 静态方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.getReservoir(String type)` | type | IReservoir | 获取指定类型的储层（无 `capacity` 和 `current`） |
| `.getRegisteredReservoirs()` | 无 | List\<IReservoir\> | 获取所有已注册储层 |

返回的储层没有 `capacity` 和 `current`，需手动设置后才能添加到区块。可能返回 `null`，使用 `isNull()` 检查。

**注意：** 配置文件中的储层在模组 init 阶段注册，可能早于 CraftTweaker 脚本加载。建议使用 ZenUtils 的自定义入口点。