# Hummer Kernel (GKI 6.6)

[![Build Kernel](https://github.com/WZL203/hummer-kernel/actions/workflows/build.yml/badge.svg)](https://github.com/WZL203/hummer-kernel/actions)
[![License: GPL-2.0](https://img.shields.io/badge/License-GPL%202.0-blue.svg)](https://opensource.org/licenses/GPL-2.0)
[![Android](https://img.shields.io/badge/Android-17-green.svg)](https://www.android.com/)

面向 OnePlus Ace 5 Pro（hummer / PKR110）的自定义内核，基于 LineageOS 24.0 官方内核树构建，集成 FinaSU 与 SUSFS，兼顾系统稳定性与运行效率。

> [!IMPORTANT]
> **本内核仅适用于 LineageOS 24.0（Android 17）。** crDroid、ColorOS 等其他系统请勿刷入——上一版收到的"用不了"反馈多源于底包与系统不匹配，本版起底包与 LineageOS 严格对齐。

---

## 📌 项目特性

- **LineageOS 官方底包**：基于 LineageOS `android_kernel_oneplus_sm8750` 的 `lineage-24.0` 分支最新提交构建，跟随上游维护节奏更新。
- **4K 页面对齐**：采用标准 4KB 内存分页大小（Page Size），保障针对非 16K 环境的深度兼容性。
- **Root 方案（FinaSU）**：内置编译 FinaSU v1.7.0（33224），自带 FolkZygisk、Sui 与 NoMount（VFS 路径重定向）引擎，无需额外模块。
- **隐蔽增强 (SUSFS)**：集成 SUSFS v2.4.0 内核层补丁，采用 SUSFS Inline 钩子后端，全部子功能开启，消除挂载特征、隐藏敏感路径并协助通过严苛的应用环境检测。
- **规范的内核标识**：版本串与构建信息与官方构建保持一致格式（`6.6.144-4k-g01ee97578159`，`nobody@android-build`）。

---

## ⚙️ 编译规格

| 配置项 | 规格说明 |
| :--- | :--- |
| **内核基线** | LineageOS 24.0 内核树（Linux 6.6.144） |
| **内核版本串** | `6.6.144-4k-g01ee97578159` |
| **目标架构** | `aarch64` / `arm64` |
| **Page Size** | 4 KB (`CONFIG_ARM64_4K_PAGES=y`) |
| **工具链** | Clang / LLVM 22 |
| **核心组件** | FinaSU v1.7.0（内置，SUSFS Inline）+ SUSFS v2.4.0 |

---

## 📦 刷入指南

> [!WARNING]
> 刷入第三方内核具有一定风险。在执行任何刷写操作前，请务必备份当前设备的 `boot` 分区镜像。
> 刷入前请核对：设置 → 关于手机 → 内核版本应以 `6.6.144-4k` 开头；若完整版本串与 `6.6.144-4k-g01ee97578159` 不一致，请先在 Issues 反馈再刷。

### 方式一：通过 Kernel Flasher / ReKernelFlasher（推荐）
1. 在 [Releases](../../releases) 页面下载最新构建的 `AK3-*.zip` 刷机包。
2. 打开具备 Root 权限的内核刷写工具，选取下载的 zip 刷机包进行刷入并重启设备。

### 方式二：通过 Recovery
1. 设备重启至支持的三方 Recovery 界面。
2. 选择下载的 `AK3-*.zip` 刷入并重启设备。

### 管理器（必读）
内核按 **FinaSU v1.7.0（33224）官方管理器 APK** 的签名校验，请从 Releases 一并下载配套管理器安装。**不要单独升级管理器版本**，否则内核将无法识别管理器。

---

## 📝 版本历史

- **finasu-v1.7.0（2026-11-23）**：底包由 crDroid 内核树换为 LineageOS 24 内核树；KernelSU 官方版换为 FinaSU v1.7.0 内置 + SUSFS Inline；SUSFS v2.3.0 升至 v2.4.0。
- **6.6（2026-10-15）**：crDroid 底包 + KernelSU v3.3.1 内置 + SuSFS v2.3.0（已停更，见 Releases）。
