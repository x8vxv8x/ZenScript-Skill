# Creative Tabs API

## ICreativeTab

> `import crafttweaker.creativetabs.ICreativeTab;`

### 属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `id` | int | 标签页 ID |
| `name` | string | 标签页名称 |
| `displayName` | string | 显示名称 |
| `commandString` | string | 命令字符串 |
| `iconItem` | IItemStack | 图标物品 |
| `tabIndex` | int | 标签页索引 |
| `isSearchTab` | bool | 是否搜索标签页 |
| `hasSearchBar` | bool | 是否有搜索栏 |

### 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.setTabIconItem(IItemStack)` | IItemStack | void | 设置标签页图标物品 |
| `.setTabLabel(string)` | string | void | 设置标签页标签 |
| `.setTabTitle(string)` | string | void | 设置标签页标题 |
| `.setBackgroundImage(string)` | string | void | 设置背景图片 |
| `.setHasSearchBar(bool)` | bool | void | 设置是否有搜索栏 |
| `.setSearchBarWidth(int)` | int | void | 设置搜索栏宽度 |
| `.setTabsVisibleSingleColumn(bool)` | bool | void | 设置单列是否可见 |
| `.setTabsVisibleDoubleColumn(bool)` | bool | void | 设置双列是否可见 |
| `.setNoScrollBar(bool)` | bool | void | 设置无滚动条 |
| `.setNoTitle()` | 无 | void | 设置无标题 |

---

## 获取创造模式标签页

```zenscript
// 获取所有创造模式标签页
for tab in game.creativeTabs {
    print(tab.name ~ ": " ~ tab.displayName);
}

// 按名称获取
val buildingBlocks = game.getCreativeTab("buildingBlocks");
```

---

## 物品设置创造模式标签页

```zenscript
// 设置物品的创造模式标签页
<minecraft:stone>.definition.setCreativeTab("buildingBlocks");

// 获取物品的创造模式标签页
val tab = <minecraft:stone>.definition.creativeTab;
```

---

## ContentTweaker 扩展（需安装 ContentTweaker）

> `import mods.contenttweaker.VanillaFactory;`
> `import mods.contenttweaker.CreativeTab;`

CoT 脚本第一行必须为 `#loader contenttweaker`。

### VanillaFactory 创造标签方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.createCreativeTab(string id, IItemStack/Item/Block icon)` | 标签 ID, 图标 | CreativeTab | 创建自定义创造标签 |

### CreativeTab（自定义创造标签）

> `import mods.contenttweaker.CreativeTab;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.register()` | 无 | void | 注册创造标签 |
