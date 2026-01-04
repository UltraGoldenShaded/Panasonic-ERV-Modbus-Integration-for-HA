# Panasonic-ERV-Modbus-Integration-for-HA
# 松下新风系统 Home Assistant 接入方案 (Modbus 协议)

本项目提供了一套完整的配置方案，用于通过 Modbus TCP 协议将松下新风系统接入 Home Assistant。支持模式切换、风量控制、正压设定、滤网寿命监控及 PM2.5 数据读取。
## ⚠️ **免责声明**
1.本配置涉及 Modbus 通讯写入，请确保硬件接线正确。

2.不同型号的松下新风机寄存器地址可能略有不同，本项目基于FV-25ZDP2C，请参照设备说明书进行核对，如有不同之处需在 address后填写正确的寄存器地址。

3.作者不对因配置错误导致的设备故障负责。
## ✨ 功能特点

* **全功能控制**：开关、热交换/内循环/消毒/自动模式切换、风量调节（低噪音/弱/强）。
* **高级设定**：支持正压模式开关及强度调节、度假模式、高静压模式。
* **状态同步**：双向通信，物理面板操作会实时同步回 Home Assistant。
* **滤网监控**：实时显示下次滤网清洁时间以及 PM2.5、各类滤网（初效、集尘、送风等）的剩余寿命。
* **美观界面**：提供基于 Mushroom Cards 的现代化仪表盘配置。

## 🛠️ 硬件准备

1.  **松下RS485设备**：本项目使用FY-RS15ZDP2C，其他型号暂未做研究
2.  **串口服务器**：本项目使用 **USR-W610** (RS485 转 WiFi/Ethernet)
    * *配置提示*：需将串口服务器设置为 **TCP Server** 模式，波特率通常为 `9600`，数据位 `8`，停止位 `1`，校验位 `None` (具体请参考新风说明书)。

## 📦 软件依赖 (HACS)

仪表盘代码依赖以下第三方卡片，请通过 HACS 提前安装：

* [Mushroom Cards](https://github.com/piitaya/lovelace-mushroom)
* [Mini Graph Card](https://github.com/kalkih/mini-graph-card)

## 🚀 安装步骤

### 1. 修改 `configuration.yaml`

将本项目提供的 `panasonic_erv.yaml` 内容复制到你的配置文件中。

> ⚠️ **注意**：请务必修改 `host` 字段为你实际的串口服务器 IP 地址。
> 
### 2. 修改 `automations.yaml`

将 automations.yaml 中的内容复制到你的自动化配置文件中。

这些自动化负责在 Home Assistant 的下拉菜单 (input_select) 和 Modbus 寄存器之间进行双向数据同步。

### 3. 创建仪表盘
在 Home Assistant 前端页面，新建一个视图（View），选择 YAML 模式（或使用“手动”卡片），粘贴 dashboard.yaml 中的代码。
