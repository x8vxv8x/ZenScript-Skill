# Zen: Foundry CraftTweaker API 参考

> Mod ID: `foundry`
> 前置条件: 无
> 导入: `import mods.foundry.<ClassName>;`

## API 列表

### AlloyMixer (合金混合机)

> `import mods.foundry.AlloyMixer;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, ILiquidStack[] inputs)` | void | 添加合金混合配方，最多4种输入液体 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(ILiquidStack[] inputs)` | void | 移除指定输入的配方 |
| `.clear()` | void | 清除所有配方 |

### AlloyingCrucible (合金坩埚)

> `import mods.foundry.AlloyingCrucible;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, ILiquidStack input_a, ILiquidStack input_b)` | void | 添加合金坩埚配方，2种输入液体 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(ILiquidStack input_a, ILiquidStack input_b)` | void | 移除指定输入的配方 |
| `.clear()` | void | 清除所有配方 |

### BurnerHeater (燃烧加热器)

> `import mods.foundry.BurnerHeater;`

#### 添加燃料方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(IIngredient fuel, int time, int heat)` | void | 添加燃烧器燃料，time 为燃烧时间，heat 为提供温度 |

#### 移除燃料方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeFuel(IItemStack stack)` | void | 移除指定燃料 |
| `.clear()` | void | 清除所有燃料 |

### Casting (金属铸造)

> `import mods.foundry.Casting;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, ILiquidStack input, IItemStack mold, @Optional IIngredient extra, @Optional int ticks, @Optional boolean consumesMold)` | void | 添加金属铸造配方，mold 为模具，extra 为额外物品，ticks 为时间，consumesMold 为是否消耗模具 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(ILiquidStack input, IItemStack mold, @Optional IItemStack extra)` | void | 移除指定输入和模具的配方 |
| `.clear()` | void | 清除所有配方 |

### CastingTable (铸造台)

> `import mods.foundry.CastingTable;`

#### 添加配方方法（替换 X 为 Block、Ingot、Plate 或 Rod）
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addXRecipe(IItemStack output, ILiquidStack input)` | void | 添加指定类型铸造台配方 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeXRecipe(ILiquidStack input)` | void | 移除指定类型铸造台配方 |
| `.clearXs()` | void | 清除指定类型所有配方 |
| `.clearAll()` | void | 清除所有类型所有配方 |

### FluidHeater (流体加热器)

> `import mods.foundry.FluidHeater;`

#### 添加燃料方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFuel(ILiquidDefinition fuel, @Optional int heat)` | void | 添加流体加热器燃料，heat 为温度 |

#### 移除燃料方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeFuel(ILiquidDefinition liquid)` | void | 移除指定燃料 |
| `.clear()` | void | 清除所有燃料 |

### Heating (热源)

> `import mods.foundry.Heating;`

#### 添加热源方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addStateSource(IBlockState state, int heat)` | void | 添加方块状态作为热源，heat 为温度 |

### Infuser (金属注入机)

> `import mods.foundry.Infuser;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, ILiquidStack input, IIngredient substance, int energy)` | void | 添加金属注入配方，substance 为注入物质，energy 为所需能量 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(ILiquidStack input, IItemStack substance)` | void | 移除指定输入和物质的配方 |
| `.clear()` | void | 清除所有配方 |

### Melting (熔炼坩埚)

> `import mods.foundry.Melting;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, IIngredient input, @Optional int meltingPoint, @Optional int speed)` | void | 添加熔炼配方，meltingPoint 为熔点（K），speed 为熔炼速度 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack input)` | void | 移除指定输入的配方 |
| `.clear()` | void | 清除所有配方 |

### MoldStation (模具站)

> `import mods.foundry.MoldStation;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, int width, int height, int[] grid)` | void | 添加模具配方，width/height 为网格尺寸，grid 为网格数据 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(int[] grid)` | void | 移除指定网格的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.clear()` | void | 清除所有配方 |