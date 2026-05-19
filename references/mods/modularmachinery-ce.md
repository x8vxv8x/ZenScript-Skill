# Modular Machinery: Community Edition CraftTweaker API 参考

> 模块化机械：社区版（MMCE），与原版模块化机械是不同的模组。必须向用户询问已安装模组的类型！
> Mod ID: `modularmachinery`
> 前置条件: 无
> 导入: `import mods.modularmachinery.RecipeBuilder;` / `import mods.modularmachinery.RecipePrimer;`

## API 列表

### RecipeBuilder

> `import mods.modularmachinery.RecipeBuilder;`

用于创建 RecipePrimer 对象。

#### 创建方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.newBuilder(String recipeRegistryName, String associatedMachineRegistryName, int processingTickTime)` | RecipePrimer | 创建新的配方对象。recipeRegistryName=配方名，单个机器内不能重复；associatedMachineRegistryName=机械注册名；processingTickTime=工作时间（tick） |
| `.newBuilder(String recipeRegistryName, String associatedMachineRegistryName, int processingTickTime, int sortingPriority)` | RecipePrimer | 创建新的配方对象，带排序优先级（值越小优先级越高） |
| `.newBuilder(String recipeRegistryName, String associatedMachineRegistryName, int processingTickTime, int sortingPriority, boolean cancelIfPerTickFails)` | RecipePrimer | 创建新的配方对象。cancelIfPerTickFails=运行时失败（如跳电）是否强制取消配方（吞材料） |

### RecipePrimer

> `import mods.modularmachinery.RecipePrimer;`

配方对象，支持链式调用（每个方法返回自身）。

#### 通用输入输出

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addInput(IIngredient input)` | RecipePrimer | 添加材料输入，可以是物品、流体或矿辞，不支持气体 |
| `.addOutput(IIngredient input)` | RecipePrimer | 添加材料输出，可以是物品、流体或矿辞，不支持气体 |
| `.addInputs(IIngredient... input)` | RecipePrimer | 添加多种材料输入，支持数组写法 |
| `.addOutputs(IIngredient... input)` | RecipePrimer | 添加多种材料输出，支持数组写法 |

#### 物品输入输出

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addItemInput(IIngredient input)` | RecipePrimer | 添加物品输入，支持 withTag()，可以是物品或矿辞 |
| `.addItemOutput(IIngredient input)` | RecipePrimer | 添加物品输出，支持 withTag()，可以是物品或矿辞 |
| `.addItemInputs(IIngredient... input)` | RecipePrimer | 添加多种物品输入，支持数组写法 |
| `.addItemOutputs(IIngredient... input)` | RecipePrimer | 添加多种物品输出，支持数组写法 |

#### 流体输入输出

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFluidInput(ILiquidStack stack)` | RecipePrimer | 添加流体输入 |
| `.addFluidOutput(ILiquidStack stack)` | RecipePrimer | 添加流体输出 |
| `.addFluidInputs(ILiquidStack... stacks)` | RecipePrimer | 添加多种流体输入，支持数组写法 |
| `.addFluidOutputs(ILiquidStack... stacks)` | RecipePrimer | 添加多种流体输出，支持数组写法 |

#### 气体输入输出（需安装通用机械）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addGasInput(String gasName, int amount)` | RecipePrimer | 添加气体输入。gasName=气体名，amount=数量（mb） |
| `.addGasOutput(String gasName, int amount)` | RecipePrimer | 添加气体输出。gasName=气体名，amount=数量（mb） |

#### 能量输入输出

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addEnergyPerTickInput(long perTick)` | RecipePrimer | 添加每 tick 能量输入。总能量=配方时间×每tick能量。最大值为 long 上限 |
| `.addEnergyPerTickOutput(long perTick)` | RecipePrimer | 添加每 tick 能量输出。总能量=配方时间×每tick能量。最大值为 long 上限 |

#### 概率设置

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setChance(float chance)` | RecipePrimer | 设置输出概率，1.0=100%，0.0=0%。只能在添加物品/流体之后调用。多种输入输出（addInputs/addOutputs）不支持设置概率 |

#### 组件 Tag 匹配

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setTag(String selectorTag)` | RecipePrimer | 设置组件 Tag 匹配（高级功能），允许指定物品的输入输出仓。这不是 NBT，使用 withTag() 设置 NBT |

#### 并行化设置

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setParallelized(boolean parallelized)` | RecipePrimer | 设置此配方是否允许并行化 |
| `.setParallelizeUnaffected(boolean unaffected)` | RecipePrimer | 设置是否不受并行影响（如催化剂、编程电路等固定消耗的物品） |

#### 材料组输入

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addIngredientArrayInput(IngredientArrayBuilder builder)` | RecipePrimer | 添加物品组输入，机器只会消耗其中一种物品 |

#### 催化剂输入

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addCatalystInput(IIngredient input, String[] tooltips, RecipeModifierBuilder[] modifiers)` | RecipePrimer | 添加催化剂输入（可选输入），当检测到催化剂时给配方添加 RecipeModifier |

#### NBT 相关

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setPreViewNBT(IData nbt)` | RecipePrimer | 设置配方预览时显示的 NBT，不影响实际配方 NBT 匹配 |
| `.setNBTChecker(IMachineController controller, AdvancedItemNBTChecker checker)` | RecipePrimer | 设置自定义 NBT 检查器（仅限物品类型输入），返回 bool |
| `.addItemModifier(IMachineController controller, AdvancedItemModifier modifier)` | RecipePrimer | 设置自定义物品修改器（仅限物品类型输入输出），返回 IItemStack |

#### 提示信息

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addRecipeTooltip(String... tooltips)` | RecipePrimer | 添加 JEI 提示信息，支持多行 |

#### 线程设置（工厂系统）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setThreadName(String name)` | RecipePrimer | 设置配方只能在指定名称的线程中运行 |
| `.setMaxThreads(int maxThreads)` | RecipePrimer | 设置配方最大线程数 |

#### 智能数据接口

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addSmartInterfaceDataInput(String type, int minValue, int maxValue)` | RecipePrimer | 添加智能数据接口输入 |

#### 事件处理器

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addCheckHandler(IEventHandler<RecipeCheckEvent> handler)` | RecipePrimer | 添加配方检查事件监听器（旧版，建议使用 addPreCheckHandler/addPostCheckHandler） |
| `.addPreCheckHandler(IEventHandler<RecipeCheckEvent> handler)` | RecipePrimer | 添加配方预检查事件监听器 |
| `.addPostCheckHandler(IEventHandler<RecipeCheckEvent> handler)` | RecipePrimer | 添加配方后检查事件监听器 |
| `.addStartHandler(IEventHandler<RecipeStartEvent> handler)` | RecipePrimer | 添加配方开始事件监听器 |
| `.addPreTickHandler(IEventHandler<RecipeTickEvent> handler)` | RecipePrimer | 添加配方预 Tick 事件监听器（每个 Tick 触发，在能量消耗前） |
| `.addPostTickHandler(IEventHandler<RecipeTickEvent> handler)` | RecipePrimer | 添加配方后 Tick 事件监听器（每个 Tick 触发，在能量消耗后） |
| `.addFinishHandler(IEventHandler<RecipeFinishEvent> handler)` | RecipePrimer | 添加配方完成事件监听器 |
| `.addFactoryStartHandler(IEventHandler<FactoryRecipeStartEvent> handler)` | RecipePrimer | 添加工厂配方开始事件监听器 |
| `.addFactoryFinishHandler(IEventHandler<FactoryRecipeFinishEvent> handler)` | RecipePrimer | 添加工厂配方完成事件监听器 |

#### 构建

| 方法 | 返回 | 说明 |
|------|------|------|
| `.build()` | void | 构建并注册配方。必须调用此方法配方才会生效 |

### IngredientArrayBuilder

> `import mods.modularmachinery.IngredientArrayBuilder;`

用于创建材料组。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.newBuilder()` | IngredientArrayBuilder | 创建新的材料组构建器 |
| `.addIngredient(IIngredient input)` | IngredientArrayBuilder | 添加单个材料（物品或矿辞） |
| `.addIngredients(IIngredient... inputs)` | IngredientArrayBuilder | 添加多个材料 |
| `.addChancedIngredient(IIngredient input, float chance)` | IngredientArrayBuilder | 添加带独立概率的材料 |
| `.build()` | IngredientArrayPrimer | 构建材料组（可选调用） |

### RecipeModifierBuilder

> `import mods.modularmachinery.RecipeModifierBuilder;`

用于构建 RecipeModifier，动态修改配方输入输出。

#### 创建方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.newBuilder()` | RecipeModifierBuilder | 创建新的构建器（Builder 模式） |
| `.create(String type, String ioTypeStr, float value, int operation, boolean affectChance)` | RecipeModifierBuilder | 快速构建。type=类型；ioTypeStr="input"/"output"；value=数值；operation=0加/1乘；affectChance=是否应用到概率 |

#### Builder 模式方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setRequirementType(String type)` | RecipeModifierBuilder | 设置应用类型（如 "modularmachinery:energy"） |
| `.setIOType(String ioTypeStr)` | RecipeModifierBuilder | 设置应用到输入还是输出（"input"/"output"） |
| `.setOperation(int operation)` | RecipeModifierBuilder | 设置计算方式（0=加，1=乘，默认0） |
| `.setValue(float value)` | RecipeModifierBuilder | 设置数值 |
| `.isAffectChance(boolean affectChance)` | RecipeModifierBuilder | 是否应用到概率 |
| `.build()` | RecipeModifier | 构建 RecipeModifier |

#### 类型常量

| 类型 | 说明 |
|------|------|
| `modularmachinery:duration` | 工作时间 |
| `modularmachinery:energy` | 能量 |
| `modularmachinery:item` | 物品 |
| `modularmachinery:fluid` | 流体 |
| `modularmachinery:aspect` | 源质（神秘时代） |
| `modularmachinery:aura` | 气场（自然灵气） |
| `modularmachinery:lifeessence` | 生命源质（血魔法） |
| `modularmachinery:starlight` | 星能（星辉魔法） |
| `modularmachinery:mana` | 魔力（植物魔法） |
| `modularmachinery:impetus` | 元动能量 |

### RecipeAdapterBuilder

> `import mods.modularmachinery.RecipeAdapterBuilder;`

用于复制其他机械的所有配方，支持微调配方内容。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(String targetMachine, String sourceMachine)` | RecipeAdapterBuilder | 创建适配器，将 sourceMachine 的所有配方复制到 targetMachine |
| `.addModifier(RecipeModifier modifier)` | RecipeAdapterBuilder | 添加配方修改器 |
| `.addFluidInput(ILiquidStack stack)` | RecipeAdapterBuilder | 添加额外流体输入（RecipeBuilder/RecipePrimer 的大部分方法都可用） |
| `.build()` | void | 构建并注册适配器 |

#### 内置模组配方支持

| 适配器 ID | 需要模组 | 说明 |
|-----------|----------|------|
| `minecraft:furnace` | 无 | 复制熔炉配方，产物经验写入 customData 的 "experience" |
| `ic2:te_compressor` | IC2 | 复制 IC2 压缩机配方 |
| `tconstruct:smeltery_alloy` | 匠魂2 | 复制匠魂2合金配方 |
| `tconstruct:smeltery_melting` | 匠魂2 | 复制匠魂2冶炼配方，温度写入 customData 的 "temperatureRequired" |
| `nuclearcraft:alloy_furnace` | 核电工艺 | 复制核电工艺合金炉配方 |
| `nuclearcraft:chemical_reactor` | 核电工艺 | 复制核电工艺化学反应器配方 |
| `nuclearcraft:infuser` | 核电工艺 | 复制核电工艺流体注入器配方 |
| `nuclearcraft:melter` | 核电工艺 | 复制核电工艺融化机配方 |

### MachineModifier

> `import mods.modularmachinery.MachineModifier;`

用于修改机械属性的静态方法类。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setParallelizable(String machineName, boolean parallelizable)` | void | 启用/禁用机械并行化（需 MMCE R56+） |
| `.setMaxParallelism(String machineName, int parallelism)` | void | 设置机械最大并行数 |
| `.setInternalParallelism(String machineName, int parallelism)` | void | 设置机械内置并行数（不可配置的并行来源） |
| `.setMachineGeoModel(String machineName, String modelName)` | void | 为机械绑定自定义 GeckoLib 模型 |
| `.setMaxThreads(String machineName, int maxThreads)` | void | 设置工厂机械最大线程数 |
| `.addCoreThread(String machineName, FactoryRecipeThread thread)` | void | 为工厂机械添加核心线程 |

### MachineBuilder

> `import mods.modularmachinery.MachineBuilder;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getBuilder(String machineName)` | MachineBuilder | 获取机械构建器 |
| `.setParallelizable(boolean parallelizable)` | MachineBuilder | 设置是否启用并行化 |
| `.setMaxParallelism(int parallelism)` | MachineBuilder | 设置最大并行数 |
| `.setInternalParallelism(int parallelism)` | MachineBuilder | 设置内置并行数 |

### FactoryRecipeThread

> `import mods.modularmachinery.FactoryRecipeThread;`

工厂配方线程。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createCoreThread(String name)` | FactoryRecipeThread | 创建核心线程 |
| `.addRecipe(String recipeName)` | FactoryRecipeThread | 限制线程只能运行指定配方 |

### IMachineController

> 通过机械事件获取，提供对控制器的操作。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `world` | IWorld | 控制器所在世界 |
| `blockState` | IBlockState | 控制器方块状态 |
| `pos` | IBlockPos | 控制器位置 |
| `ticksExisted` | int | 机械在当前世界运行的时间（非世界时间，进入退出世界会被重置） |
| `activeRecipeList` | ActiveMachineRecipe[] | 正在运行的配方列表。普通机械返回大小为1的数组（内容可能null），工厂返回任意大小（内容非null） |
| `isWorking` | boolean | 机器是否在运行 |
| `formedMachineName` | String | 机械结构注册名（如 "modularmachinery:machine_1"），未形成结构返回 null |
| `customData` | IData | 自定义数据，可用于存储数据，游戏关闭时保存在 NBT |
| `smartInterfaceDataList` | SmartInterfaceData[] | 绑定的所有智能数据接口数据，无则为空数组 |
| `foundModifiers` | String[] | 找到的机械升级注册名数组 |
| `recipeThreadList` | FactoryRecipeThread[] | 工厂配方线程列表 |

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `customData` | IData | 自定义数据，修改后需要调用 setter 同步 |
| `statusMessage` | String | 覆盖控制器当前的状态消息 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addModifier(String key, RecipeModifier modifier)` | void | 添加自定义名称的 RecipeModifier，同步到正在运行的配方 |
| `.removeModifier(String key)` | void | 删除对应名称的 RecipeModifier |
| `.hasModifier(String key)` | boolean | 检查是否存在对应名称的 RecipeModifier |
| `.getSmartInterfaceData(String type)` | SmartInterfaceData | 获取指定类型的智能数据接口数据，可能返回 null |
| `.hasModifierReplacement(String modifierName)` | boolean | 检查是否已找到指定注册名的机械升级 |

### SmartInterfaceData

智能数据接口数据。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `type` | String | 数据类型 |
| `value` | int | 数据值 |

### GeoMachineModel

> `import mods.modularmachinery.GeoMachineModel;`

用于注册 GeckoLib 自定义模型。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.registerGeoMachineModel(String name, String geoPath, String texturePath, String animationPath)` | void | 注册模型。name=模型名称；geoPath=模型文件路径；texturePath=贴图路径；animationPath=动画路径 |

### MachineUpgradeBuilder

> `import mods.modularmachinery.MachineUpgradeBuilder;`

用于创建机械升级（需 MMCE R39+）。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.newBuilder(String name, String localizedName, int level, int maxStack)` | MachineUpgradeBuilder | 创建升级。name 必须唯一；level 暂无作用 |
| `.addDescriptions(String... descriptions)` | MachineUpgradeBuilder | 添加固定工具提示 |
| `.setBusGUIDescriptionHandler(IFunction<SimpleMachineUpgrade, String[]> handler)` | MachineUpgradeBuilder | 添加升级总线提示的事件监测 |
| `.addCompatibleMachines(String... machineNames)` | MachineUpgradeBuilder | 添加白名单机械（与黑名单冲突） |
| `.addIncompatibleMachines(String... machineNames)` | MachineUpgradeBuilder | 添加黑名单机械（与白名单冲突） |
| `.addRecipeCheckHandler(UpgradeEventHandlerCT handler)` | MachineUpgradeBuilder | 添加配方检查事件 |
| `.addRecipeStartHandler(UpgradeEventHandlerCT handler)` | MachineUpgradeBuilder | 添加配方开始事件 |
| `.addRecipePreTickHandler(UpgradeEventHandlerCT handler)` | MachineUpgradeBuilder | 添加配方预 Tick 事件 |
| `.addRecipePostTickHandler(UpgradeEventHandlerCT handler)` | MachineUpgradeBuilder | 添加配方后 Tick 事件 |

### MachineUpgradeHelper

> `import mods.modularmachinery.MachineUpgradeHelper;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addFixedUpgrade(IItemStack itemStack, String upgradeName)` | void | 绑定物品到升级，使物品可作为升级装入升级总线 |
| `.castToSimpleDynamicMachineUpgrade(MachineUpgrade upgrade)` | SimpleDynamicMachineUpgrade | 将 MachineUpgrade 转换为 SimpleDynamicMachineUpgrade |

### MMEvents

> `import mods.modularmachinery.MMEvents;`

机械事件注册类。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.onStructureFormed(String machineName, IEventHandler<MachineStructureFormedEvent> handler)` | void | 注册结构形成事件 |
| `.onMachinePreTick(String machineName, IEventHandler<MachineTickEvent> handler)` | void | 注册机械预 Tick 事件 |
| `.onMachinePostTick(String machineName, IEventHandler<MachineTickEvent> handler)` | void | 注册机械后 Tick 事件 |
| `.onMachineTick(String machineName, IEventHandler<MachineTickEvent> handler)` | void | 注册机械 Tick 事件（结构形成后每 Tick 触发） |
| `.onControllerGUIRender(String machineName, IEventHandler<ControllerGUIRenderEvent> handler)` | void | 注册控制器 GUI 渲染事件 |
| `.onSmartInterfaceUpdate(String machineName, IEventHandler<SmartInterfaceUpdateEvent> handler)` | void | 注册智能数据接口更新事件 |
| `.onControllerModelAnimation(String machineName, IEventHandler<ControllerModelAnimationEvent> handler)` | void | 注册控制器模型动画事件 |
| `.onControllerModelGet(String machineName, IEventHandler<ControllerModelGetEvent> handler)` | void | 注册控制器模型获取事件（动态模型切换） |
| `.onStructureUpdate(String machineName, IEventHandler<MachineStructureUpdateEvent> handler)` | void | 注册结构更新事件 |

## 事件类

### 通用事件 ZenGetter

所有配方事件通用：

| 属性 | 类型 | 说明 |
|------|------|------|
| `activeRecipe` | ActiveMachineRecipe | 事件对应的机械配方 |
| `controller` | IMachineController | 触发事件的机械控制器 |

所有机械事件通用：

| 属性 | 类型 | 说明 |
|------|------|------|
| `controller` | IMachineController | 触发事件的机械控制器 |

### RecipeCheckEvent

> `import mods.modularmachinery.RecipeCheckEvent;`

配方检查事件，在机械扫描配方并满足运行条件时触发。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setFailed(String reason)` | void | 设置配方检查失败，阻止配方运行，支持本地化字符串 |

### RecipeStartEvent / FactoryRecipeStartEvent

> `import mods.modularmachinery.RecipeStartEvent;`
> `import mods.modularmachinery.FactoryRecipeStartEvent;`

配方开始事件，在机械运行配方后触发。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addModifier(String name, RecipeModifier modifier)` | void | 添加临时修改器（配方结束时删除） |
| `.addPermanentModifier(String name, RecipeModifier modifier)` | void | 添加永久修改器（核心线程和控制器可用） |

工厂版本特有：

| 属性 | 类型 | 说明 |
|------|------|------|
| `factoryRecipeThread` | FactoryRecipeThread | 触发事件的线程 |

### RecipePreTickEvent / RecipePostTickEvent

> `import mods.modularmachinery.RecipeTickEvent;`

配方 Tick 事件，每个 Tick 触发。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.preventProgressing(String reason)` | void | 阻止机器增加进度（仍会 Tick 并消耗能量），原因显示在控制器上 |
| `.setFailed(boolean destructRecipe, String reason)` | void | 设置运行失败。destructRecipe=true 时取消运行配方（吞材料） |

### RecipeFinishEvent / FactoryRecipeFinishEvent

> `import mods.modularmachinery.RecipeFinishEvent;`
> `import mods.modularmachinery.FactoryRecipeFinishEvent;`

配方完成事件，配方完成后触发一次。

### MachineStructureFormedEvent

> `import mods.modularmachinery.MachineStructureFormedEvent;`

机械结构形成事件。

### MachineTickEvent

> `import mods.modularmachinery.MachineTickEvent;`

机械 Tick 事件，结构形成后每 Tick 触发。

### ControllerGUIRenderEvent

> `import mods.modularmachinery.ControllerGUIRenderEvent;`

控制器 GUI 渲染事件（客户端），允许添加自定义信息。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `extraInfo` | String[] | 额外信息数组 |

### SmartInterfaceUpdateEvent

> `import mods.modularmachinery.SmartInterfaceUpdateEvent;`

智能数据接口更新事件。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `interfacePos` | IBlockPos | 触发事件的智能数据接口位置 |
| `newData` | SmartInterfaceData | 更新的数据 |

### ControllerModelAnimationEvent

> `import mods.modularmachinery.ControllerModelAnimationEvent;`

控制器模型动画事件。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addAnimation(String animationName)` | void | 添加动画（只播放一次） |
| `.addAnimation(String animationName, boolean loop)` | void | 添加动画并设置是否循环 |
| `.setAnimation(String animationName)` | void | 设置动画（覆盖先前所有动画） |
| `.setAnimation(String animationName, boolean loop)` | void | 设置动画并设置是否循环（覆盖先前所有动画） |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `currentModelName` | String | 当前模型注册名称 |
| `transitionLengthTicks` | double | 当前模型过渡长度（Tick） |
| `playState` | int | 动画运行状态（0=运行，其他=停止） |
| `currentAnimationName` | String | 当前运行的动画名称 |
| `animationSpeed` | double | 当前动画速度 |
| `animationTick` | double | 当前动画进度（Tick） |
| `animationState` | int | 动画状态（0=运行，1=切换中，2=停止中） |

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `transitionLengthTicks` | double | 设置过渡长度（Tick） |
| `playState` | int | 设置动画运行状态（0=运行，其他=停止） |

### ControllerModelGetEvent

> `import mods.modularmachinery.ControllerModelGetEvent;`

控制器模型获取事件，用于动态模型切换。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `modelName` | String | 模型名称，设置为未注册的名称会回滚至默认模型 |

## 咕咕工具扩展（需安装 gugu-utils）

> `import mods.guguutils.xxx;`

### 源质输入输出（神秘时代）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addAspcetInput(int amount, String aspectTag)` | RecipePrimer | 添加源质输入 |
| `.addAspectOutput(int amount, String aspectTag)` | RecipePrimer | 添加源质输出 |

### 压缩空气输入输出（气动工艺）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addCompressedAirInput(float pressure, int air)` | RecipePrimer | 添加压缩空气输入 |
| `.addCompressedAirOutput(float pressure, int air)` | RecipePrimer | 添加压缩空气输出 |
| `.addCompressedAirPerTickInput(float pressure, int air)` | RecipePrimer | 添加每 tick 压缩空气输入 |
| `.addCompressedAirPerTickOutput(float pressure, int air)` | RecipePrimer | 添加每 tick 压缩空气输出 |

### 魔力输入输出（植物魔法）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addManaInput(int mana)` | RecipePrimer | 添加魔力输入 |
| `.addManaOutput(int mana)` | RecipePrimer | 添加魔力输出 |
| `.addManaPerTickInput(int mana)` | RecipePrimer | 添加每 tick 魔力输入 |
| `.addManaPerTickOutput(int mana)` | RecipePrimer | 添加每 tick 魔力输出 |

## 使用示例

### 基础配方创建

```zenscript
import mods.modularmachinery.RecipeBuilder;
import mods.modularmachinery.RecipePrimer;

// 链式调用
RecipeBuilder.newBuilder("circuit_0", "machine_1", 80)
    .addEnergyPerTickInput(800)
    .addItemInputs([
        <ore:ingotOsmium> * 8,
        <mekanism:compressedredstone> * 1,
    ])
    .addItemOutput(<mekanism:controlcircuit> * 8)
    .build();

// 分步调用
val builder as RecipePrimer = RecipeBuilder.newBuilder("circuit_1", "machine_1", 80);
builder.addEnergyPerTickInput(800);
builder.addItemInput(<ore:ingotOsmium> * 8);
builder.addItemOutput(<mekanism:controlcircuit> * 8);
builder.build();
```

### 概率输出

```zenscript
RecipeBuilder.newBuilder("chance_test", "machine_1", 20)
    .addItemInput(<minecraft:diamond>)
    .addItemOutput(<minecraft:diamond_block>).setChance(0.3) // 30% 概率输出
    .addFluidOutput(<liquid:water>).setChance(1.0) // 100% 概率输出
    .build();
```

### 催化剂输入

```zenscript
import mods.modularmachinery.RecipeModifierBuilder;

RecipeBuilder.newBuilder("catalyst_test", "machine_1", 80)
    .addCatalystInput(<avaritia:resource:5>,
        ["无尽催化剂作为催化剂输入时，能量消耗降低 90%"],
        [RecipeModifierBuilder.create("modularmachinery:energy", "input", 0.1, 1, false)]
    )
    .addEnergyPerTickInput(1000)
    .addItemInput(<minecraft:diamond>)
    .addItemOutput(<minecraft:diamond_block>)
    .build();
```

### 材料组输入

```zenscript
import mods.modularmachinery.IngredientArrayBuilder;

RecipeBuilder.newBuilder("array_test", "machine_1", 80)
    .addIngredientArrayInput(
        IngredientArrayBuilder.newBuilder()
            .addIngredients([
                <ore:ingotStellarAlloy>,
                <ore:ingotGelidEnderium>,
                <ore:ingotBoundMetal> * 2,
            ])
        .build()
    )
    .addItemOutput(<minecraft:diamond>)
    .build();
```

### 配方适配器

```zenscript
import mods.modularmachinery.RecipeAdapterBuilder;
import mods.modularmachinery.RecipeModifierBuilder;

// 复制熔炉配方到自定义机械，时间减半，能量消耗5倍
RecipeAdapterBuilder.create("assembler_mk2", "minecraft:furnace")
    .addModifier(RecipeModifierBuilder.create("modularmachinery:duration", "input", 0.5, 1, false).build())
    .addModifier(RecipeModifierBuilder.create("modularmachinery:energy", "input", 5.0, 1, false).build())
    .addFluidInput(<liquid:ic2coolant> * 50)
    .build();
```

### 事件处理

```zenscript
import mods.modularmachinery.RecipeCheckEvent;
import mods.modularmachinery.RecipeFinishEvent;
import mods.modularmachinery.IMachineController;

RecipeBuilder.newBuilder("event_test", "machine_1", 80)
    .addEnergyPerTickInput(1000)
    .addItemInput(<minecraft:diamond>)
    .addItemOutput(<minecraft:diamond_block>)
    .addPreCheckHandler(function(event as RecipeCheckEvent) {
        val ctrl = event.controller;
        val data = ctrl.customData;
        val mana = isNull(data.mana) ? 0 : data.mana;
        if (mana < 100) {
            event.setFailed("魔力不够了喵");
        }
    })
    .addFinishHandler(function(event as RecipeFinishEvent) {
        // 配方完成时的操作
    })
    .build();
```

### 工厂系统（集成控制器）

```zenscript
import mods.modularmachinery.MachineModifier;
import mods.modularmachinery.FactoryRecipeThread;

// 设置最大线程数
MachineModifier.setMaxThreads("EC", 0);

// 添加核心线程并限制可运行的配方
MachineModifier.addCoreThread("EC", FactoryRecipeThread.createCoreThread("电量输入").addRecipe("EnergyInput"));
MachineModifier.addCoreThread("EC", FactoryRecipeThread.createCoreThread("电量输出").addRecipe("EnergyOutput"));
MachineModifier.addCoreThread("EC", FactoryRecipeThread.createCoreThread("能量聚合"));
```

### 自定义 GUI 信息

```zenscript
import mods.modularmachinery.MMEvents;
import mods.modularmachinery.ControllerGUIRenderEvent;

MMEvents.onControllerGUIRender("EC", function(event as ControllerGUIRenderEvent) {
    val ctrl = event.controller;
    val data = ctrl.customData;
    var energy = isNull(data.energy) ? 0 : data.energy;
    var info as string[] = [];
    info += "—————能量核心监控器—————";
    info += "能量: " + energy;
    event.extraInfo = info;
});
```

### GeckoLib 模型

```zenscript
import mods.modularmachinery.GeoMachineModel;
import mods.modularmachinery.MachineModifier;
import mods.modularmachinery.MMEvents;
import mods.modularmachinery.ControllerModelAnimationEvent;

// 注册模型
GeoMachineModel.registerGeoMachineModel("model_name",
    "modularmachinery:geo/model.geo.json",
    "modularmachinery:textures/model.png",
    "modularmachinery:animations/model.animation.json"
);

// 绑定模型到机械
MachineModifier.setMachineGeoModel("machine_name", "model_name");

// 设置动画
MMEvents.onControllerModelAnimation("machine_name", function(event as ControllerModelAnimationEvent) {
    val ctrl = event.controller;
    if (ctrl.isWorking) {
        event.addAnimation("working");
    } else {
        event.addAnimation("idle", true);
    }
});
```