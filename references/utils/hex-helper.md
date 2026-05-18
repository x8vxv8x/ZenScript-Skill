# HexHelper（十六进制工具）

> 需安装 ZenUtils
> 导入: `import mods.zenutils.HexHelper;`

---

## 方法

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `HexHelper.toHexString(int)` | int | String | 十进制转十六进制字符串 |
| `HexHelper.toDecInteger(String)` | String | int | 十六进制字符串转十进制 |

## 示例

```zenscript
HexHelper.toDecInteger("ABCDEF"); // 返回 11259375
HexHelper.toHexString(114514);    // 返回 "1bf52"
```
