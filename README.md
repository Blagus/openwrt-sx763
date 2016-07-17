# OpenWRT for SX763
#### _Yet another OpenWRT fork for SX763_
_(Thank you, Lantiq maintainer!)_

### Introduction
This fork's aim is to be as updated and as close to the upstream as possible, while keeping the current board support level.  
It's based on latest stable version of Chaos Calmer (15.05) with minimal modifications.
I also didn't bother with keeping original Siemens' partitions and primary bootloader in order to save space.

The best performance is gained when internal ROM is bypassed by grounding BOOT_SEL0.

### Usage
Clone the repository and enter the directory.

First make packages available:
```
./scripts/feeds update -a
./scripts/feeds install -a
```

Then select SX763 board:
```
make menuconfig
* Target System -> Lantiq
* Subtarget -> XWAY
* Target Profile -> Gigaset sx76x
* Exit and save configuration
make defconfig
```

This prepares everything for a base OpenWRT build. Execute `make` to start compiling.  
Use `make menuconfig` to select packages which you need (think about space if you're installing to internal flash!).

### Installation
(TODO: Detailed instructions)  
Compatibility with current methods where only the secondary bootloader is replaced is not tested.  
You'll get the least overhead and most space by replacing primary bootloader.

To do that, select both ROM and RAM versions of U-Boot in menuconfig and send RAM version (with _.asc_ extension) via UART. Then load ROM version via YMODEM or TFTP and flash it to the beginning of NOR flash.

After reboot you should see U-Boot console. Use TFTP to load kernel and rootfs to RAM and save them to the flash.  
Reboot once again and you should see OpenWRT boot process.
