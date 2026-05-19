# Requious Frakto CraftTweaker API 参考

> Mod ID: `requious`
> 前置条件: 无
> 导入: `import mods.requious.AssemblyRecipe;`

高级自定义单方块机器模组，支持自定义 GUI、槽位、配方、激光系统和 JEI 集成。

**单位约定**: 能量 = FE，流体 = mb，时间 = Tick

机器 GUI 为 9×5 格，通过 `<assembly:机器名>` 获取机器实例。

---

## API 列表

### ComponentFace（组件面）

> `import mods.requious.ComponentFace;`

用于定义槽位接受输入/输出的机器面。

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.all()` | ComponentFace | 所有面 |
| `.front()` | ComponentFace | 前面 |
| `.back()` | ComponentFace | 后面 |
| `.side()` | ComponentFace | 侧面（非前后面） |
| `.frontBack()` | ComponentFace | 前后面 |
| `.frontSide()` | ComponentFace | 前面和侧面 |
| `.backSide()` | ComponentFace | 后面和侧面 |
| `.none()` | ComponentFace | 无面 |
| `.up()` | ComponentFace | 上面 |
| `.down()` | ComponentFace | 下面 |
| `.north()` | ComponentFace | 北 |
| `.south()` | ComponentFace | 南 |
| `.east()` | ComponentFace | 东 |
| `.west()` | ComponentFace | 西 |
| `.horizontal()` | ComponentFace | 水平四面 |
| `.vertical()` | ComponentFace | 垂直两面（上下） |

---

### ItemSlot（物品槽）

> 由 `Assembly.setItemSlot()` 创建

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setGroup(String group)` | ItemSlot | 将槽加入指定组，可多次调用加入多个组 |
| `.setHidden()` | ItemSlot | 隐藏槽位，阻止玩家交互 |
| `.setAccess(boolean input, boolean output)` | ItemSlot | 设置外部物品输入/输出权限。不影响玩家手动放置和配方 |
| `.setHandAccess(boolean input, boolean output)` | ItemSlot | 设置玩家在 GUI 中的放入/取出权限 |
| `.allowOverfill()` | ItemSlot | 空槽首次输入忽略容量限制。适合输出物品的配方 |
| `.noDrop()` | ItemSlot | 机器被破坏时不掉落物品 |
| `.pushItem(int size)` | ItemSlot | 每 tick 自动向相邻容器推送指定数量物品 |
| `.pushItem(int size, int slot)` | ItemSlot | 每 tick 自动向相邻容器指定槽位推送物品。slot 为 -1 表示任意槽 |

---

### FluidSlot（流体槽）

> 由 `Assembly.setFluidSlot()` 创建

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setGroup(String group)` | FluidSlot | 将槽加入指定组 |
| `.setHidden()` | FluidSlot | 隐藏槽位 |
| `.setAccess(boolean input, boolean output)` | FluidSlot | 设置外部流体输入/输出权限 |
| `.allowBucket(boolean input, boolean output, boolean drops)` | FluidSlot | 设置玩家在 GUI 中的流体容器操作权限。drops 控制机器破坏时是否掉落容器 |
| `.allowOverfill()` | FluidSlot | 空槽首次输入忽略容量限制 |
| `.pushFluid(int size)` | FluidSlot | 每 tick 自动向相邻流体容器推送指定 mb 流体 |

---

### EnergySlot（能量槽）

> 由 `Assembly.setEnergySlot()` 创建

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setGroup(String group)` | EnergySlot | 将槽加入指定组 |
| `.setHidden()` | EnergySlot | 隐藏槽位 |
| `.setAccess(boolean input, boolean output)` | EnergySlot | 设置外部能量输入/输出权限 |
| `.allowBattery(boolean input, boolean output, boolean drops)` | EnergySlot | 设置玩家在 GUI 中的电池操作权限 |
| `.setUnit(String unit)` | EnergySlot | 设置 tooltip 显示单位。Langkey: `requious.unit.[unit]`，默认 `"fe"` |
| `.setPowerLoss(float loss)` | EnergySlot | 设置每秒能量流失量。低于 1 FE 时变为每多少 Tick 流失 1 FE（如 0.4 ≈ 每 4 tick 流失 1 FE） |
| `.allowOverfill()` | EnergySlot | 空槽首次输入忽略容量限制 |
| `.setTexture(int x, int y, GaugeDirection direction)` | EnergySlot | 设置能量条纹理和方向。纹理坐标自动乘以 18 |
| `.setTexture(String texture, int x, int y, GaugeDirection direction)` | EnergySlot | 自定义纹理位置。默认: `"requious:textures/gui/assembly_gauges.png"` |
| `.pushEnergy(int size)` | EnergySlot | 每 tick 自动向相邻能量方块推送指定 FE |

---

### LaserSlot（激光槽）

> 由 `Assembly.setLaserSlot()` 创建

激光是 Requious Frakto 的特殊能量传输方式：无线传输、可定义能量类型和目标区域、多束激光可合并、方向相关。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setGroup(String group)` | LaserSlot | 将槽加入指定组 |
| `.setHidden()` | LaserSlot | 隐藏槽位 |
| `.setAccess(boolean input, boolean output)` | LaserSlot | 设置激光输入/输出权限 |
| `.setType(String type)` | LaserSlot | 限制接受的激光类型 |
| `.setLimit(int min, int max)` | LaserSlot | 设置激光功率限制。低于 min 的不接受，高于 max 的截断为 max |
| `.setArea(int x1, int y1, int z1, int x2, int y2, int z2)` | LaserSlot | 设置激光目标区域（相对于机器朝向，正 y 指向机器前方） |

---

### SelectionSlot（选择槽）

> 由 `Assembly.setSelectionSlot()` 创建

选择槽创建可选图标列表，列表内容由配方需求填充。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setGroup(String group)` | SelectionSlot | 将槽加入指定组 |
| `.setHidden()` | SelectionSlot | 隐藏槽位 |
| `.setMaxSelection(int max)` | SelectionSlot | 设置该选择组中可同时选中的最大图标数。只需在组内任一槽调用即可 |

---

### DurationSlot（时长槽）

> 由 `Assembly.setDurationSlot()` 创建

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setGroup(String group)` | DurationSlot | 将槽加入指定组 |
| `.setVisual(SlotVisual slotVisual)` | DurationSlot | 设置槽的视觉效果 |

---

### SlotVisual（槽位视觉）

> `import mods.requious.SlotVisual;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.itemSlot()` | SlotVisual | 物品槽样式 |
| `.fluidSlot()` | SlotVisual | 流体容器样式（红色仪表） |
| `.energySlot()` | SlotVisual | 能量表样式（红色垂直填充） |
| `.infoSlot()` | SlotVisual | 信息样式（蓝色圆圈白色 i，JEI 风格） |
| `.selectionSlot()` | SlotVisual | 选择样式（选中时红色勾） |
| `.arrowRight()` | SlotVisual | 右箭头（向右填充） |
| `.arrowDown()` | SlotVisual | 下箭头 |
| `.arrowLeft()` | SlotVisual | 左箭头 |
| `.arrowUp()` | SlotVisual | 上箭头 |
| `.createSimple(String texture, int x, int y)` | SlotVisual | 创建简单视觉。纹理坐标自动乘以 18 |
| `.createGauge(String texture, int x1, int y1, int x2, int y2, GaugeDirectionCT direction, boolean inverse, @Optional int width, @Optional int height, @Optional int[] rgb)` | SlotVisual | 创建仪表视觉。x1/y1 为背景部分，x2/y2 为填充部分；inverse 为 true 时反转显示；rgb 为 RGBA 或 RGB 颜色着色 |
| `.create(int width, int height)` | SlotVisual | 创建自定义复合视觉 |

#### 实例方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addPart(String texture, int x, int y, @Optional int[] rgb)` | SlotVisual | 添加静态部件 |
| `.addDirectional(String texture, int x, int y, GaugeDirectionCT direction, boolean inverse, @Optional int[] rgb)` | SlotVisual | 添加方向填充部件。可组合多个不同方向的填充部件 |

---

### AssemblyRecipe（配方）

> `import mods.requious.AssemblyRecipe;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.create(function(container))` | AssemblyRecipe | 创建配方。container 为 RecipeContainer 实例 |

#### 需求方法（按添加顺序解析）

| 方法 | 返回 | 说明 |
|------|------|------|
| `.requireItem(String group, IIngredient ingredient)` | AssemblyRecipe | 物品需求 |
| `.requireItem(String group, IIngredient ingredient, int min, int max)` | AssemblyRecipe | 物品需求（指定最小/最大提取量） |
| `.requireFluid(String group, ILiquidStack ingredient)` | AssemblyRecipe | 流体需求 |
| `.requireFluid(String group, ILiquidStack ingredient, int min, int max)` | AssemblyRecipe | 流体需求（指定最小/最大 mb） |
| `.requireEnergy(String group, int energy, @Optional String mark)` | AssemblyRecipe | 能量需求。mark 可使提取量在 container 中可用 |
| `.requireEnergy(String group, int min, int max, @Optional String mark)` | AssemblyRecipe | 能量需求（范围） |
| `.requireLaser(String group, int energy, @Optional String mark, @Optional SlotVisual slotVisual)` | AssemblyRecipe | 激光需求 |
| `.requireLaser(String group, String type, int energy, @Optional String mark, @Optional SlotVisual slotVisual)` | AssemblyRecipe | 激光需求（指定类型） |
| `.requireWorldCondition(String group, function(machine), int interval)` | AssemblyRecipe | 世界条件。function 返回 true 表示可工作。interval 为检测间隔 tick |
| `.requireSelection(String group, IItemStack stack, boolean reset)` | AssemblyRecipe | 选择需求。stack 为选择组中显示的图标；reset 为配方完成后是否重置选择 |
| `.requireDuration(String group, int duration)` | AssemblyRecipe | 时长需求。duration 为 tick 数。配方可有多个时长，每次执行填充一个 |
| `.setSubProcess(String processGroup)` | AssemblyRecipe | 设置子进程组。同一进程组每 tick 只执行一个配方 |

---

### RecipeContainer（配方容器）

> `import mods.requious.RecipeContainer;`
> 在配方函数中用于交换数据。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `.jei` | boolean | 当前是否在 JEI 中执行 |

#### 标记读取方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getItem(String mark)` | IItemStack | 获取标记的物品。如接受任意铁矿标记为 `"ironOre"`，返回实际匹配的物品 |
| `.getFluid(String mark)` | ILiquidStack | 获取标记的流体 |
| `.getEnergy(String mark)` | int | 获取标记的能量 |

#### 输出方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addItemOutput(String group, IItemStack item)` | void | 输出物品到指定组 |
| `.addItemOutput(String group, IItemStack item, int minInsert)` | void | 输出物品。minInsert 为处理所需的实际最小数量 |
| `.addFluidOutput(String group, ILiquidStack fluid)` | void | 输出流体到指定组 |
| `.addFluidOutput(String group, ILiquidStack fluid, int minInsert)` | void | 输出流体。minInsert 为处理所需的实际最小 mb |
| `.addEnergyOutput(String group, int energy)` | void | 输出能量到指定组 |
| `.addEnergyOutput(String group, int energy, int minInsert)` | void | 输出能量。minInsert 为处理所需的实际最小 FE |
| `.addLaserOutput(String group, String type, int energy, LaserVisual visual, @Optional SlotVisual slotVisual)` | void | 输出激光 |
| `.addWorldOutput(function(machine))` | void | 世界输出。含世界输出的配方不能直接添加到 JEI |

---

### MachineContainer（机器容器）

> `import mods.requious.MachineContainer;`
> 在世界输出/条件函数中使用，提供机器实例信息。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `.world` | IWorld | 机器所在世界 |
| `.pos` | IBlockPos | 机器坐标 |
| `.block` | IBlock | 机器方块 |
| `.state` | IBlockState | 机器方块状态 |
| `.facing` | IFacing | 机器朝向 |
| `.random` | Random | 随机数对象 |

#### 数据读写方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getInteger(String name)` | int | 获取整数数据 |
| `.getDouble(String name)` | double | 获取浮点数据 |
| `.getString(String name)` | string | 获取字符串数据 |
| `.getItem(String name)` | IItemStack | 获取物品数据 |
| `.getFluid(String name)` | ILiquidStack | 获取流体数据 |
| `.getVector(String name)` | IVector3d | 获取向量数据 |
| `.setInteger(String name, int value)` | void | 设置整数数据 |
| `.setDouble(String name, double value)` | void | 设置浮点数据 |
| `.setString(String name, string value)` | void | 设置字符串数据 |
| `.setFacing(String name, IFacing value)` | void | 设置朝向数据 |
| `.setColor(String name, ColorCT value)` | void | 设置颜色数据 |
| `.setItem(String name, IItemStack value)` | void | 设置物品数据 |
| `.setFluid(String name, ILiquidStack value)` | void | 设置流体数据 |
| `.setVector(String name, double x, double y, double z)` | void | 设置向量数据 |

#### 槽位操作方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getItem(int x, int y)` | IItemStack | 获取指定坐标的物品 |
| `.getFluid(int x, int y)` | ILiquidStack | 获取指定坐标的流体 |
| `.getEnergy(int x, int y)` | int | 获取指定坐标的能量 |
| `.setItem(int x, int y, IItemStack stack)` | void | 设置指定坐标的物品 |
| `.setFluid(int x, int y, ILiquidStack stack)` | void | 设置指定坐标的流体 |
| `.setEnergy(int x, int y, int amount)` | void | 设置指定坐标的能量 |

#### 组操作方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.insertItem(String group, IItemStack stack)` | IItemStack | 向指定组插入物品，返回剩余物品 |
| `.extractItem(String group, IIngredient filter)` | IItemStack | 从指定组提取物品 |
| `.insertFluid(String group, ILiquidStack stack)` | ILiquidStack | 向指定组插入流体，返回剩余流体 |
| `.extractFluid(String group, IIngredient filter)` | ILiquidStack | 从指定组提取流体 |
| `.insertEnergy(String group, int energy)` | int | 向指定组插入能量，返回剩余能量 |
| `.extractEnergy(String group, int energy)` | int | 从指定组提取能量 |

---

### Random（随机数工具）

> `import mods.requious.Random;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.seedInt(int seed, int max)` | int | 通过种子生成不超过 max 的整数 |
| `.seedDouble(int seed)` | double | 通过种子生成 0~1 的浮点数 |
| `.nextInt(int max)` | int | 生成不超过 max 的随机整数 |
| `.nextDouble()` | double | 生成 0~1 的随机浮点数 |

---

## Assembly 机器方法

> 由 `<assembly:机器名>` 获取

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setItemSlot(int x, int y, ComponentFace face, int capacity)` | ItemSlot | 添加物品槽。capacity 最大 64 |
| `.setFluidSlot(int x, int y, ComponentFace face, int capacity)` | FluidSlot | 添加流体槽。capacity 单位 mb |
| `.setEnergySlot(int x, int y, ComponentFace face, int capacity)` | EnergySlot | 添加能量槽。capacity 单位 FE |
| `.setLaserSlot(int x, int y, ComponentFace face)` | LaserSlot | 添加激光槽 |
| `.setSelectionSlot(int x, int y, String selectionGroup, int index)` | SelectionSlot | 添加选择槽 |
| `.setDurationSlot(int x, int y)` | DurationSlot | 添加时长槽 |
| `.addRecipe(AssemblyRecipe recipe)` | void | 向机器添加配方。同一配方可添加到多个机器 |
| `.addJEIRecipe(AssemblyRecipe recipe)` | void | 向机器 JEI 处理器添加配方。只能添加到一个机器的 JEI |
| `.addJEIRecipe(IItemStack catalyst)` | void | 注册 JEI 配方催化剂（机器图标） |
| `.setJEIItemSlot(int x, int y, String group, @Optional SlotVisual visual)` | void | 设置 JEI 物品槽 |
| `.setJEIFluidSlot(int x, int y, String group)` | void | 设置 JEI 流体槽 |
| `.setJEIEnergySlot(int x, int y, String group, @Optional String unit)` | void | 设置 JEI 能量槽 |
| `.setJEILaserSlot(int x, int y, String group)` | void | 设置 JEI 激光槽 |
| `.setJEISelectionSlot(int x, int y, String group, @Optional SlotVisual visual)` | void | 设置 JEI 选择槽 |
| `.setJEIDurationSlot(int x, int y, String group, SlotVisual visual)` | void | 设置 JEI 时长槽 |
| `.setJEIDecoration(int x, int y, String group, SlotVisual visual)` | void | 设置 JEI 装饰 |

---

## 使用示例

### 创建简单机器（泥土→沙砾）

```zenscript
import mods.requious.AssemblyRecipe;
import mods.requious.ComponentFace;

var machine = <assembly:my_machine>;

// 添加输入槽和输出槽
machine.setItemSlot(1, 1, ComponentFace.all(), 64)
       .setAccess(true, false)
       .setGroup("input");
machine.setItemSlot(3, 1, ComponentFace.all(), 64)
       .setAccess(false, true)
       .setGroup("output");

// 添加配方
var dirtToGravel = AssemblyRecipe.create(function(container) {
    container.addItemOutput("output", <minecraft:gravel>);
}).requireItem("input", <minecraft:dirt>);

machine.addRecipe(dirtToGravel);
```

### 使用标记传递物品

```zenscript
import mods.requious.AssemblyRecipe;
import mods.requious.ComponentFace;

var machine = <assembly:my_machine>;

machine.setItemSlot(1, 1, ComponentFace.all(), 64)
       .setAccess(true, false)
       .setGroup("input");
machine.setItemSlot(3, 1, ComponentFace.all(), 64)
       .setAccess(false, true)
       .setGroup("output");

// 将输入物品传递到输出
var tenOfAny = <*>.marked("inputItem") * 10;

var transferItem = AssemblyRecipe.create(function(container) {
    container.addItemOutput("output", container.getItem("inputItem"));
}).requireItem("input", tenOfAny);

machine.addRecipe(transferItem);
```

### 带能量和时长的配方

```zenscript
import mods.requious.AssemblyRecipe;
import mods.requious.ComponentFace;
import mods.requious.SlotVisual;

var machine = <assembly:my_machine>;
var arrowRight = SlotVisual.arrowRight();

machine.setItemSlot(1, 1, ComponentFace.all(), 64)
       .setAccess(true, false)
       .setGroup("input");
machine.setItemSlot(3, 1, ComponentFace.all(), 64)
       .setAccess(false, true)
       .setGroup("output");
machine.setEnergySlot(0, 0, ComponentFace.all(), 10000)
       .setAccess(true, false)
       .setGroup("energy");
machine.setDurationSlot(2, 1)
       .setVisual(arrowRight);

var recipe = AssemblyRecipe.create(function(container) {
    container.addItemOutput("output", <minecraft:diamond>);
}).requireItem("input", <minecraft:coal_block>)
  .requireEnergy("energy", 1000)
  .requireDuration("duration", 100);

machine.addRecipe(recipe);

// JEI 显示
machine.setJEIItemSlot(0, 0, "input");
machine.setJEIItemSlot(4, 0, "output");
machine.setJEIEnergySlot(0, 2, "energy");
machine.setJEIDurationSlot(2, 0, "duration", arrowRight);
machine.addJEIRecipe(recipe);
```

### 世界条件（下方需要石头才能工作）

```zenscript
import mods.requious.AssemblyRecipe;
import mods.requious.ComponentFace;
import crafttweaker.world.IFacing;
import crafttweaker.world.IWorld;
import crafttweaker.world.IBlockPos;

var machine = <assembly:my_machine>;

machine.setItemSlot(2, 1, ComponentFace.all(), 64)
       .setAccess(true, true)
       .setGroup("io");

var recipe = AssemblyRecipe.create(function(container) {
    container.addItemOutput("io", <minecraft:iron_ingot>);
}).requireItem("io", <minecraft:iron_ore>)
  .requireWorldCondition("world_check", function(machineContainer) {
    var world as IWorld = machineContainer.world;
    var pos as IBlockPos = machineContainer.pos;
    if (!world.remote && world.getBlockState(pos.getOffset(IFacing.down(), 1)) == <blockstate:minecraft:stone>) {
        return true;
    }
    return false;
  }, 20);

machine.addRecipe(recipe);
```

### 世界输出（在机器上方放置方块）

```zenscript
import mods.requious.AssemblyRecipe;
import crafttweaker.world.IFacing;

var machine = <assembly:my_machine>;

var recipe = AssemblyRecipe.create(function(container) {
    if (!container.jei) {
        container.addWorldOutput(function(machineContainer) {
            var world = machineContainer.world;
            if (!world.remote) {
                world.setBlockState(<blockstate:minecraft:iron_block>, machineContainer.pos.getOffset(IFacing.up(), 1));
                return true;
            }
            return false;
        });
    }
});

machine.addRecipe(recipe);
```

### 激光配方

```zenscript
import mods.requious.AssemblyRecipe;
import mods.requious.ComponentFace;
import mods.requious.SlotVisual;

var machine = <assembly:my_machine>;

machine.setLaserSlot(0, 0, ComponentFace.all())
       .setAccess(true, false)
       .setGroup("laser");
machine.setItemSlot(4, 0, ComponentFace.all(), 64)
       .setAccess(false, true)
       .setGroup("output");

var recipe = AssemblyRecipe.create(function(container) {
    container.addItemOutput("output", <minecraft:diamond>);
}).requireLaser("laser", 1000);

machine.addRecipe(recipe);

// JEI 显示
machine.setJEILaserSlot(0, 0, "laser");
machine.setJEIItemSlot(4, 0, "output");
machine.addJEIRecipe(recipe);
```

---

## 机器 JSON 定义

机器需在 `/config/requious/assembly.json` 中定义：

```json
{
  "resourceName": "my_machine",
  "model": "requious:assembly_block",
  "placeType": "Horizontal",
  "hasGUI": true,
  "colorA": { "r": 255, "g": 255, "b": 255, "a": 255 },
  "colorB": { "r": 255, "g": 255, "b": 255, "a": 255 }
}
```

**placeType 可选值**: `Any`、`Up`、`Down`、`Horizontal`、`Vertical`、`HorizontalUp`、`HorizontalDown`

---

## 注意事项

- `group` 用于机器内部配方交互，`face` 用于机器外部交互
- 需求按添加顺序解析，选择槽放在其他需求之前则始终显示图标，放在之后则需满足前置需求才显示
- 时长需求应最后添加
- 单个需求只能从一个槽获取。10+10 分布在两个槽的物品不能满足 20 的需求
- 同一配方可添加到多个机器，但 JEI 配方只能添加到一个机器
- 含 `addWorldOutput` 的配方不能直接添加到 JEI
- JEI 中执行配方函数时不会返回标记值，可用 `container.jei` 判断并做替代处理
- JEI 槽位只能属于一个组
- 每个进程组每 tick 只执行一个配方
