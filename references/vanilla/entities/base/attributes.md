# 实体属性 CraftTweaker API 参考

> Mod ID: `minecraft`
> 前置条件: 无
> 导入: `import crafttweaker.entity.Attribute;`、`import crafttweaker.entity.AttributeInstance;`、`import crafttweaker.entity.AttributeModifier;`

IEntityAttribute、IEntityAttributeInstance、IEntityAttributeModifier 属性系统 API。

---

## API 列表

### IEntityAttribute（属性）

> `import crafttweaker.entity.Attribute;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `name` | string | 属性名称 |
| `defaultValue` | double | 默认值 |
| `shouldWatch` | boolean | 是否监控 |
| `parent` | IEntityAttribute | 父属性 |

#### 方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.clampValue(double)` | double | 将值限制在属性允许范围内 |

### IEntityAttributeInstance（属性实例）

> `import crafttweaker.entity.AttributeInstance;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `attribute` | IEntityAttribute | 属性定义 |
| `baseValue` | double | 基础值 |
| `modifiers` | List<IEntityAttributeModifier> | 修饰符列表 |
| `attributeValue` | double | 最终属性值 |

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `baseValue` | double | 设置基础值 |

#### 修饰符方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `.getModifiersByOperation(int)` | List<IEntityAttributeModifier> | 按操作类型获取修饰符 |
| `.hasModifier(IEntityAttributeModifier)` | boolean | 检查是否拥有指定修饰符 |
| `.getModifier(String)` | IEntityAttributeModifier | 按 UUID 获取修饰符 |
| `.applyModifier(IEntityAttributeModifier)` | void | 应用修饰符 |
| `.removeModifier(IEntityAttributeModifier)` | void | 移除修饰符 |
| `.removeModifier(String)` | void | 按 UUID 移除修饰符 |
| `.removeAllModifiers()` | void | 移除所有修饰符 |

### IEntityAttributeModifier（属性修饰符）

> `import crafttweaker.entity.AttributeModifier;`

#### @ZenGetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `uuid` | string | UUID |
| `name` | string | 名称 |
| `operation` | int | 操作类型（0=加法, 1=乘法基础, 2=乘法） |
| `amount` | double | 数值 |
| `saved` | boolean | 是否已保存 |

#### @ZenSetter

| 属性 | 类型 | 说明 |
|------|------|------|
| `saved` | boolean | 设置是否保存 |

#### 静态方法

| 方法 | 返回 | 说明 |
|------|------|------|
| `AttributeModifier.createModifier(String, double, int, @Optional String)` | IEntityAttributeModifier | 创建属性修饰符 |

操作类型说明：
- 0 = add：增加 X 由 Amount
- 1 = multiply_base：增加 Y 由 X * Amount
- 2 = multiply：Y = Y * (1 + Amount)
