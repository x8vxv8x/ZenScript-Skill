# 自定义方块 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: ContentTweaker（部分需要 ZenUtils 或 RandomTweaker）
> 导入: `import mods.contenttweaker.VanillaFactory;`、`import mods.contenttweaker.Block;`

ContentTweaker 和 ZenUtils 自定义方块 API。

---

## ContentTweaker 扩展（需安装 ContentTweaker）

> `import mods.contenttweaker.VanillaFactory;`
> `import mods.contenttweaker.Block;`

CoT 脚本第一行必须为 `#loader contenttweaker`。

### VanillaFactory 方块方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.createBlock(string id, BlockMaterial)` | Block | 创建自定义方块 |

### Block（自定义方块）

> `import mods.contenttweaker.Block;`

| ZenProperty | 类型 | 默认值 | 说明 |
|-------------|------|--------|------|
| `blockHardness` | float | 5.0 | 方块硬度 |
| `blockResistance` | float | 5.0 | 防爆等级 |
| `blockSoundType` | SoundType | `<soundtype:metal>` | 方块声音 |
| `creativeTab` | ICreativeTab | 杂项 | 所在创造标签 |
| `lightValue` | int | 0 | 光照等级（最大 15） |
| `lightOpacity` | int | 255/0 | 不透明度 |
| `fullBlock` | bool | true | 是否完整方块 |
| `translucent` | bool | false | 是否半透明 |
| `blockLayer` | string | "SOLID" | 渲染层: "SOLID"/"CUTOUT_MIPPED"/"CUTOUT"/"TRANSLUCENT" |
| `gravity` | bool | false | 是否受重力影响 |
| `slipperiness` | float | 0.6 | 滑度（冰为 0.98） |
| `toolClass` | string | "pickaxe" | 需要的挖掘工具 |
| `toolLevel` | int | 2 | 需要的挖掘等级 |
| `entitySpawnable` | bool | true | 生物是否可在此方块上生成 |
| `witherProof` | bool | false | 是否抵御凋灵爆炸 |
| `beaconBase` | bool | false | 是否可作为信标基座 |
| `replaceable` | bool | 取决于材质 | 是否可直接替换 |
| `passable` | bool | 取决于材质 | 玩家是否可通过 |
| `dropHandler` | IBlockDropHandler | null | 自定义掉落物函数 |

| 方法 | 返回 | 说明 |
|------|------|------|
| `.register()` | void | 注册方块进游戏 |

### ContentTweaker 方块示例

```zenscript
#loader contenttweaker
import mods.contenttweaker.VanillaFactory;
import mods.contenttweaker.Block;

var antiIceBlock as Block = VanillaFactory.createBlock("anti_ice", <blockmaterial:ice>);
antiIceBlock.lightOpacity = 3;
antiIceBlock.blockHardness = 1.0;
antiIceBlock.blockResistance = 5.0;
antiIceBlock.toolClass = "pickaxe";
antiIceBlock.toolLevel = 0;
antiIceBlock.blockSoundType = <soundtype:snow>;
antiIceBlock.slipperiness = 0.75;
antiIceBlock.register();
```

---

## ZenUtils 扩展（需安装 ZenUtils + ContentTweaker）

> `import mods.zenutils.cotx.*;`

该部分是对 ContentTweaker 方块系统的扩展。(见上方ContentTweaker 扩展)

### VanillaFactory 方块扩展方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `VanillaFactory.createExpandBlock(String, IBlockMaterialDefinition)` | ExpandBlock | 创建扩展方块 |

### ExpandBlock（扩展方块）

> `import mods.zenutils.cotx.Block;`

继承 ContentTweaker 的 `BlockRepresentation`。

| 属性 | 类型 | 默认值 | 说明 |
|------|------|--------|------|
| `onBlockActivated` | IBlockActivated | null | 方块右键交互回调 |
| `onEntityWalk` | IEntityWalk | null | 实体踩踏回调 |
| `onEntityCollidedWithBlock` | IEntityCollided | null | 实体碰撞回调 |
| `tileEntity` | TileEntity | null | 关联的方块实体 |

#### IBlockActivated（函数式接口）

> `import mods.zenutils.cotx.IBlockActivated;`

| 参数 | 类型 |
|------|------|
| world | IWorld |
| pos | IBlockPos |
| state | ICTBlockState |
| player | ICTPlayer |
| hand | Hand |
| facing | Facing |
| blockHit | Position3f |

返回 `bool`。

#### IEntityWalk（函数式接口）

> `import mods.zenutils.cotx.IEntityWalk;`

参数：`IWorld`, `IBlockPos`, `IEntity`。返回 void。

#### IEntityCollided（函数式接口）

> `import mods.zenutils.cotx.IEntityCollided;`

参数：`IWorld`, `IBlockPos`, `ICTBlockState`, `IEntity`。返回 void。

### LateSetCoTFunction 方块部分

| Bracket | 返回 | 说明 |
|------|------|------|
| `<cotBlock:name>` | IBlockRepresentation | 获取 ContentTweaker 方块 |

| 方法 | 返回 | 说明 |
|------|------|------|
| `VanillaFactory.putTileEntityTickFunction(int, ITileEntityTick)` | void | 注册方块实体 tick 函数（可重载） |

---

## RandomTweaker 扩展（需安装 RandomTweaker）

> `import mods.randomtweaker.vanilla.IBlockPos;`

IBlockPos 的扩展类，IBlockPos 实例可直接使用这些方法。

### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `IBlockPos.getAllInBox(from as IBlockPos, to as IBlockPos)` | IBlockPos[] | 返回 from 到 to 范围内所有的 IBlockPos 对象集合。只能用类名调用，用对象调用会报错 |

### 扩展实例方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.add(x as int, y as int, z as int)` | IBlockPos | 返回坐标偏移 xyz 后的新坐标 |
| `.up(@Optional n as int)` | IBlockPos | 返回坐标向上偏移 n 格后的新坐标，默认 n=1 |
| `.down(@Optional n as int)` | IBlockPos | 返回坐标向下偏移 n 格后的新坐标，默认 n=1 |
| `.north(@Optional n as int)` | IBlockPos | 返回坐标向北偏移 n 格后的新坐标，默认 n=1 |
| `.south(@Optional n as int)` | IBlockPos | 返回坐标向南偏移 n 格后的新坐标，默认 n=1 |
| `.west(@Optional n as int)` | IBlockPos | 返回坐标向西偏移 n 格后的新坐标，默认 n=1 |
| `.east(@Optional n as int)` | IBlockPos | 返回坐标向东偏移 n 格后的新坐标，默认 n=1 |
