# Energy Storage CraftTweaker API 参考

> Mod ID: `ctintegration`
> 前置条件: roid's tweaker
> 导入: `import mods.ctintegration.IEnergyStorage;`

## API 列表

### IEnergyStorage

> `import mods.ctintegration.IEnergyStorage;`

操作能量（FE/RF）存储物品的接口。通过 `IItemStack.energy` 获取。使用前确保物品是能量存储设备！

| 方法 | 返回 | 说明 |
|------|------|------|
| `.receiveEnergy(int maxReceive, @Optional boolean simulate)` | int | 添加能量，返回实际接收量 |
| `.extractEnergy(int maxExtract, @Optional boolean simulate)` | int | 提取能量，返回实际提取量 |
| `.getEnergyStored()` | int | 获取当前存储能量 |
| `.getMaxEnergyStored()` | int | 获取最大存储能量 |
| `.canExtract()` | boolean | 是否可提取能量（也是 ZenGetter） |
| `.canReceive()` | boolean | 是否可接收能量（也是 ZenGetter） |
