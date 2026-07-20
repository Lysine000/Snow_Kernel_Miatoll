# Snow Kernel for Xiaomi Miatoll ❄️

[![Build Snow Kernel](https://github.com/Lysine000/Snow_Kernel_Miatoll/actions/workflows/build.yml/badge.svg?branch=snow-android10)](https://github.com/Lysine000/Snow_Kernel_Miatoll/actions/workflows/build.yml)
[![Latest Release](https://img.shields.io/github/v/release/Lysine000/Snow_Kernel_Miatoll?color=blue)](https://github.com/Lysine000/Snow_Kernel_Miatoll/releases/latest)

A custom, high-performance Linux kernel built specifically for the **Xiaomi Miatoll** platform (Redmi Note 9 Pro Max / Poco M2 Pro / Redmi Note 9 Pro / Redmi Note 9S) under the codename **excalibur**, targeting **Android 10** (Snapdragon 720G).

## Features 🚀

- **KernelSU-Next Integration**: Integrated at the kernel level for secure, systemless root management.
- **Proton Clang Toolchain**: Compiled using Proton Clang and LLD with high-level optimizations.
- **LTO (Link Time Optimization)**: Enabled to optimize execution speed and binary footprint.
- **Governor**: Tuned `schedutil` governor for optimal CPU frequency scaling and battery efficiency.
- **Scheduler**: `CFQ` I/O scheduler.
- **SELinux**: Fully enforcing by default for robust system security.

## Flashing Instructions 🛠️

1. Download the latest flashable package (`Snow-Kernel-Miatoll.zip`) from the [Releases](https://github.com/Lysine000/Snow_Kernel_Miatoll/releases) page.
2. Boot into a custom recovery (e.g., OrangeFox Recovery Project or TWRP).
3. (Optional but Recommended) Back up your current boot partition.
4. Select `Snow-Kernel-Miatoll.zip` and swipe to install.
5. Reboot system.

## Compiling from Source 🏗️

The kernel is built automatically using GitHub Actions. If you wish to build it manually:

### Setup Toolchain
We recommend using the Proton Clang toolchain:
```bash
git clone --depth=1 https://github.com/kdrag0n/proton-clang.git clang
export PATH=$(pwd)/clang/bin:$PATH
```

### Build Command
```bash
export ARCH=arm64
export SUBARCH=arm64

# Configure defconfig
make O=out excalibur_defconfig

# Compile
make -j$(nproc --all) O=out \
  CC=clang \
  LD=ld.lld \
  NM=llvm-nm \
  OBJCOPY=llvm-objcopy \
  OBJDUMP=llvm-objdump \
  STRIP=llvm-strip \
  CLANG_TRIPLE=aarch64-linux-gnu- \
  CROSS_COMPILE=aarch64-linux-gnu- \
  CROSS_COMPILE_ARM32=arm-linux-gnueabi- \
  Image.gz-dtb dtbo.img
```
