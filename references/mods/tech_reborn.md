# Tech Reborn CraftTweaker API 参考

> Mod ID: `techreborn`
> 前置条件: 无
> 导入: `import mods.techreborn.<ClassName>;`

## API 列表

### alloySmelter (合金炉)

> `import mods.techreborn.alloySmelter;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input1, IIngredient input2, int ticktime, int euTick)` | void | 添加合金冶炼配方，ticktime 为处理时间，euTick 为每tick消耗EU |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredientA, IIngredient ingredientB)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### assemblingMachine (装配机)

> `import mods.techreborn.assemblingMachine;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input1, IIngredient input2, int ticktime, int euTick)` | void | 添加组装机配方，ticktime 为处理时间，euTick 为每tick消耗EU |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredientA, IIngredient ingredientB)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### blastFurnace (工业高炉)

> `import mods.techreborn.blastFurnace;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output1, IItemStack output2, IIngredient input1, IIngredient input2, int ticktime, int euTick, int neededHeat)` | void | 添加工业高炉配方，neededHeat 为所需热度 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredient)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### centrifuge (离心机)

> `import mods.techreborn.centrifuge;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output1, IItemStack output2, IItemStack output3, IItemStack output4, IIngredient input1, IIngredient input2, int ticktime, int euTick)` | void | 添加离心机配方，最多4个输出 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient iIngredient)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### chemicalReactor (化学反应器)

> `import mods.techreborn.chemicalReactor;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output1, IIngredient input1, IIngredient input2, int ticktime, int euTick)` | void | 添加化学反应器配方，ticktime 为处理时间，euTick 为每tick消耗EU |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredient)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### compressor (压缩机)

> `import mods.techreborn.compressor;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output1, IIngredient input1, int ticktime, int euTick)` | void | 添加压缩机配方，ticktime 为处理时间，euTick 为每tick消耗EU |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredient)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### distillationTower (蒸馏塔)

> `import mods.techreborn.distillationTower;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output1, IItemStack output2, IItemStack output3, IItemStack output4, IIngredient input1, IIngredient input2, int ticktime, int euTick)` | void | 添加蒸馏塔配方，最多4个输出 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredient)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### extractor (提取机)

> `import mods.techreborn.extractor;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input1, int ticktime, int euTick)` | void | 添加提取配方，ticktime 为处理时间，euTick 为每tick消耗EU |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredient)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### fluidGen (流体发电机)

> `import mods.techreborn.fluidGen;`

#### 添加燃料方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addThermalFluid(ILiquidStack fluid, int energyPerMb)` | void | 添加热力发电机流体燃料 |
| `.addGasFluid(ILiquidStack fluid, int energyPerMb)` | void | 添加燃气发电机流体燃料 |
| `.addSemiFluid(ILiquidStack fluid, int energyPerMb)` | void | 添加半流体发电机流体燃料 |
| `.addDieselFluid(ILiquidStack fluid, int energyPerMb)` | void | 添加柴油发电机流体燃料 |
| `.addPlasmaFluid(ILiquidStack fluid, int energyPerMb)` | void | 添加等离子发电机流体燃料 |

#### 移除燃料方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeThermalFluid(ILiquidStack fluid)` | void | 移除热力发电机流体燃料 |
| `.removeGasFluid(ILiquidStack fluid)` | void | 移除燃气发电机流体燃料 |
| `.removeSemiFluid(ILiquidStack fluid)` | void | 移除半流体发电机流体燃料 |
| `.removeDieselFluid(ILiquidStack fluid)` | void | 移除柴油发电机流体燃料 |
| `.removePlasmaFluid(ILiquidStack fluid)` | void | 移除等离子发电机流体燃料 |

### fluidReplicator (流体复制机)

> `import mods.techreborn.fluidReplicator;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(int input, ILiquidStack output, int ticks, int euPerTick)` | void | 添加流体复制配方，input 为输入量，ticks 为处理时间，euPerTick 为每tick消耗EU |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(ILiquidStack fluid)` | void | 移除指定输出的配方 |

### fusionReactor (聚变反应堆)

> `import mods.techreborn.fusionReactor;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IIngredient topInput, IIngredient bottomInput, IItemStack output, int startEU, int euTick, int tickTime)` | void | 添加聚变反应堆配方，startEU 为启动EU，euTick 为每tick消耗EU，tickTime 为处理时间 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeTopInputRecipe(IIngredient iIngredient)` | void | 移除指定顶部输入的配方 |
| `.removeBottomInputRecipe(IIngredient iIngredient)` | void | 移除指定底部输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### grinder (磨粉机)

> `import mods.techreborn.grinder;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input1, int ticktime, int euTick)` | void | 添加研磨机配方，ticktime 为处理时间，euTick 为每tick消耗EU |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredient)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### implosionCompressor (聚爆压缩机)

> `import mods.techreborn.implosionCompressor;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output1, IItemStack output2, IIngredient input1, IIngredient input2, int ticktime, int euTick)` | void | 添加配方，ticktime 为处理时间，euTick 为每tick消耗EU |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredient)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### industrialElectrolyzer (工业电解器)

> `import mods.techreborn.industrialElectrolyzer;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output1, IItemStack output2, IItemStack output3, IItemStack output4, IIngredient cells, IIngredient input2, int ticktime, int euTick)` | void | 添加工业电解配方，最多4个输出 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredient)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### industrialGrinder (工业磨粉机)

> `import mods.techreborn.industrialGrinder;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output1, IItemStack output2, IItemStack output3, IItemStack output4, IIngredient input1, IIngredient input2, int ticktime, int euTick)` | void | 添加配方（无流体），最多4个输出 |
| `.addRecipe(IItemStack output1, IItemStack output2, IItemStack output3, IItemStack output4, IIngredient input1, IIngredient input2, ILiquidStack fluid, int ticktime, int euTick)` | void | 添加配方（含流体），最多4个输出 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredient)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### industrialSawmill (工业锯木机)

> `import mods.techreborn.industrialSawmill;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output1, IItemStack output2, IItemStack output3, IIngredient input1, ILiquidStack fluid, int ticktime, int euTick)` | void | 添加工业锯木机配方（含流体），最多3个输出 |
| `.addRecipe(IItemStack output1, IItemStack output2, IItemStack output3, IIngredient input1, int ticktime, int euTick)` | void | 添加工业锯木机配方（无流体），最多3个输出 |
| `.addRecipe(IItemStack output1, IItemStack output2, IItemStack output3, IIngredient input1, int ticktime, int euTick, boolean useOreDic)` | void | 添加工业锯木机配方（无流体，指定矿辞），最多3个输出 |
| `.addRecipe(IItemStack output1, IItemStack output2, IItemStack output3, IIngredient input1, ILiquidStack fluid, int ticktime, int euTick, boolean useOreDic)` | void | 添加工业锯木机配方（含流体，指定矿辞），最多3个输出 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredient)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### plateBendingMachine (卷板机)

> `import mods.techreborn.plateBendingMachine;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output1, IIngredient input1, int ticktime, int euTick)` | void | 添加配方，ticktime 为处理时间，euTick 为每tick消耗EU |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### rollingMachine (辊压机)

> `import mods.techreborn.rollingMachine;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addShaped(IItemStack output, IIngredient[][] ingredients)` | void | 添加有序合成配方 |
| `.addShapeless(IItemStack output, IIngredient[] ingredients)` | void | 添加无序合成配方 |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### scrapbox (废料拆包机)

> `import mods.techreborn.scrapbox;`

#### 添加掉落物方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addScrapboxDrop(IIngredient input)` | void | 添加掉落物 |

#### 移除掉落物方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的掉落物 |
| `.removeAll()` | void | 移除所有掉落物 |

### solidCanningMachine (固体装罐机)

> `import mods.techreborn.solidCanningMachine;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output1, IIngredient input1, IIngredient input2, int ticktime, int euTick)` | void | 添加固体装罐机配方，ticktime 为处理时间，euTick 为每tick消耗EU |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### vacuumFreezer (真空冷凝器)

> `import mods.techreborn.vacuumFreezer;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output, IIngredient input, int ticktime, int euTick)` | void | 添加配方，ticktime 为处理时间，euTick 为每tick消耗EU |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeInputRecipe(IIngredient ingredient)` | void | 移除指定输入的配方 |
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |

### wireMill (线材轧机)

> `import mods.techreborn.wireMill;`

#### 添加配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipe(IItemStack output1, IIngredient input1, int ticktime, int euTick)` | void | 添加线材轧机配方，ticktime 为处理时间，euTick 为每tick消耗EU |

#### 移除配方方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.removeRecipe(IItemStack output)` | void | 移除指定输出的配方 |
| `.removeAll()` | void | 移除所有配方 |