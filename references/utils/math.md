# Math API

> `import crafttweaker.util.Math;`

| 方法 | 参数 | 返回 | 说明 |
|------|------|------|------|
| `Math.max` | 2个 double/float/int/long | 同类型 | 最大值 |
| `Math.min` | 2个 double/float/int/long | 同类型 | 最小值 |
| `Math.floor` | double | int | 向下取整 |
| `Math.ceil` | double | int | 向上取整 |
| `Math.round` | double | int | 四舍五入 |
| `Math.abs` | double/float/int/long | 同类型 | 绝对值 |
| `Math.sqrt` | double | double | 开方 |
| `Math.log` | double | double | 自然对数 |
| `Math.log10` | double | double | 常用对数 |
| `Math.sin` | double | double | 正弦（弧度） |
| `Math.cos` | double | double | 余弦（弧度） |
| `Math.tan` | double | double | 正切（弧度） |
| `Math.asin` | double | double | 反正弦 |
| `Math.acos` | double | double | 反余弦 |
| `Math.atan` | double | double | 反正切 |
| `Math.sinh` | double | double | 双曲正弦 |
| `Math.cosh` | double | double | 双曲余弦 |
| `Math.tanh` | double | double | 双曲正切 |
| `Math.clamp` | 3个同类型 | 同类型 | 区间限制 clamp(x, min, max) |

```zenscript
import crafttweaker.util.Math;
Math.clamp(15, 10, 19);  // 15
Math.clamp(10, 12, 19);  // 12
Math.floor(3.7);          // 3
Math.ceil(3.2);           // 4
```
