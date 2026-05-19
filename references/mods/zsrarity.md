# ZSRarity CraftTweaker API 参考

> Mod ID: `zsrarity`
> 前置条件: 无
> 导入: `import zsrarity.MaterialPartRarity;`

## API 列表

### IItemStack 扩展

> 无需额外导入，直接在 IItemStack 上使用

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setRarity(string colorName)` | void | 设置物品在 GUI 中的稀有度颜色 |

**colorName 可用值**（不区分大小写）：
- `red` - 红色
- `blue` - 蓝色
- `gold` - 金色
- `dark_blue` - 深蓝色
- `dark_purple` - 深紫色
- `purple` - 紫色
- `green` - 绿色
- `dark_green` - 深绿色
- `dark_aqua` - 深青色
- `black` - 黑色
- `aqua` - 青色
- `dark_red` - 深红色
- `light_purple` - 浅紫色
- `white` - 白色
- `yellow` - 黄色
- `gray` - 灰色
- `dark_gray` - 深灰色

---

### MaterialPartRarity

> `import zsrarity.MaterialPartRarity;`

用于 ContentTweaker / B.A.S.E 材料系统的稀有度设置。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setRarity(MaterialPartDefinition part, string rarity)` | void | 设置材料部件的稀有度颜色。part 为 `<materialpart:material:part>` 引用，rarity 为颜色名称（同上） |

---

## 注意事项

- 可在游戏运行中更改稀有度，即时生效
- 不需要编辑语言文件，所有语言通用
- ContentTweaker / B.A.S.E 材料系统需要使用 `MaterialPartRarity` 类，直接对 IItemStack 使用无效
