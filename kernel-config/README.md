# Kernel Configuration

This repository maintains one kernel configuration:

```text
kernel-config/release/stable/config-6.18
```

The stable workflow always builds `MyWRT/linux-6.18.y` with this configuration:

```yaml
with:
  kernel_source: MyWRT
  kernel_version: 6.18.y
  kernel_config: kernel-config/release/stable
```

Edit `config-6.18` to change built-in features or modules. Source code, device-tree, and driver changes belong in [`MyWRT/linux-6.18.y`](https://github.com/MyWRT/linux-6.18.y), not in a build-time patch directory.

# 内核配置

本仓库只维护一份内核配置：

```text
kernel-config/release/stable/config-6.18
```

稳定版工作流始终使用该配置构建 `MyWRT/linux-6.18.y`：

```yaml
with:
  kernel_source: MyWRT
  kernel_version: 6.18.y
  kernel_config: kernel-config/release/stable
```

修改 `config-6.18` 可以调整内建功能或模块。内核源码、设备树和驱动修改应直接提交到 [`MyWRT/linux-6.18.y`](https://github.com/MyWRT/linux-6.18.y)，而不是通过构建时补丁目录维护。
