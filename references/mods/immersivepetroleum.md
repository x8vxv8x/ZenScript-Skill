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