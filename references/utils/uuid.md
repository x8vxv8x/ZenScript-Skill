# CrTUUID（UUID 工具）CraftTweaker API 参考

> Mod ID: 无
> 前置条件: ZenUtils
> 导入: `import mods.zenutils.UUID;`

UUID 工具。

---

## API 列表

### UUID（UUID 工具）

> `import mods.zenutils.UUID;`

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `UUID.randomUUID()` | CrTUUID | 创建随机 UUID |
| `UUID.fromString(String)` | CrTUUID | 从字符串解析 UUID |

#### 实例方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `entity.getUUIDObject()` | CrTUUID | 获取实体的 UUID 对象（实体扩展方法） |
| `getMostSignificantBits()` | long | 获取高 64 位 |
| `getLeastSignificantBits()` | long | 获取低 64 位 |
| `asString()` | String | 转为字符串 |

支持 `==`、`>`、`<` 等比较运算符。

---

## 使用示例

```zenscript
import mods.zenutils.UUID;

var uuid = UUID.randomUUID();
print(uuid.asString());
```
