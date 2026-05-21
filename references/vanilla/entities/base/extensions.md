# 实体扩展 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 部分需要 ZenUtils
> 导入: `import mods.zenutils.*;`

实体掉落示例、IEntity 扩展、IEntityDefinition 扩展。

---

## 使用示例

### 生物掉落示例

```zenscript
val sheep = <entity:minecraft:sheep>;

// 添加掉落：物品, 最小数量, 最大数量, 几率
sheep.addDrop(<minecraft:apple>);
sheep.addDrop(<minecraft:stone> % 20);  // 权重 20

// 仅玩家击杀掉落
sheep.addPlayerOnlyDrop(<minecraft:gold_ingot>, 10, 64);
sheep.addPlayerOnlyDrop(<minecraft:iron_ingot> % 20, 1, 3);

// 移除掉落
sheep.removeDrop(<minecraft:wool>);

// 清除所有掉落
sheep.clearDrops();

// 创建和生成实体
val world = crafttweaker.world.IWorld.getFromString("overworld"); // 示例
<entity:minecraft:sheep>.spawnEntity(world, blockPos);
```

---

## ZenUtils 扩展（需安装 ZenUtils）

> `import mods.zenutils.*;`

### IEntity 扩展

对 `crafttweaker.entity.IEntity` 的扩展，所有实体对象自动可用。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.setMotionX(double)` | void | 设置 X 轴速度 |
| `.setMotionVector(IVector3d)` | void | 设置速度向量 |
| `.getUUIDObject()` | CrTUUID | 获取实体的 UUID 对象 |
| `.updateNBT(IData)` | void | 更新实体 NBT 数据。与 CraftTweaker 的 `setNBT` 不同，此方法修改实体的完整 NBT，而非仅 ForgeData |

```zenscript
// 设置实体速度
entity.setMotionX(0.5);
entity.setMotionVector(crafttweaker.world.IVector3d.create(0.5, 1.0, 0.5));

// 获取 UUID 对象
val uuid = entity.getUUIDObject();

// 更新完整 NBT（区别于仅修改 ForgeData 的 setNBT）
entity.updateNBT({CustomName: "自定义名称"});
```

### IEntityDefinition 扩展

对 `crafttweaker.entity.IEntityDefinition` 的扩展。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.onTick(IEntityTick, @Optional int)` | void | 为特定实体类型添加周期性 tick 回调。仅服务端执行，无需检查 `world.remote`。第二个参数为间隔 tick 数 |

```zenscript
// 每 50 tick 对所有苦力怕执行一次
<entity:minecraft:creeper>.onTick(function(entity) {
    print("creeper? " ~ entity.world.time);
}, 50);
```
