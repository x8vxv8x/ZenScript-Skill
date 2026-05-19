# Extra Utilities 2 CraftTweaker API 参考

> Mod ID: `extrautils2`
> 前置条件: Modtweaker
> 导入: `import mods.extrautils2.*;`

## API 列表

### Crusher（粉碎机）

> `import mods.extrautils2.Crusher;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IItemStack input, @Optional IItemStack secondaryOutput, @Optional float secondaryChance)` | void | 添加粉碎配方，可选副产物及概率 |
| `.remove(IItemStack output)` | void | 按输出移除配方 |

### Resonator（共振仪）

> `import mods.extrautils2.Resonator;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(IItemStack output, IItemStack input, int energy, @Optional boolean addOwnerTag)` | void | 添加共振仪配方。`energy` 为能量消耗（1 GP = 100 energy）。`addOwnerTag` 是否添加所有者标签 |
| `.remove(IItemStack output)` | void | 按输出移除配方 |

## 使用示例

### 添加粉碎机配方

```zenscript
import mods.extrautils2.Crusher;

// 金块粉碎为 9 个金锭，10% 概率产出铁锭
Crusher.add(<minecraft:gold_ingot> * 9, <minecraft:gold_block>, <minecraft:iron_ingot>, 0.1f);

// 无副产物
Crusher.add(<minecraft:iron_ingot> * 9, <minecraft:iron_block>);
```

### 添加共振仪配方

```zenscript
import mods.extrautils2.Resonator;

// 1 GP = 100 energy，金块转化为红石块消耗 100 energy (1 GP)
Resonator.add(<minecraft:redstone_block>, <minecraft:gold_block>, 100);

// 不添加所有者标签
Resonator.add(<minecraft:gold_block>, <minecraft:iron_block>, 200, false);
```

---

## XUTweaker（实用工具）

> `import extrautilities2.Tweaker.XUTweaker;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.allowSurvivalFlight()` | void | 允许所有玩家永久飞行 |
| `.disableNetherPortals()` | void | 永久禁止下界传送门生成 |
| `.isPlayerFake(player as IPlayer)` | bool | 检查玩家是否为假玩家 |
| `.openBookScreen(player as IPlayer, pages as string[])` | bool | 为玩家打开书本界面 |

---

## InterModCommsHandler（模组间通信）

> `import extrautilities2.Tweaker.InterModCommsHandler;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.sendMessageNBT(mod as string, key as string, dataMap as DataMap)` | void | 发送NBT消息 |
| `.sendMessageString(mod as string, key as string, message as string)` | void | 发送字符串消息 |
| `.sendMessageItemStack(mod as string, key as string, stack as IItemStack)` | void | 发送物品栈消息 |
| `.sendMessageResourceLocation(mod as string, key as string, resourceLocation as string)` | void | 发送资源位置消息 |
| `.sendRuntimeMessageNBT(mod as string, key as string, dataMap as DataMap)` | void | 运行时发送NBT消息 |
| `.sendRuntimeMessageString(mod as string, key as string, message as string)` | void | 运行时发送字符串消息 |
| `.sendRuntimeMessageItemStack(mod as string, key as string, stack as IItemStack)` | void | 运行时发送物品栈消息 |
| `.sendRuntimeMessageResourceLocation(mod as string, key as string, resourceLocation as string)` | void | 运行时发送资源位置消息 |

---

## CustomMachines（自定义机器）

> `import extrautilities2.Tweaker.IMachineRegistry;`
> `import extrautilities2.Tweaker.IMachine;`
> `import extrautilities2.Tweaker.IMachineSlot;`

### IMachineRegistry（机器注册表）

#### 创建机器

```zenscript
IMachineRegistry.createNewMachine(
    name as string,
    energyBufferSize as int,
    energyTransferLimit as int,
    inputSlots as IMachineSlot[],
    outputSlots as IMachineSlot[],
    frontTexture as string,
    frontTextureActive as string,
    @Optional color as int
);

IMachineRegistry.createNewGenerator(
    name as string,
    energyBufferSize as int,
    energyTransferLimit as int,
    inputSlots as IMachineSlot[],
    outputSlots as IMachineSlot[],
    frontTexture as string,
    frontTextureActive as string,
    @Optional color as int
);
```

#### 获取机器

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getMachine(name as string)` | IMachine | 按名称获取机器 |
| `.getRegisterdMachineNames()` | IMachine[] | 获取所有已注册机器 |

#### 内置机器

| 属性 | 说明 |
|------|------|
| `crusher` | 粉碎机 |
| `enchanter` | 附魔器 |
| `generator_culinary` | 烹饪发电机 |
| `generator_death` | 死亡发电机 |
| `generator_dragon` | 龙发电机 |
| `generator_enchant` | 附魔发电机 |
| `generator_ender` | 末影发电机 |
| `generator_furnace` | 熔炉发电机 |
| `generator_ice` | 冰发电机 |
| `generator_lava` | 岩浆发电机 |
| `generator_netherstar` | 下界之星发电机 |
| `generator_overclock` | 超频发电机 |
| `generator_pink` | 粉色发电机 |
| `generator_potion` | 药水发电机 |
| `generator_redstone` | 红石发电机 |
| `generator_slime` | 史莱姆发电机 |
| `generator_survivalist` | 生存主义者发电机 |
| `generator_tnt` | TNT发电机 |

### IMachine（机器）

#### 添加配方

```zenscript
// 使用概率映射
myMachine.addRecipe(
    inputs as IIngredient[string],
    outputs as IIngredient[string],
    energy as int,
    time as int,
    probabilities as float[string]
);

// 使用输出映射
myMachine.addRecipe(
    inputs as IIngredient[string],
    outputs as Object[string],
    energy as int,
    time as int
);
```

#### 移除配方

```zenscript
// 使用IIngredient
myMachine.removeRecipe(inputs as IIngredient[string]);

// 使用分离映射
myMachine.removeRecipe(
    items as IItemStack[string],
    liquids as ILiquidStack[string]
);
```

#### 获取信息

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getInputSlots()` | IMachineSlot[] | 获取输入槽 |
| `.getOutputSlots()` | IMachineSlot[] | 获取输出槽 |
| `.getSlot(name as string)` | IMachineSlot | 按名称获取槽 |

### IMachineSlot（机器槽）

#### 创建槽

```zenscript
IMachineSlot.newItemStackSlot(name as string);
IMachineSlot.newItemStackSlot(name as string, isOptional as bool);
IMachineSlot.newItemStackSlot(name as string, stackCapacity as int);
IMachineSlot.newItemStackSlot(name as string, isOptional as bool, stackCapacity as int);
IMachineSlot.newItemStackSlot(name as string, color as int, isOptional as bool, backgroundTexture as string, stackCapacity as int);

IMachineSlot.newFluidSlot(name as string);
IMachineSlot.newFluidSlot(name as string, stackCapacity as int);
IMachineSlot.newFluidSlot(name as string, stackCapacity as int, filterLiquidStack as ILiquidStack);
IMachineSlot.newFluidSlot(name as string, stackCapacity as int, isOptional as bool, filterLiquidStack as ILiquidStack);
IMachineSlot.newFluidSlot(name as string, stackCapacity as int, color as int, isOptional as bool, filterLiquidStack as ILiquidStack);
```

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 槽名称 |
| `optional` | bool | 是否可选 |
| `stackCapacity` | int | 容量 |

---

## 使用XUTweaker

```zenscript
import extrautilities2.Tweaker.XUTweaker;

XUTweaker.allowSurvivalFlight();
XUTweaker.disableNetherPortals();
```

## 使用自定义机器

```zenscript
import extrautilities2.Tweaker.IMachineRegistry;
import extrautilities2.Tweaker.IMachineSlot;

// 创建输入输出槽
val inputSlot = IMachineSlot.newItemStackSlot("input");
val outputSlot = IMachineSlot.newItemStackSlot("output");

// 创建机器
val machine = IMachineRegistry.createNewMachine(
    "my_machine",
    10000,  // 能量缓冲区大小
    100,    // 能量传输限制
    [inputSlot],
    [outputSlot],
    "minecraft:textures/blocks/stone.png",
    "minecraft:textures/blocks/stone.png"
);

// 添加配方
machine.addRecipe(
    {"input": <minecraft:iron_ore>},
    {"output": <minecraft:iron_ingot>},
    1000,   // 能量消耗
    200     // 处理时间
);
```
