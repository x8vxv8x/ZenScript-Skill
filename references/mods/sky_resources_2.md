# Sky Resources 2 CraftTweaker API 参考

> Mod ID: `skyresources`
> 前置条件: 无
> 导入: `import mods.skyresources.<ClassName>;`

## API 列表

### fusion (炼金灌注台)

> `import mods.skyresources.fusion;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack[] input, float catalystUsedPerCraft)` | void | 添加炼金配方，catalystUsedPerCraft 为每次合成消耗的催化剂数量 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的炼金配方 |

### catalysts (炼金融合催化剂)

> `import mods.skyresources.catalysts;`

#### 添加催化剂方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack stack, float value)` | void | 添加催化剂及其值 |

#### 移除催化剂方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(IItemStack output)` | void | 移除指定物品的催化剂 |

### cauldronclean (炼药锅清洗)

> `import mods.skyresources.cauldronclean;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input)` | void | 添加炼药锅清洗配方 |
| `.addRecipe(IItemStack output, IItemStack input, float chance)` | void | 添加炼药锅清洗配方，chance 为成功概率 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的清洗配方 |

### combustion (氧化加热器)

> `import mods.skyresources.combustion;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack[] input, int temperature)` | void | 添加配方，temperature 为所需温度 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |

### condenser (冷凝器)

> `import mods.skyresources.condenser;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, int tickTime, IItemStack catalyst, ILiquidStack inputFluid)` | void | 添加冷凝器配方，tickTime 为处理时间，catalyst 为催化剂，inputFluid 为输入流体 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的冷凝器配方 |

### crucible (坩埚)

> `import mods.skyresources.crucible;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(ILiquidStack output, IItemStack input)` | void | 添加坩埚配方，将物品熔炼为流体 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(ILiquidStack output)` | void | 移除指定输出的坩埚配方 |

### knife (切割刀)

> `import mods.skyresources.knife;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input)` | void | 添加切割刀配方 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的切割刀配方 |

### freezer (冰箱)

> `import mods.skyresources.freezer;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input, int ticks)` | void | 添加冷冻配方，ticks 为处理时间（tick） |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的冷冻配方 |

### heatsources (热源)

> `import mods.skyresources.heatsources;`

#### 添加热源方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack stack, int heatValue)` | void | 添加热源方块及其热值，仅对方块形式的物品有效 |

#### 移除热源方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.remove(IItemStack output)` | void | 移除指定物品的热源 |

### infusion (生命灌注)

> `import mods.skyresources.infusion;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack inputStack, IItemStack inputBlock, int health)` | void | 添加生命灌注配方，health 为所需生命值 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的生命灌注配方 |

### rockgrinder (岩石研磨机)

> `import mods.skyresources.rockgrinder;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IItemStack input)` | void | 添加岩石研磨配方 |
| `.addRecipe(IItemStack output, IItemStack input, float chance)` | void | 添加岩石研磨配方，chance 为成功概率 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的岩石研磨配方 |

### waterextractor (水提取器)

> `import mods.skyresources.waterextractor;`

#### Extract 提取方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.extract.addRecipe(int waterOut, IItemStack output, IIngredient input)` | void | 添加水提取器提取配方，waterOut 为产出水量 |

#### Insert 注入方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.insert.addRecipe(IItemStack output, IIngredient input, int waterIn)` | void | 添加水提取器注入配方，waterIn 为输入水量 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.extract.removeRecipe(int waterOut, IItemStack output, IIngredient input)` | void | 移除指定的提取配方 |
| `.insert.removeRecipe(IItemStack output)` | void | 移除指定输出的注入配方 |