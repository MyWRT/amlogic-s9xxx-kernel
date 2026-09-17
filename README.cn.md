# MyWRT 6.18 内核构建

[English](README.md) | [中文说明](README.cn.md)

本仓库用于为 MyWRT 固件流程构建最新稳定版 `6.18.x` ARM64 内核。仓库只维护一个源码系列、一份配置和一个 Release 通道。

## 构建约定

| 项目 | 固定值 |
| --- | --- |
| 内核源码 | [`MyWRT/linux-6.18.y`](https://github.com/MyWRT/linux-6.18.y) 的 `main` 分支 |
| 内核系列 | `6.18.y`，自动解析为最新的 `6.18.x` 版本 |
| 内核配置 | [`kernel-config/release/stable/config-6.18`](kernel-config/release/stable/config-6.18) |
| 内核签名 | `-mywrt` |
| 软件包集合 | `all`，包含 boot、DTB 和 modules |
| Release 标签 | [`kernel_stable`](https://github.com/MyWRT/amlogic-s9xxx-kernel/releases/tag/kernel_stable) |

所有内核源码修改都应直接提交到 `MyWRT/linux-6.18.y`，构建工作流不再应用额外的补丁层。

## 构建内核

在仓库的 Actions 页面运行 **Compile mainline stable kernel**。工作流始终解析最新的 `6.18.x` 版本，只保留以下运行选项：

- 编译后是否删除已检出的源码；
- 编译工具链和 Armbian 构建镜像；
- 是否清理 ccache。

源码仓库、内核系列、配置路径、软件包集合和内核签名均固定在 [`.github/workflows/compile-mainline-stable-kernel.yml`](.github/workflows/compile-mainline-stable-kernel.yml) 中。

工作流使用 [`ophub/amlogic-s9xxx-armbian`](https://github.com/ophub/amlogic-s9xxx-armbian) 完成编译和打包。构建成功后会更新 `kernel_stable` Release，生成供 `amlogic-s9xxx-openwrt` 使用的完整内核产物。

## 自定义内核

- 内核代码、设备树和树内驱动修改应提交到 [`MyWRT/linux-6.18.y`](https://github.com/MyWRT/linux-6.18.y)。
- 内建功能和模块选项应修改 [`config-6.18`](kernel-config/release/stable/config-6.18)。
- 源码仓库应保留 `main` 分支；工作流使用该分支的提交哈希生成 ccache 键。

## 上游

本仓库派生自 [`ophub/kernel`](https://github.com/ophub/kernel)。内核编译和打包由 [`ophub/amlogic-s9xxx-armbian`](https://github.com/ophub/amlogic-s9xxx-armbian/tree/main/compile-kernel) 提供。

## 许可证

使用 [GPL-2.0](LICENSE) 许可证。
