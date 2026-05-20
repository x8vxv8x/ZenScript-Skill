# Players CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.player.IPlayer;`、`import crafttweaker.player.IFoodStats;`、`import crafttweaker.player.IUser;`

玩家 API，用于操作玩家属性、物品栏和数据。

---

## API 列表

### IPlayer（玩家）

> `import crafttweaker.player.IPlayer;`

IPlayer 继承 IEntityLivingBase，IEntityLivingBase 继承 IEntity。

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 玩家名称 |
| `displayName` | string | 显示名称 |
| `uuid` | string | UUID |
| `xp` | int | 经验值 |
| `xpLevel` | int | 经验等级 |
| `xpCap` | int | 当前等级经验上限 |
| `health` | float | 生命值 |
| `maxHealth` | float | 最大生命值 |
| `foodLevel` | int | 饥饿值 |
| `saturation` | float | 饱和度 |
| `creative` | bool | 是否创造模式 |
| `isCreative` | bool | 是否创造模式（同 creative） |
| `isSpectator` | bool | 是否旁观者模式 |
| `adventure` | bool | 是否冒险模式 |
| `isAdventure` | bool | 是否冒险模式（同 adventure） |
| `isSurvival` | bool | 是否生存模式 |
| `isFlying` | bool | 是否飞行 |
| `isSleeping` | bool | 是否睡觉 |
| `isSneaking` | bool | 是否潜行 |
| `isSprinting` | bool | 是否冲刺 |
| `isElytraFlying` | bool | 是否鞘翅飞行 |
| `isBlocking` | bool | 是否格挡 |
| `isBurning` | bool | 是否着火 |
| `isInWater` | bool | 是否在水中 |
| `isOnGround` | bool | 是否在地面上 |
| `isRiding` | bool | 是否骑乘 |
| `isInvisible` | bool | 是否隐身 |
| `isInvulnerable` | bool | 是否无敌 |
| `isDead` | bool | 是否死亡 |
| `isEntityAlive` | bool | 是否存活 |
| `dimension` | int | 维度 ID |
| `world` | IWorld | 所在世界 |
| `position` | IBlockPos | 位置 |
| `x` | double | X 坐标 |
| `y` | double | Y 坐标 |
| `z` | double | Z 坐标 |
| `eyeHeight` | float | 眼睛高度 |
| `rotationYaw` | float | 偏航角 |
| `rotationPitch` | float | 俯仰角 |
| `offHandHeldItem` | IItemStack | 副手物品 |
| `mainHandHeldItem` | IItemStack | 主手物品 |
| `inventory` | IInventory | 物品栏 |
| `data` | IData | 玩家数据 |
| `team` | ITeam | 所属队伍 |
| `gameType` | string | 游戏模式 |
| `hotbarSize` | int | 快捷栏大小 |
| `inventorySize` | int | 背包大小 |
| `currentItem` | IItemStack | 当前手持物品 |
| `foodStats` | IFoodStats | 食物状态 |
| `bedLocation` | IBlockPos | 床的位置 |
| `fishHook` | IEntity | 鱼钩实体 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.update(IData)` | void | 更新玩家数据 |
| `.give(IItemStack)` | void | 给予物品 |
| `.sendChat(string)` | void | 发送消息 |
| `.sendChat(IChatMessage)` | void | 发送富文本消息 |
| `.sendStatusMessage(string, @Optional bool)` | void | 发送状态消息。第二个参数为 true 时显示在快捷栏 |
| `.sendRichTextStatusMessage(ITextComponent, @Optional bool)` | void | 发送富文本状态消息 |
| `.sendToast(string, string)` | void | 发送通知 |
| `.executeCommand(string)` | void | 执行命令 |
| `.attackEntityFrom(IDamageSource, float)` | void | 造成伤害 |
| `.heal(float)` | void | 治疗 |
| `.setHealth(float)` | void | 设置生命值 |
| `.setFoodLevel(int)` | void | 设置饥饿值 |
| `.setSaturation(float)` | void | 设置饱和度 |
| `.addExperience(int)` | void | 添加经验 |
| `.removeXP(int)` | void | 移除经验等级 |
| `.setXPLevel(int)` | void | 设置经验等级 |
| `.getHeldItem(EnumHand)` | IItemStack | 获取手持物品 |
| `.setItemToSlot(EntityEquipmentSlot, IItemStack)` | void | 设置装备 |
| `.hasGameRule(string)` | bool | 是否有游戏规则 |
| `.getGameRule(string)` | string | 获取游戏规则 |
| `.getHotbarStack(int)` | IItemStack | 获取快捷栏指定位置的物品 |
| `.getInventoryStack(int)` | IItemStack | 获取背包指定位置的物品 |
| `.teleport(Position3f)` | void | 传送到指定位置（同一维度） |
| `.dropItem(bool)` | void | 丢弃当前手持物品。true 丢弃整个堆叠 |
| `.dropItem(IItemStack)` | void | 在玩家位置丢弃指定物品 |
| `.getCooldown(IItemStack)` | int | 获取指定物品的冷却时间 |
| `.setCooldown(IItemStack, int)` | void | 设置指定物品的冷却时间 |

### IFoodStats（食物状态）

> `import crafttweaker.player.IFoodStats;`

IFoodStats 用于查看和操作玩家的食物状态，通过 `player.foodStats` 获取。

#### @ZenGetter / @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `foodLevel` | int | 饥饿值（可读写） |
| `saturationLevel` | float | 饱和度（可读写） |
| `needFood` | bool | 是否需要食物 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.addStats(int, float)` | void | 添加食物值和饱和度 |
| `.onUpdate(IPlayer)` | void | 更新食物状态 |
| `.asNBT()` | IData | 获取食物状态的 NBT 数据 |
| `.addExhaustion(float)` | void | 添加疲劳值 |

### IUser（用户接口）

> `import crafttweaker.player.IUser;`

IUser 是一个内部接口，用于统一不同用户类型（控制台、玩家、命令方块）。IUser 继承 ICommandSender。IUser 目前没有独有的方法。

---

## 使用示例

### 玩家数据持久化

#### 写入数据

```zenscript
events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if (event.player.world.remote) return;
    // 写入到 ForgeData（死亡时清空）
    event.player.update({custom: 1 as byte});
    // 写入到 PlayerPersisted（死亡后保留）
    event.player.update({PlayerPersisted: {custom: 1}});
});
```

#### 读取数据

```zenscript
events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if (event.player.world.remote) return;
    var data = event.player.data;
    if (!isNull(data.PlayerPersisted.custom)) {
        val value = data.PlayerPersisted.custom.asInt();
        print(value);
    }
});
```

#### 修改数据

```zenscript
// 不能直接赋值：event.player.data.PlayerPersisted.custom = 10; // 错误！
// 需要用 update 覆盖
event.player.update({PlayerPersisted: {custom: 10}});
```

---

## ZenUtils 扩展（需安装 ZenUtils）

> `import mods.zenutils.*;`

### IPlayer 扩展

对 `crafttweaker.player.IPlayer` 的扩展，所有玩家对象自动可用。

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.replaceItemInInventory(int slot, IItemStack stack)` | bool | 替换玩家背包指定槽位的物品 |
| `.readStat(PlayerStat stat)` | int | 读取统计值 |
| `.addStat(PlayerStat stat, @Optional int amount)` | void | 增加统计计数（默认 1） |
| `.takeStat(PlayerStat stat)` | void | 将统计值重置为 0 |

### 玩家交互模拟

@since 1.14.3

模拟玩家交互（左键/右键），仅应在服务端调用。

#### simulateRightClickItem

模拟玩家右键使用物品（不指向方块或实体）。

| 参数 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| item | IItemStack | 使用的物品 | |
| hand | IEntityEquipmentSlot | 使用的手（仅 mainHand/offHand） | mainHand |

返回 `String`：`SUCCESS`、`PASS` 或 `FAIL`

#### simulateRightClickBlock

模拟玩家右键点击方块。

| 参数 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| item | IItemStack | 使用的物品 | |
| hand | IEntityEquipmentSlot | 使用的手 | mainHand |
| pos | IBlockPos | 方块位置 | 根据玩家视线确定 |
| side | IFacing | 点击的方块面 | 根据玩家视线确定 |
| hitX | float | 点击相对 X 坐标（0~1） | 根据玩家视线确定 |
| hitY | float | 点击相对 Y 坐标（0~1） | 根据玩家视线确定 |
| hitZ | float | 点击相对 Z 坐标（0~1） | 根据玩家视线确定 |

返回 `String`：`SUCCESS`、`PASS` 或 `FAIL`

#### simulateRightClickEntity

模拟玩家右键点击实体。

| 参数 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| entity | IEntity | 目标实体 | |
| item | IItemStack | 使用的物品 | 手中物品 |
| hand | IEntityEquipmentSlot | 使用的手 | mainHand |

返回 `String`：`SUCCESS`、`PASS` 或 `FAIL`

#### simulateLeftClickBlock

模拟玩家左键点击方块。

| 参数 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| item | IItemStack | 使用的物品 | 主手物品 |
| pos | IBlockPos | 方块位置 | 根据玩家视线确定 |
| side | IFacing | 点击的方块面 | 根据玩家视线确定 |

无返回值。

#### simulateUseItemFinish

模拟玩家完成使用物品（如吃完食物）。返回结果物品（如牛奶桶→空桶）。

| 参数 | 类型 | 说明 | 默认值 |
|------|------|------|--------|
| item | IItemStack | 使用的物品 | |
| hand | IEntityEquipmentSlot | 使用的手 | 当前激活手 |

### PlayerStat（玩家统计）

> `import mods.zenutils.PlayerStat;`

#### 获取 PlayerStat

| 方法 | 返回 | 说明 |
|------|------|------|
| `PlayerStat.getBasicStat(String)` | PlayerStat | 获取基础统计（用 `/ct stats` 查看所有） |
| `PlayerStat.getBlockStats(IBlockDefinition)` | PlayerStat | 方块相关统计 |
| `PlayerStat.getCraftStats(IItemDefinition)` | PlayerStat | 合成统计 |
| `PlayerStat.getObjectUseStats(IItemDefinition)` | PlayerStat | 物品使用统计 |
| `PlayerStat.getObjectBreakStats(IItemDefinition)` | PlayerStat | 物品破坏统计 |
| `PlayerStat.getObjectsPickedUpStats(IItemDefinition)` | PlayerStat | 物品拾取统计 |
| `PlayerStat.getDroppedObjectStats(IItemDefinition)` | PlayerStat | 物品掉落统计 |
| `PlayerStat.getKillEntityStats(IEntityDefinition)` | PlayerStat | 击杀实体统计 |
| `PlayerStat.getKilledByEntityStats(IEntityDefinition)` | PlayerStat | 被实体击杀统计 |

#### 创建 PlayerStat

| 方法 | 返回 | 说明 |
|------|------|------|
| `PlayerStat.create(String id, ITextComponent name, @Optional IStatFormatter)` | PlayerStat | 创建自定义统计（需在游戏初始化阶段调用） |

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | ITextComponent | 统计名称 |

#### 玩家统计操作

| 方法 | 返回 | 说明 |
|------|------|------|
| `player.readStat(PlayerStat)` | int | 读取统计值 |
| `player.addStat(PlayerStat, @Optional int)` | void | 增加统计计数（默认 1） |
| `player.takeStat(PlayerStat)` | void | 重置统计值为 0 |

### IStatFormatter（统计格式化器）

> `import mods.zenutils.IStatFormatter;`

函数式接口：接收 `int`，返回 `string`。

| 预置格式化器 | 说明 |
|------|------|
| `IStatFormatter.simple()` | 数字分组显示（默认） |
| `IStatFormatter.time()` | 时间格式显示 |
| `IStatFormatter.distance()` | 距离单位显示 |
| `IStatFormatter.divideByTen()` | 除以十后显示 |

| 工具方法 | 返回 | 说明 |
|------|------|------|
| `IStatFormatter.numberFormat(int)` | string | 格式化整数（分组分隔符） |
| `IStatFormatter.decimalFormat(double)` | string | 格式化小数（保留2位） |

---

## Roids-Tweaker 扩展

### IPlayer 扩展

可在任何 IPlayer 上调用。

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `.addExperience(int amount)` | amount | void | 添加经验点（非等级） |
| `.removeExperience(int amount)` | amount | void | 移除经验点 |
| `.getTotalXP()` | 无 | int | 获取总经验量 |
| `.playSound(String sound, float volume, float pitch)` | sound, volume, pitch | void | 播放声音。客户端和服务端玩家行为不同，检查 `world.remote` 判断端 |
| `.sendPlaySoundPacket(String sound, String category, Position3f pos, float volume, float pitch)` | sound, category, pos, volume, pitch | void | 使玩家客户端播放声音 |
| `.isPlayerMP()` | 无 | bool | 是否为 EntityPlayerMP 实例（服务端玩家） |
| `.isFake()` | 无 | bool | 是否为 FakePlayer 实例 |
| `.getAdvancementProgress(IAdvancement advancement)` | advancement | IAdvancementProgress | 获取进度完成状态。玩家必须是 EntityPlayerMP 实例，否则返回 null |

### IRandom 扩展

可在任何 IRandom 上调用。

| 方法 | 返回 | 说明 |
|------|------|------|
| `.nextGaussian()` | double | 返回服从标准正态分布的随机 double |
