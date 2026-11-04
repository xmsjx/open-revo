# OpenRevo 个人修改版

> 本仓库是 [OpenRevo](https://github.com/faintonce/open-revo)（机械革命 / 同方笔记本控制中心）的**个人修改分支**，非官方版本。
> 此处只说明本分支新增与修改的功能；软件的完整介绍、安装方式与上游功能请查看上游仓库。

## 本分支的修改

### 电池与供电

- **电池读取**：适配器类型 / 功率、充电功率、电池循环次数
- **Type-C 适配器功率识别**：`0x7CD` / `0x7CE` 双地址读取（含 3 次 ×100ms 防抖），圆口沿用 `0x49F` 编码
- **充电功率兜底**：电池 IOCTL 返回 0 时改用 `NtPowerInformation(SystemBatteryState)`
- **接电判断**：改用系统 `ACLineStatus`，Type-C 供电不再误显示「电池供电」
- **限充写入**：上限 + 下限（上限-5）、门控脉冲、清上限寄存器
- **Windows 智能充电提示开关**：默认关闭，可在设置页开启

### 性能与功耗

- **平衡模式 Dynamic Boost 默认关闭**，可在设置页手动开启；顶部「原厂目标 TGP」跟随开关显示
- **GPU OC 默认值**：core / mem 偏移可在设置页配置（本分支改动）
- **静音狂暴**：不再依赖 OEM 注册表，改用 MULong 能力探测 + EC 选择位，负探测 5 秒可重试

### 灯光与显示

- **键盘灯光**：单色呼吸（白/红/绿/蓝）、六色轮换、速度调节、恢复默认复位
- **内置息屏**：usbmmidd 虚拟屏方案，物理屏熄灭但系统继续运行，鼠标移动恢复；退出 / 停服务 / 异常退出均清理残余虚拟屏

### 监控

- **LHM 监控兜底**：内置传感器读取失败时，读取 LHM 外置插件写入的状态文件兜底（插件可选安装）

## 开源协议

- 本项目沿用上游 **GPL-3.0** 协议，详见 [LICENSE](LICENSE)
- 上游项目：https://github.com/faintonce/open-revo

### 第三方组件与引用

- **usbmmidd_v2**：© Amyuni Technologies，随程序分发，许可见 `src-tauri/resources/usbmmidd_v2/License.txt`
- **NullSignal**：息屏方案参考（IYATT-yx，MIT License）
- **LibreHardwareMonitor**：https://github.com/LibreHardwareMonitor/LibreHardwareMonitor （MPL-2.0）
- **HidSharp**：https://github.com/IntergatedCircuits/HidSharp （Apache-2.0）

以上组件/项目的版权归原作者所有，本分支仅按各自许可使用。
