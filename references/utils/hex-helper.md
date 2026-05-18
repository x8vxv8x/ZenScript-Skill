# HexHelper（十六进制工具）CraftTweaker API 参考

> Mod ID: 无
> 前置条件: ZenUtils
> 导入: `import mods.zenutils.HexHelper;`

十六进制转换工具。

---

## API 列表

### HexHelper（十六进制工具）

> `import mods.zenutils.HexHelper;`

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `HexHelper.toHexString(int)` | String | 十进制转十六进制字符串 |
| `HexHelper.toDecInteger(String)` | int | 十六进制字符串转十进制 |

---

## 使用示例

```zenscript
HexHelper.toDecInteger("ABCDEF"); // 返回 11259375
HexHelper.toHexString(114514);    // 返回 "1bf52"
```
