# 语言基础 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: 无需导入

ZenScript 语言基础语法。

---

## 括号处理器列表

### 物品括号处理器（Item）

返回 `IItemStack` 对象。

```zenscript
<minecraft:apple>                    // 苹果
<minecraft:coal:0>                   // 煤炭（meta 0）
<minecraft:coal:1>                   // 木炭（meta 1）
<minecraft:coal:*>                   // 所有 meta 值
<item:minecraft:coal:*>              // 显式指定为物品（可选）
```

- `modid`：物品所属 mod 的 ID
- `itemname`：物品名称（用 `/ct hand` 获取）
- `meta`：meta 值（整数，可选，默认 0，可用 `*` 通配符）

### 方块状态括号处理器（BlockState）

返回 `IBlockState` 对象。

```zenscript
<blockstate:minecraft:dirt>                              // 泥土默认状态
<blockstate:minecraft:log>                               // 原木默认状态
<blockstate:minecraft:log:variant=oak,axis=y>            // 橡木原木，垂直
<blockstate:minecraft:log:variant=spruce,axis=x>         // 云杉原木，水平 X 轴
```

- 用逗号分隔的 `name=value` 对指定方块属性
- 未指定的属性使用默认方块状态的值

### 流体括号处理器（Liquid）

返回 `ILiquidStack` 对象。

```zenscript
<liquid:lava>       // 岩浆
<liquid:water>      // 水
<fluid:lava>        // 同上，fluid 别名
```

### 矿物辞典括号处理器（Ore）

返回 `IOreDictEntry` 对象。如果矿辞不存在，会创建一个新的空矿辞。

```zenscript
<ore:ingotIron>     // 铁锭矿辞
```

### 实体括号处理器（Entity）

返回 `IEntityDefinition` 对象。

```zenscript
<entity:minecraft:sheep>     // 羊
```

### 药水括号处理器（Potion）

返回 `IPotion` 对象。

```zenscript
<potion:minecraft:strength>      // 力量效果
```

### 药水类型括号处理器（PotionType）

返回 `IPotionType` 对象。

```zenscript
<potiontype:minecraft:strength>          // 力量药水
```

### 附魔括号处理器（Enchantment）

返回 `IEnchantmentDefinition` 对象。

```zenscript
<enchantment:minecraft:protection>       // 保护
```

### 伤害来源括号处理器（DamageSource）

返回 `IDamageSource` 对象。如果伤害来源不是预定义的，会创建一个新的。

```zenscript
<damageSource:MAGIC>             // 魔法伤害
<damageSource:GENERIC>           // 通用伤害
<damageSource:IN_FIRE>           // 火焰伤害
<damageSource:LAVA>              // 岩浆伤害
<damageSource:IN_WALL>           // 窒息伤害
<damageSource:STARVE>            // 饥饿伤害
<damageSource:OUT_OF_WORLD>      // 虚空伤害
<damageSource:FALL>              // 摔落伤害
<damageSource:CRAMMING>          // 挤压伤害
<damageSource:DROWN>             // 溺水伤害
<damageSource:LIGHTNING_BOLT>    // 闪电伤害
<damageSource:ON_FIRE>           // 着火伤害
<damageSource:HOT_FLOOR>         // 烫脚伤害
<damageSource:CACTUS>            // 仙人掌伤害
<damageSource:FLY_INTO_WALL>     // 撞墙伤害
<damageSource:WITHER>            // 凋零伤害
<damageSource:ANVIL>             // 铁砧伤害
<damageSource:FALLING_BLOCK>     // 下落方块伤害
<damageSource:DRAGON_BREATH>     // 龙息伤害
<damageSource:FIREWORKS>         // 烟花伤害
```

### 创造标签页括号处理器（CreativeTab）

返回 `ICreativeTab` 对象。

```zenscript
<creativetab:buildingBlocks>  // 建筑方块标签页
```

---

## 控制流

### if-else

```zenscript
if (condition) { ... }
else if (condition) { ... }
else { ... }
```

### 三元操作符

```zenscript
val result = condition ? valueA : valueB;
```

### for 循环

```zenscript
for i in 0 .. 10 { print(i); }         // 0 到 9
for i in 0 to 10 { print(i); }         // 同上
for item in array { print(item); }      // 遍历数组
for i, item in array { print(i); }      // 带索引遍历
for key in map { print(key); }          // 遍历映射键
for key, val in map { print(key); }     // 遍历映射键值
for entry in map.entrySet { }           // 遍历 Entry
```

### while 循环

```zenscript
var i = 0;
while (i < 10) { i = i + 1; }
```

### break / continue

```zenscript
for i in 0 .. 5 {
    if (i == 3) break;      // 跳出循环
    if (i == 2) continue;   // 跳过本次
    print(i);
}
```

---

## 函数

### 匿名函数

```zenscript
// 基本格式
function(参数列表) {
    return 返回值;
}

// 用于物品条件
<minecraft:iron_pickaxe>.only(function(item) {
    return !isNull(item) && item.damage > 100;
});

// 用于配方函数（第4个参数）
recipes.addShapeless("test", <minecraft:stone>, [<minecraft:dirt>],
    function(output, ins, info) {
        // output: 输出物品
        // ins: 输入物品映射
        // info: IRecipeFunctionInfo（含 player, world 等）
        return info.player.world.dimension == -1 ? output : null;
    },
null);

// 匿名函数内只能读取外部变量，不能重新赋值
// 但可以修改数组/映射的元素
```

### 自定义函数

#### 基本格式

```zenscript
function 函数名(参数表) as 返回类型 {
    // 代码
    return 返回值;
}
```

- 无参数：只写 `()`
- 无返回值：省略 `as 返回类型` 和 `return`
- 单行函数：直接写在 return 行

#### 示例

```zenscript
// 获取物品名
function getItemName(input as IItemStack) as string {
    val id = input.definition.id;
    val meta = input.metadata;
    if (meta == 0) {
        return id;
    } else {
        return id ~ ":" ~ meta;
    }
}

// 打包操作（无返回值）
function recipeTweak(isShaped as bool, out as IItemStack, input as IIngredient[][]) {
    recipes.remove(out, true);
    if (isShaped) {
        recipes.addShaped(getItemName(out), out, input);
    } else {
        recipes.addShapeless(getItemName(out), out, input[0]);
    }
}
```

### 全局函数变量

```zenscript
global addition as function(int, int)int = function(a as int, b as int) as int {
    return a + b;
};
```