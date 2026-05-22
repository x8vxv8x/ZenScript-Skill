# 村庄 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: 见各章节

村庄系统 API，用于查询和操作村庄状态。

---

## CraftTweakerAdditions 扩展（需安装 CraftTweakerAdditions）

### IVillage

> `import mods.crtadd.vanilla.IVillage;`

#### @ZenGetter
| 属性 | 类型 | 说明 |
|------|------|------|
| `reputation` | int | 获取玩家在村庄的声望 |
| `isPlayerReputationTooLow` | bool | 获取玩家声望是否过低（会导致铁傀儡攻击） |
| `center` | IBlockPos | 获取村庄中心位置 |
| `villageRadius` | int | 获取村庄半径 |
| `numVillageDoors` | int | 获取村庄有效门的数量 |
| `numVillagers` | int | 获取村庄内村民的数量 |
| `isAnnihilated` | bool | 获取村庄是否已被摧毁 |

#### @ZenSetter
| 属性 | 类型 | 说明 |
|------|------|------|
| `reputation` | int | 设置玩家在村庄的声望 |
| `village` | [IVillage] | 获取玩家所在位置的村庄（搜索半径 32 格），未找到村庄时返回 null |

#### 村庄方法
| 方法 | 返回 | 说明 |
|------|------|------|
| `.getExistedDoor(IBlockPos blockPos)` | bool | 检查指定位置是否存在有效门 |
| `.addOrRenewAgressor(IEntityLivingBase entity)` | void | 向村庄添加或刷新袭击者 |
| `.findNearestVillageAggressor(IEntityLivingBase entity)` | IEntityLivingBase | 获取距离指定实体最近的村庄袭击者 |
| `.isBlockPosWithinSqVillageRadius(IBlockPos blockPos)` | bool | 检查指定位置是否在村庄范围内 |

---

## 使用示例

```zenscript
// 获取玩家所在村庄
val village = player.village;
if (!isNull(village)) {
    val rep = village.reputation;
    print("当前声望: " ~ rep);
    if (village.isPlayerReputationTooLow) {
        print("警告：声望过低，铁傀儡可能会攻击你！");
    }
    village.reputation = rep + 10;
}
```