# OpenWRT-CI 云编译框架

## 📖 项目简介

本项目基于 GitHub Actions 构建，提供全自动化的 OpenWRT 固件云编译服务。通过自定义配置与脚本，实现对多平台、多设备固件的灵活定制。

**上游源码支持：**
* **官方版 (ImmortalWrt)**: `https://github.com/immortalwrt/immortalwrt.git`
* **高通优化版**: `https://github.com/VIKINGYFY/immortalwrt.git`

## ✨ 固件特性

* **定时自动化编译**：系统配置为每天自动拉取最新源码并执行编译任务（约早上 4:00）。
* **版本追溯便捷**：固件信息中的时间戳代表编译开始的时间，方便用户核对上游源码的具体提交记录。
* **默认网络配置**：
  * **后台地址**: `192.168.10.1`
  * **登录密码**: 无（首次登录请及时设置）
  * **默认 WIFI 名称**: `OWRT` / `ImmoralWRT`
  * **默认 WIFI 密码**: `12345678`
  * **默认后台主题**: `Argon`
* **开箱即用插件**：高度集成了 Homeproxy、OpenClash、Passwall、Tailscale 等主流应用，内置硬件加速，无需繁琐设置刷入即用。

## 🚀 支持平台与设备

当前仓库已配置并支持以下主流平台固件的生成，部分设备区分带有 WIFI 与无 WIFI 的精简版本：

* **高通系列 (QUALCOMMAX)**: 
  * 支持 IPQ50XX 平台（如：京东云 RE-CS-03）。
  * 支持 IPQ60XX 平台（如：京东云 RE-SS-01 等）。
  * 支持 IPQ807X 平台（如：阿里云 AP8220、红米 AX6、小米 AX3600 / AX9000 等）。
* **联发科系列 (MEDIATEK)**: 
  * 支持 Filogic 平台（涵盖 360 T7、华三 NX30 Pro、小米 WR30U / AX3000T、红米 AX6000、GL.iNet 等大量热门机型）。
* **瑞芯微 (ROCKCHIP)**: 
  * 支持 ARMv8 平台（如：FriendlyARM NanoPi R4S）。
* **瑞昱 (REALTEK)**: 
  * 支持 RTL930x 平台（如：兮克 SKS8300-8X 交换机路由器）。
* **X86 系列**: 
  * 支持传统 X86_64 架构平台，并自动生成适用于虚拟机的 GRUB 及 VMDK 镜像。

## 📂 目录结构与说明

* `.github/workflows/` —— **自定义 CI 配置**：包含自动清理机制、缓存管理及不同平台（OWRT-ALL、QCA-ALL等）的独立编译流水线。
* `Config/` —— **自定义配置**：按硬件平台划分的设备清单与编译参数列表，其中 `GENERAL.txt` 包含全局通用插件及系统基础特性设置。
* `Scripts/` —— **自定义脚本**：
  * `Packages.sh`: 用于自动克隆、替换及批量更新各类第三方插件源码。
  * `Handles.sh`: 深度定制系统环境，处理依赖冲突、菜单位置修改、启动顺序优化及预置分流规则资源。
  * `Settings.sh`: 固件底层参数注入（IP 地址、WIFI 账号密码、内核调整及默认语言主题等设定）。
