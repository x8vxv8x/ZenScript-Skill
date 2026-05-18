# GlStateManager API 参考

> Mod ID: `eventtweaker`
> 前置条件: 无
> 导入: `import mods.eventtweaker.GlStateManager;`

EventTweaker 提供的独立工具类。事件相关 API 请参见 `references/vanilla/events/other.md`，客户端信息 API 请参见 `references/vanilla/game.md`。

---

## API 列表

### GlStateManager（渲染状态管理）

> `import mods.eventtweaker.GlStateManager;`

提供 OpenGL 渲染状态控制和基础绘图功能。

#### 渲染状态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.enableLighting()` | 未说明 | 启用光照 |
| `.disableLighting()` | 未说明 | 禁用光照 |
| `.enableTexture2D()` | 未说明 | 启用 2D 纹理 |
| `.disableTexture2D()` | 未说明 | 禁用 2D 纹理 |
| `.disableAlpha()` | 未说明 | 禁用 Alpha 测试 |
| `.enableBlend()` | 未说明 | 启用混合 |
| `.disableBlend()` | 未说明 | 禁用混合 |
| `.enableColorLogic()` | 未说明 | 启用颜色逻辑运算 |
| `.disableColorLogic()` | 未说明 | 禁用颜色逻辑运算 |
| `.enableColorMaterial()` | 未说明 | 启用颜色材质 |
| `.disableColorMaterial()` | 未说明 | 禁用颜色材质 |
| `.enableCull()` | 未说明 | 启用面剔除 |
| `.disableCull()` | 未说明 | 禁用面剔除 |
| `.enableFog()` | 未说明 | 启用雾效 |
| `.disableFog()` | 未说明 | 禁用雾效 |
| `.enableDepth()` | 未说明 | 启用深度测试 |
| `.disableDepth()` | 未说明 | 禁用深度测试 |
| `.enableNormalize()` | 未说明 | 启用法线归一化 |
| `.disableNormalize()` | 未说明 | 禁用法线归一化 |
| `.enablePolygonOffset()` | 未说明 | 启用多边形偏移 |
| `.disablePolygonOffset()` | 未说明 | 禁用多边形偏移 |

#### 变换方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.translate(float x, float y, float z)` | 未说明 | 平移变换 |
| `.rotate(float angle, float x, float y, float z)` | 未说明 | 旋转变换（角度 + 轴向量） |
| `.scale(float x, float y, float z)` | 未说明 | 缩放变换 |
| `.color(float red, float green, float blue)` | 未说明 | 设置颜色（RGB） |
| `.clearColor(float red, float green, float blue, float alpha)` | 未说明 | 设置清除颜色（RGBA） |

#### 绘图方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.renderImage(string str)` | 未说明 | 渲染图片，str 为图片路径/资源位置 |
| `.createTessellator(float x1, float y1, float z1, float x2, float y2, float z2, float x3, float y3, float z3, float x4, float y4, float z4)` | 未说明 | 创建四边形 Tessellator（4 个 3D 顶点，共 12 个 float） |
| `.draw()` | 未说明 | 绘制 Tessellator 缓冲 |
