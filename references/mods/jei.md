# JEI CraftTweaker API 参考

> Mod ID: `jei`
> 前置条件: 无
> 导入: `import mods.jei.JEI;`

## API 列表

### JEI

> `import mods.jei.JEI;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.hide(IItemStack item)` | void | 从 JEI 中隐藏指定物品 |
| `.hide(ILiquidStack liquid)` | void | 从 JEI 中隐藏指定流体 |
| `.removeAndHide(IIngredient output)` | void | 从 JEI 中隐藏物品/流体，同时移除其所有合成台配方 |
| `.removeAndHide(IIngredient output, bool NBTMatch)` | void | 同上，可指定是否匹配 NBT |
| `.hideCategory(String category)` | void | 隐藏整个 JEI 分类。可用 `/ct jeiCategories` 查看所有已注册分类 |
| `.addItem(IItemStack item)` | void | 向 JEI 添加物品（适用于未自动添加的物品或带 NBT 的物品） |
| `.addDescription(IItemStack item, string... desc)` | void | 为物品添加 JEI 描述页面 |
| `.addDescription(IItemStack[] items, string... desc)` | void | 为多个物品添加共享的 JEI 描述页面 |
| `.addDescription(IOreDictEntry dict, string... desc)` | void | 为矿辞条目添加 JEI 描述页面 |
| `.addDescription(ILiquidStack liquid, string... desc)` | void | 为流体添加 JEI 描述页面 |

---

## RandomTweaker 扩展（需安装 RandomTweaker）

> `import mods.randomtweaker.jei.IJeiPanel;`
> `import mods.randomtweaker.jei.IJeiUtils;`
> `import mods.randomtweaker.jei.IJeiRecipe;`

RandomTweaker 向 JEI 类添加了自定义界面和配方的创建功能。

### JEI 扩展方法

> `import mods.jei.JEI;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createJeiRecipe(uid as string)` | IJeiRecipe | 创建 JEI 配方 |
| `.createJei(uid as string, title as string)` | IJeiPanel | 创建 JEI 界面 |

### IJeiPanel（JEI 自定义界面）

> `import mods.randomtweaker.jei.IJeiPanel;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setModid(modid as string)` | IJeiPanel | 设置显示的模组 ID |
| `.setIcon(icon as IItemStack)` | IJeiPanel | 设置界面图标 |
| `.addSlot(slot as IJeiSlot)` | IJeiPanel | 增加槽位 |
| `.setSlots(slots as IJeiSlot[])` | IJeiPanel | 设置槽位 |
| `.onTooltip(tooltip as IJeiTooltip)` | IJeiPanel | 添加提示（不覆盖 Item 和 Fluid） |
| `.addElement(elements as IJeiElement)` | IJeiPanel | 增加元素 |
| `.setElements(elements as IJeiElement[])` | IJeiPanel | 设置元素 |
| `.addRecipeCatalyst(stack as IItemStack)` | IJeiPanel | 增加配方催化剂（按 R/U 键跳转的物品） |
| `.setRecipeCatalysts(stacks as IItemStack[])` | IJeiPanel | 设置配方催化剂 |
| `.setBackground(background as IJeiBackground)` | IJeiPanel | 设置背景 |
| `.getJeiSlots()` | IJeiSlot[] | 获取槽位 |
| `.getJeiSlot(slotName as string)` | IJeiSlot | 根据 ID 获取槽位 |
| `.getJeiElements()` | IJeiElement[] | 获取元素 |
| `.getJeiElement(elementName as string)` | IJeiElement | 根据 ID 获取元素 |
| `.register()` | void | 注册 JEI 界面 |

### IJeiUtils（JEI 工具类）

> `import mods.randomtweaker.jei.IJeiUtils;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createBackground(width as int, height as int)` | IJeiBackground | 创建背景（默认贴图） |
| `.createBackground(u, v, width, height, resourceName)` | IJeiBackground | 创建背景（自定义贴图） |
| `.createLiquidSlot(x, y, width, height, capacityMb, showCapacity, isInput, @Optional hasBase)` | IJeiSlotLiquid | 创建流体槽位。`hasBase` 默认 true |
| `.createLiquidSlot(x, y, isInput, @Optional hasBase)` | IJeiSlotLiquid | 创建流体槽位（简化版） |
| `.createLiquidSlot(slotName, x, y, width, height, capacityMb, showCapacity, isInput, @Optional hasBase)` | IJeiSlotLiquid | 创建命名流体槽位 |
| `.createLiquidSlot(slotName, x, y, isInput, @Optional hasBase)` | IJeiSlotLiquid | 创建命名流体槽位（简化版） |
| `.createItemSlot(x, y, isInput, @Optional hasBase)` | IJeiSlotItem | 创建物品槽位。`hasBase` 默认 true |
| `.createItemSlot(slotName, x, y, isInput, @Optional hasBase)` | IJeiSlotItem | 创建命名物品槽位 |
| `.createItemInputElement(x, y)` | IJeiElements | 创建物品输入元素 |
| `.createItemInputElement(elementName, x, y)` | IJeiElements | 创建命名物品输入元素 |
| `.createItemOutputElement(x, y)` | IJeiElements | 创建物品输出元素 |
| `.createItemOutputElement(elementName, x, y)` | IJeiElements | 创建命名物品输出元素 |
| `.createLiquidElement(x, y, width, height)` | IJeiElements | 创建流体元素 |
| `.createLiquidElement(elementName, x, y, width, height)` | IJeiElements | 创建命名流体元素 |
| `.createFontInfoElement(info, x, y, color, @Optional width, @Optional height)` | IJeiElements | 创建文字元素 |
| `.createFontInfoElement(elementName, info, x, y, color, @Optional width, @Optional height)` | IJeiElements | 创建命名文字元素 |
| `.createArrowElement(x, y, direction)` | IJeiElements | 创建箭头元素。`direction`：0=→、1=←、2=↑、3=↓ |
| `.createArrowElement(elementName, x, y, direction)` | IJeiElements | 创建命名箭头元素 |
| `.createImageElement(elementName, x, y, width, height, u, v, texture, textureWidth, textureHeight)` | IJeiElements | 创建图片元素。`texture` 格式 `modid:path` |
| `.createJeiManaBarElement(x, y, mana, @Optional mode)` | IJeiElements | 创建魔力条元素。`mode` 为 1 时上限为魔力池上限的十分之一 |

**注意：** 流体槽位必须根据固定宽高创建（如 16×16、43×16、16×34）。

### IJeiRecipe（JEI 自定义配方）

> `import mods.randomtweaker.jei.IJeiRecipe;`

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addInput(input as IIngredient)` | IJeiRecipe | 增加输入 |
| `.setInputs(inputs as IIngredient[])` | IJeiRecipe | 设置输入 |
| `.addOutput(output as IIngredient)` | IJeiRecipe | 增加输出 |
| `.setOutputs(outputs as IIngredient[])` | IJeiRecipe | 设置输出 |
| `.setElements(elements as IJeiElement[])` | IJeiRecipe | 设置独属于此配方的元素 |
| `.addElement(element as IJeiElement)` | IJeiRecipe | 增加独属于此配方的元素 |
| `.onJEITooltip(tooltip as IJeiTooltip)` | IJeiRecipe | 添加提示（不覆盖 Item 和 Fluid） |
| `.build()` | void | 注册 JEI 配方 |