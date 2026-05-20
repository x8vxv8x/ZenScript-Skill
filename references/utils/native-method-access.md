# 原生方法访问 CraftTweaker API 参考

> Mod ID: 无
> 前置条件: ZenUtils（版本要求: 1.19.0+）
> 导入: `import native.<完整类名>;`

ZenUtils 允许在 ZenScript 中直接访问 Java 原生类和方法。

---

## 用法

### 导入原生类

使用 `native.` 前缀导入 Java 类：

```zenscript
import native.net.minecraft.world.World;
import native.net.minecraft.entity.player.EntityPlayer;
```

所有公共方法和字段均可访问。

### CraftTweaker 与 Minecraft 类互转

| 方向 | 方法 | 说明 |
|------|------|------|
| CraftTweaker → MC | `.native` getter | 如 `entity.native` 返回 `Entity` |
| MC → CraftTweaker | `.wrapper` getter | 如 `mcEntity.wrapper` 返回 `IEntity` |

也可用 `as` 强转，传参时自动转换。

```zenscript
// CraftTweaker → MC
val mcWorld as native.net.minecraft.world.World = iWorld.native;

// MC → CraftTweaker
val iWorld2 as IWorld = mcWorld.wrapper;
```

### MCP 名称映射

ZenUtils 内置 MCP `stable-39` 映射，可使用人类可读的方法名：

```zenscript
import native.net.minecraft.world.World;

// 使用 MCP 名称（如 getLoadedChunks()）
val chunkProvider = world.native.chunkProvider;
```

### Getter/Setter 映射

Java 的 `getFoo()`/`setFoo(val)` 自动映射为 ZenScript 的 `foo` getter/setter。

### Iterable 接口

`Iterable<T>` 及其子类支持 for 循环、`.length` 和 `as [T]` 转换：

```zenscript
val set = ...; // Set<String>
val list = set as [string];  // 转为列表
print(set.length);           // 获取长度
for s in set {               // 遍历
    print(s);
}
```

### 相等判断

`==` 和 `!=` 运算符可用于所有原生类，调用 `Objects.equals`。

### 向下转型

```zenscript
// CraftTweaker 类：左 unchecked cast 允许
val entity as IEntity = event.entity;
if (entity instanceof IPlayer) {
    val player as IPlayer = entity;  // 合法
}

// 原生类：需要右 checked cast
val mcEntity as Entity = entity.native;
if (mcEntity instanceof EntityPlayer) {
    val mcPlayer = mcEntity as EntityPlayer;  // 合法
}
```

---

## 使用示例

### 获取已加载区块数

```zenscript
import crafttweaker.event.PlayerLoggedInEvent;
import native.net.minecraft.world.gen.ChunkProviderServer;
import native.net.minecraft.world.World;

$expand World$loadedChunkCount() as int {
    val chunkProvider = this.chunkProvider;
    if (chunkProvider instanceof ChunkProviderServer) {
        return (chunkProvider as ChunkProviderServer).loadedChunks.length;
    }
    return 0;
}

events.onPlayerLoggedIn(function(event as PlayerLoggedInEvent) {
    if (event.player.world.remote) return;
    event.player.world.catenation()
        .sleep(10)
        .run(function(world, context) {
            print(world.native.loadedChunkCount() ~ " 个区块已加载");
        })
        .start();
});
```

### zenClass 继承原生类

@since 1.21.0

自定义 zenClass 可继承原生类或接口：

```zenscript
#loader preinit
import native.net.minecraft.init.Blocks;
import native.net.minecraft.block.Block;
import native.net.minecraft.block.BlockCrops;
import native.net.minecraft.util.ResourceLocation;
import native.net.minecraft.world.World;
import native.net.minecraft.item.Item;
import native.net.minecraft.util.math.BlockPos;
import native.net.minecraft.block.state.IBlockState;
import native.net.minecraft.item.ItemSeeds;
import native.java.util.Random;

zenClass CrystalAlga extends BlockCrops {
    zenConstructor() { super(); }

    // canUseBonemeal - 必须使用 SRG 名称
    function func_180670_a(world as World, rand as Random, pos as BlockPos, state as IBlockState) as bool {
        return false;
    }

    // getSeed
    function func_149866_i() as Item {
        return itemUtils.getItem("contenttweaker:crystal_alga_seeds").definition.native;
    }

    // getCrop
    function func_149865_P() as Item {
        return itemUtils.getItem("contenttweaker:crystal_alga").definition.native;
    }
}
```

规则：
- `extends` 后第一个可以是类或接口，后续必须是接口
- 构造函数中必须调用 `super()`
- 方法重写必须使用 SRG 名称（`func_XXXXXX_x`），MCP 名称不可用于重写
- 函数体内可使用 MCP 名称调用 MC 代码

---

## 敏感操作黑名单

以下原生代码**不可访问**：

- 文件 IO
- 网络
- 窗口
- 多线程
- Mixin/ASM
- 其他语言库（Scala、Kotlin、Groovy）
- Java 底层代码（`java.lang`、`jdk.`、`sun.` 等）

### java.lang.Class 访问

@since 1.22.4

`java.lang.Class` 可导入但**禁止反射操作**：

```zenscript
import native.java.lang.Class;
import native.java.util.ArrayList;
import native.net.minecraft.item.ItemStack;

val listClass = ArrayList.class;  // 合法
print(toString(listClass));       // "class java.util.ArrayList"

val item as ItemStack = <minecraft:apple>.native;
val itemClass = item.class;       // 获取运行时类

// 以下操作被禁止:
// itemClass.getName()        // 错误
// itemClass.getMethods()     // 错误
// Class.forName("...")       // 错误
```
