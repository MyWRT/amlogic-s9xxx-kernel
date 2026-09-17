# MyWRT 6.18 Kernel Builds

[English](README.md) | [中文说明](README.cn.md)

This repository builds the latest stable `6.18.x` ARM64 kernel for the MyWRT firmware pipeline. It is intentionally limited to one source series, one configuration, and one release channel.

## Build Contract

| Item | Value |
| --- | --- |
| Kernel source | [`MyWRT/linux-6.18.y`](https://github.com/MyWRT/linux-6.18.y), branch `main` |
| Kernel series | `6.18.y`, automatically resolved to the latest `6.18.x` release |
| Kernel configuration | [`kernel-config/release/stable/config-6.18`](kernel-config/release/stable/config-6.18) |
| Kernel signature | `-mywrt` |
| Package set | `all` — boot, DTBs, and modules |
| Release tag | [`kernel_stable`](https://github.com/MyWRT/amlogic-s9xxx-kernel/releases/tag/kernel_stable) |

Kernel source changes belong in `MyWRT/linux-6.18.y`; the build workflow does not apply an additional patch layer.

## Build the Kernel

Run **Compile mainline stable kernel** from the repository's Actions page. The workflow always resolves the latest `6.18.x` release and exposes only these operational choices:

- remove the checked-out source after compilation;
- select the compiler toolchain and Armbian build image;
- optionally clear ccache.

The source owner, kernel series, configuration path, package set, and signature are fixed in [`.github/workflows/compile-mainline-stable-kernel.yml`](.github/workflows/compile-mainline-stable-kernel.yml).

The workflow uses [`ophub/amlogic-s9xxx-armbian`](https://github.com/ophub/amlogic-s9xxx-armbian) as the compiler and packager. Successful builds update the `kernel_stable` Release with the complete artifacts consumed by `amlogic-s9xxx-openwrt`.

## Customize the Kernel

- Change kernel code, device trees, or in-tree drivers in [`MyWRT/linux-6.18.y`](https://github.com/MyWRT/linux-6.18.y).
- Change built-in/module selections in [`config-6.18`](kernel-config/release/stable/config-6.18).
- Keep the source repository on branch `main`; the workflow uses its commit hash for the ccache key.

## Upstream

This repository is derived from [`ophub/kernel`](https://github.com/ophub/kernel). Kernel compilation and packaging are provided by [`ophub/amlogic-s9xxx-armbian`](https://github.com/ophub/amlogic-s9xxx-armbian/tree/main/compile-kernel).

## License

Licensed under [GPL-2.0](LICENSE).
