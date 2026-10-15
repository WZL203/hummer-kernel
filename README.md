# Hummer Kernel (GKI 6.6)

[![Build Kernel](https://github.com/WZL203/hummer-kernel/actions/workflows/build.yml/badge.svg)](https://github.com/WZL203/hummer-kernel/actions)
[![License: GPL-2.0](https://img.shields.io/badge/License-GPL%202.0-blue.svg)](https://opensource.org/licenses/GPL-2.0)
[![Android](https://img.shields.io/badge/Android-15%2B-green.svg)](https://www.android.com/)

基于通用 Android GKI 6.6 内核构建的自定义分支，重点集成内核级权限控制与深度隐蔽方案，兼顾系统稳定性与运行效率。

---

## 📌 项目特性

- **通用 GKI 架构**：遵循 Google Android Common Kernel (ACK) 规范构建，适配兼容的 GKI 架构设备。
- **4K 页面对齐**：采用标准 4KB 内存分页大小（Page Size），保障针对非 16K 环境的深度兼容性。
- **Root 方案集成**：内置支持 KernelSU，提供高效的底层权限控制与隔离机制。
- **隐蔽增强 (SuSFS)**：同步集成 SuSFS 内核层补丁，消除挂载特征、隐藏敏感文件路径并协助通过严苛的应用环境检测。
- **自动化构建体系**：基于 GitHub Actions 提供持续集成（CI）与自动化 AnyKernel3 (AK3) 打包分发。

---

## ⚙️ 编译规格

| 配置项 | 规格说明 |
| :--- | :--- |
| **内核基线** | Linux Kernel 6.6.y (ACK) |
| **目标架构** | `aarch64` / `arm64` |
| **Page Size** | 4 KB (`CONFIG_ARM64_4K_PAGES=y`) |
| **工具链** | Clang / LLVM (AOSP Toolchain) |
| **核心组件** | KernelSU + SuSFS 2.x |

---

## 📦 刷入指南

> [!WARNING]
> 刷入第三方内核具有一定风险。在执行任何刷写操作前，请务必备份当前设备的 `boot` 及 `init_boot` 分区镜像。

### 方式一：通过 [ReKernelFlasher](https://github.com/Bacillusf/ReKernelFlasher)（推荐）
1. 在 [Releases](../../releases) 页面下载最新构建的 `AK3-*.zip` 刷机包。
2. 打开具备 Root 权限的 [ReKernelFlasher](https://github.com/Bacillusf/ReKernelFlasher) 或类似内核管理工具。
3. 选取下载的 zip 刷机包进行刷入并重启设备。

### 方式二：通过 Recovery
1. 设备重启至支持的三方 Recovery 界面。
2. 直接通过 `Apply update` 或 `Install` 刷入 `AK3-*.zip`。
3. 刷入完成后清除 Cache 并重启至系统。

### 方式三：通过 Fastboot 命令行刷入 `boot.img`
将手机连接电脑并开启 USB 调试，打开终端（PowerShell）执行以下指令：

```powershell
# 1. 进入 platform-tools 工具目录
cd C:\path\to\platform-tools

# 2. 重启设备至 Bootloader (Fastboot) 模式
.\adb reboot bootloader

# 3. 确认设备已正常连接
.\fastboot devices

# 4. 刷入内核镜像（请根据当前激活槽位选择 boot_a 或 boot_b，或直接刷入 boot）
.\fastboot flash boot_b C:\path\to\new-boot.img

# 5. 重启进入系统
.\fastboot reboot
