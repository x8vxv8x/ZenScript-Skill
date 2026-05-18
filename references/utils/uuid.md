# CrTUUID（UUID 工具）

> 需安装 ZenUtils
> 导入: `import mods.zenutils.UUID;`

---

## 静态方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `UUID.randomUUID()` | 无 | CrTUUID | 创建随机 UUID |
| `UUID.fromString(String)` | String | CrTUUID | 从字符串解析 UUID |

## 实例方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `entity.getUUIDObject()` | 无 | CrTUUID | 获取实体的 UUID 对象（实体扩展方法） |
| `getMostSignificantBits()` | 无 | long | 获取高 64 位 |
| `getLeastSignificantBits()` | 无 | long | 获取低 64 位 |
| `asString()` | 无 | String | 转为字符串 |

支持 `==`、`>`、`<` 等比较运算符。

## 示例

```zenscript
import mods.zenutils.UUID;

var uuid = UUID.randomUUID();
print(uuid.asString());
```
