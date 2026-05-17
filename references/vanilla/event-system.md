# 事件系统参考

## 概述

事件系统允许在游戏特定时间点执行自定义行为。

```zenscript
events.onPlayerCrafted(function(event){
    // 玩家合成时执行
});
```

---

## 事件监听

```zenscript
events.on<EventName>(function(event as <EventType>) {
    // 事件处理代码
});
```

---

## 常用事件

### 玩家合成事件

> `import crafttweaker.event.PlayerCraftedEvent;`

```zenscript
events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    val player = event.player;        // IPlayer
    val output = event.output;        // IItemStack 合成结果
    val inventory = event.inventory;  // ICraftingInventory
});
```

### 方块破坏掉落事件

> `import crafttweaker.event.BlockHarvestDropsEvent;`

```zenscript
events.onBlockHarvestDrops(function(event as BlockHarvestDropsEvent) {
    val block = event.block;          // IBlock
    val player = event.player;        // IPlayer
    val world = event.world;          // IWorld
    val drops = event.drops;          // WeightedItemStack[]
    val fortune = event.fortuneLevel; // int 时运等级
    val silkTouch = event.silkTouch;  // bool 精准采集
    val isPlayer = event.isPlayer;    // bool 是否玩家挖掘

    // 修改掉落物
    event.drops = [<item:minecraft:apple> % 100];
    event.addItem(<item:minecraft:arrow> * 2 % 20);
});
```

### 实体加入世界事件

> `import crafttweaker.event.EntityJoinWorldEvent;`

```zenscript
events.onEntityJoinWorld(function(event as EntityJoinWorldEvent) {
    val entity = event.entity;        // IEntity
    val definition = entity.definition; // IEntityDefinition

    // 阻止苦力怕生成
    if (!isNull(definition) && definition.id == "minecraft:creeper") {
        event.cancel();
    }
});
```

### 命令事件

> `import crafttweaker.event.CommandEvent;`

```zenscript
events.onCommand(function(event as CommandEvent) {
    val command = event.command.name;   // string 命令名
    val params = event.parameters;      // string[] 参数
    val sender = event.commandSender;   // ICommandSender

    // 阻止 /gamemode creative
    if (command == "gamemode" && (params in "creative")) {
        event.cancel();
    }
});
```

---

## 取消事件

使用 `event.cancel()` 取消事件，阻止原版行为。

```zenscript
events.onEntityJoinWorld(function(event as EntityJoinWorldEvent) {
    if (event.entity.definition.id == "minecraft:creeper") {
        event.cancel(); // 阻止苦力怕生成
    }
});
```

---

## 重要提示

### `!world.remote` 保证服务端执行

MC 分为服务端和客户端。与存档相关的操作（召唤实体、修改方块等）必须在服务端执行。

```zenscript
events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if (!event.player.world.remote) {
        // 只在服务端执行
        event.player.attackEntityFrom(<damageSource:MAGIC>, 1.0f);
    }
});
```

**原因**: 单人游戏也有内置的服务端和客户端。不加 `!world.remote` 会导致事件执行两次（客户端一次，服务端一次），出现重复实体等问题。

---

## 玩家数据持久化

### 写入数据

```zenscript
events.onPlayerCrafted(function(event as PlayerCraftedEvent) {
    if (event.player.world.remote) return;
    // 写入到 ForgeData（死亡时清空）
    event.player.update({custom: 1 as byte});
    // 写入到 PlayerPersisted（死亡后保留）
    event.player.update({PlayerPersisted: {custom: 1}});
});
```

### 读取数据

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

### 修改数据

```zenscript
// 不能直接赋值：event.player.data.PlayerPersisted.custom = 10; // 错误！
// 需要用 update 覆盖
event.player.update({PlayerPersisted: {custom: 10}});
```

---

## 常用游戏对象

| 类型 | 说明 |
|------|------|
| [IPlayer](https://docs.blamejared.com/1.12/en/Vanilla/Players/IPlayer/) | 玩家，继承 IEntityLivingBase |
| [IEntityLivingBase](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntityLivingBase/) | 实体基类，继承 IEntity |
| [IEntity](https://docs.blamejared.com/1.12/en/Vanilla/Entities/IEntity/) | 实体 |
| [IWorld](https://docs.blamejared.com/1.12/en/Vanilla/World/IWorld/) | 世界/维度 |
| [IBlockPos](https://docs.blamejared.com/1.12/en/Vanilla/World/IBlockPos/) | 坐标 |
| [IBlock](https://docs.blamejared.com/1.12/en/Vanilla/Blocks/IBlock/) | 方块 |
| [IBlockState](https://docs.blamejared.com/1.12/en/Vanilla/Blocks/IBlockState/) | 方块状态 |

---

## 可用事件列表

参见官方文档: [IEventManager](https://docs.blamejared.com/1.12/en/Vanilla/Events/IEventManager/)
