# Crosstool-NG

Crosstool-ng is a tool designed to simplify and automate the process of building cross-compilation toolchains. These toolchains are essential for developing software that runs on a different architecture or platform than the one on which it is compiled. This is common in embedded systems development, where software is often compiled on a host machine but executed on a target device with different hardware architecture.

## 1. Download crosstool-ng

```shell
git clone https://github.com/crosstool-ng/crosstool-ng.git
git checkout 25f6dae8
cd crosstool-ng/
```

## 2. Setting up Environment

Dependencies required:

```shell
sudo apt-get install -y gcc g++ gperf bison flex texinfo help2man make libncurses5-dev \
python3-dev autoconf automake libtool libtool-bin gawk wget bzip2 xz-utils unzip \
patch libstdc++6 rsync
```

Run bootstrap to set up the environment:

```shell
./bootstrap
```

Check dependencies:

```shell
./configure --enable-local
```

Generate Makefile:

```shell
make
```

## 3. Configuration for Crosstool-ng

List all supported microcontrollers:

```shell
./ct-ng list-samples
```

We will choose `arm-cortexa9_neon-linux-gnueabihf` as an example:

```shell
./ct-ng arm-cortexa9_neon-linux-gnueabihf
```

Configure the toolchain:

```shell
./ct-ng menuconfig
```

Our needed configurations:

- [ ] C-library: **musl**
- [ ] C compiler: **support C++**
- [ ] Companion tools: **autoconf, automake, make**
- [ ] Debug facilities: **starce**, **gdb**

Show our configurations:

```shell
./ct-ng show-config
```

## 4. Build Our Toolchain

Build the toolchain:

```shell
./ct-ng build
```

Wait till it finishes and check your toolchain:

```shell
cd ~/x-tools
# If you have rootfs and want to copy sysroot to it as it will be needed by your compiled apps if it is dynamically built
cp ~/x-tools/arm-cortexa9_neon-linux-musleabihf/arm-cortexa9_neon-linux-musleabihf/sysroot/* <path>/rootfs/
```

## 5. Result

![1712589230803](image/README/1712589230803.png)
```