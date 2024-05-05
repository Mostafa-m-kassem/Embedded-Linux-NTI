# Linux Kernel

he Linux Kernel serves as the central component of the Linux operating system. Operating as a Unix-like, monolithic kernel, it functions as a singular, extensive process within the system, overseeing critical operations such as process management, memory management, device management, and file system handling.


# 1. Download & Configuration for kernel !

**Vexpress Cortexa9 Qemur**

```
git clone --depth=1 git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux.git
cd linux

export CROSS_COMPILE=<Path To Compiler>/arm-cortexa9_neon-linux-musleabihf-
export ARCH=arm
make qemu_arm_vexpress_defconfig
```

**Raspberry pi**

```
git clone --depth=1 https://github.com/raspberrypi/linux
cd linux
#export the compiler
export CROSS_COMPILE=arm-linux-gnueabihf-
#export the architecture used
export ARCH=arm<32/64>
#configure the kernel to rpi depends on the SoC number
make bcmXXXX_defconfig
```

**In the configuration, configure the following  requirement :**

```
Configuration Requirements
```

For all the next board this configuration must be checked

* [ ] Enable **devtmpfs**
* [ ] Change kernel compression to XZ
* [ ] Append your name to the kernel local version (e.g., -v1.0)

Proceed with building::

```
make  -j12 zImage modules dtbs
```

# 2. Loading Kernel & Device Tree in U-Boot

Copy the output kernel and device tree to your SD card's boot directory or TFTP server for loading:

```
cp linux/arch/arm/boot/zImage /srv/tftp/
cp linux/arch/arm/boot/dts/*-ca9.dtb /srv/tftp//
```

**discussed that in U-boot** 

# 3. Starting the Kernel 

```
bootz $kernel_addr_r - $fdt_addr_r
```

# 4. Root File System Not Found

If the root file system is not found, the kernel will panic and fail to start. Refer to the BusyBox section for setting up the root file system.