# SHRED: (S)ystem for (H)igh-performance (R)eal-time (E)lectric guitar (D)igital effects
**SHRED：高性能实时电吉他数字效果系统**

如有任何问题，欢迎提交 Issues 和 PR。

**警告！本项目尚未经过长期生产环境充分测试，不提供任何形式的担保。使用风险自负！**

## 许可证

本项目采用 LGPL-2.1 或更高版本许可证。

在仔细阅读并同意许可证条款之前，**请勿**下载或克隆本项目。

## 待办事项

1. 插接子板设计
2. FPGA RTL 集成
3. 控制器固件

## 项目概述

本项目为电吉他实现了一套音频系统，包含核心组件：硬件（核心板与插接板）及其 Gerber 文件和原理图、数字逻辑设计、护板机械设计，以及提供人机交互界面和系统控制的低功耗微控制器固件。

本项目不包含 TFT 屏幕相关，需从微雪电子购买（[点击此处](https://www.waveshare.net/wiki/1.9inch_LCD_Module)）。

![PCB 预览图](https://github.com/antercreeper/shred/blob/main/core_preview.jpg?raw=true)

## 功能特性

- 音频录制与回放（SD 卡）
- 音频混音器
- USB 音频输入输出
- 无线 BLE 实时音频监听
- 音频效果（合唱、失真、均衡器等）

## 目录结构

### Core（核心板）

该目录包含主板的 PCB 设计文件（KiCad），实现了系统的主要功能。包括电池管理（TI `BQ25601` 充电芯片配合 `TPD2S300` 实现 Type-C PD 高压快充，以及 TI `BQ27720` 电量计）、系统微控制器（沁恒微 `CH32X035`）、FPGA 单元（高云 `Tang Primer 25K`），以及音频子系统（ADI/美信 `MAX9850` I2S DAC + 安森美 `FAN3852` 模拟前端+ADC 转 PDM，以及 Skyworks/芯科实验室 `Si5351` 时钟发生器）。此外，系统还集成了 BLE 模块（Nordic `nRF5340`），提供超低延迟 LE 音频流媒体功能。

电源轨经过精心设计，以实现超长续航。系统采用多颗负载开关（MPS `MP5095` 和 Diodes `AP2151`）以及超低静态电流稳压器（TI `TPS62743` 和 `TPS7A20`），可将特定组件（按键与屏幕、音频系统、闪存、蓝牙）关闭或置于低功耗状态下。

双线圈拾音器通过 IPEX-4 接口连接（需要一定的焊接工作来改装拾音器连接线），可提供低噪声的纯净原始信号。

### Plug（插接板）

该目录包含插接子板的 PCB 设计文件（KiCad），包括 `音频接口`、`microSD 卡槽`、`USB-C 插座`、`充电指示灯` 和 `环境光传感器`。

### RTL（寄存器传输级）

该目录包含音频处理逻辑：
- 核心处理器
- 音频合成器
- FLAC 编解码器
- 音频输入输出接口
- USB 设备接口
- I2C 设备接口
- SD 主控制器接口

### Controller（控制器）

该目录包含系统控制器固件，负责初始化所有设备、监测系统状态、渲染人机交互界面，并响应用户输入事件。

### LE-Audio（低功耗音频）

该目录包含来自独立仓库的 BLE 模块固件子项目。该模块可扫描、连接并配对耳机，然后进行实时音频流媒体传输（LC3 编解码）。此模块作为系统控制器的外设，通过 UART 使用标准 AT 指令集进行通信。

### Others（其他）

根目录下的杂项文件：
- `pickguard.dxf`：护板 CAD 设计文件。
- `logo.jped`: `SHRED` Logo，由 Google NanoBanana 2 生成。
- `logo.prompt`: Logo 生成提示词。

## 使用说明

**本章节正在建设中，将在未来完善。**

[![星标历史图表](https://api.star-history.com/svg?repos=antercreeper/shred&type=date&legend=top-left)](https://www.star-history.com/#antercreeper/shred&type=date&legend=top-left)