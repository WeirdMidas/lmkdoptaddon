# lmkd psi mod(ified)

**A module that optimizes how Android manages background apps (lmkd)**

## Overview

An extension of the SkyScene Add-on, where it achieves the effect of improve how the system manages background apps by modifying memory management mechanisms (lmkd, psi). And by improving background process management, it's possible to achieve a smoother and more energy-efficient system

If you want an optimization that improves the kernel's memory management behavior, check out the [SkyScene Add-on](https://github.com/WeirdMidas/SkySceneAddon), it specifically handles this aspect, such as swapping, reclaim, and others

It was intended to be a fork of [LMKD-PSI-Activator](https://github.com/lululoid/LMKD-PSI-Activator) that optimizes the LMKD PSI part more efficiently and better for Android multitasking. However, it became an original project due to the stark difference in optimization between the two modules

### Features

- Pure background memory management optimization module (lmkd, psi), without other side effects or placebos, and compatible with all major platforms, from Qualcomm to Mediatek, Unisoc, and others. It only requires using lmkd as the primary LMK module in the ROM
  - Utilize lmkd's modern pressure mechanism, PSI (pressure stall information), allowing lmkd to kill background processes based on whether the system can handle keeping them running in memory. It doesn't depend on fixed minfree thresholds or anything like that
  - Optimize both the lmkd before and after Android 15. This allows the lmkd to be adapted generationally, avoiding the addition of features not present on older devices, making maintenance easier for various devices and adapted strategies according to resource availability
- Respect the limits of each hardware component; don't push the device to its limits to avoid major I/O, memory, and CPU stalls. Maintain predictability and avoid bigger problems
- Follow Google's guidelines and standards, allowing older devices to benefit from a modern LMKD PSI in an older environment, depending on the available parameters
- Avoid stalls as much as possible, in addition to maintaining efficient and stable multitasking, reducing lmkd interventions and energy costs for each killing action by being as precise as possible, the PSI can be a professional killer based on how much each device tolerates stalls
- Pin the oom_reaper on the big/prime cores so that it has privileged access to high-performance cores, reducing the time the system experiences stalls due to lack of memory
- SELinux can still be enabled

## Requirement

- Android 10 or higher
- Have PSI enabled in the kernel
- Have lmkd as the only lmk mechanism on the device
- Having ZRAM enabled in the kernel
- 3GB or more of RAM (Optional)

## Installation

- Install this module, restart your phone, wait 20 seconds before the final optimizations are applied, and voila, you can have fun with your device
- For LMKD, these algorithms have these compression rates to allow it to better see the amount of memory saved by ZRAM:
  - lz4, lzo, lzo-rlt, lz4kd, lz4k: 3x compression ratio
  - Lz4hc: 4x compression ratio
  - Zstd, Zstdn: 5x compression ratio
  - Other algorithms: 2x compression ratio
- Other customizable LMKs are not compatible, only lmkd is compatible
- On Android devices running version 14 or lower, the "psi + minfree + new strategy" model is used, while on Android devices running version 15 or higher, the "pure psi" model is used
- Devices with 2GB of RAM or less are GO devices, 3GB-4GB of RAM are low-end, 6GB-8GB is mid-tier, and 12GB or more is high-performance

## FAQ

### Sources

- Official information about [LMKD (Low Memory Killer Daemon)](https://source-android-com.translate.goog/docs/core/perf/lmkd?_x_tr_sl=en&_x_tr_tl=pt&_x_tr_hl=pt&_x_tr_pto=tc) provided by Google

### Suggestions for Complementary Modules

- [NoSwipeToKill](https://github.com/dantmnf/NoSwipeToKill): lsposed module by [dantmnf](https://github.com/dantmnf) to reduce the aggressiveness of HyperOS/MIUI in killing processes, recommended for users of Xiaomi ROMs that use lsposed
- [A1Memory](https://github.com/OneB1ank/A1Memory): A memory management module that implements an OEM-style memory management framework in the system server, allowing you to control certain parts of memory management more efficiently than modern Android. Exclusive to Android 8-14

## Credit

@Doug Hoyte  
@topjohnwu  
@卖火炬的小菇凉--改进在红米K20pro上的zram兼容性  
@钉宫--模块配置文件放到更容易找到的位置  
@予你长情i--发现与蝰蛇杜比音效共存版magisk模块冲突导致panel读写错误  
@choksta --协助诊断v4版FSCC固定过多文件到内存  
@yishisanren --协助诊断v5版FSCC在三星平台固定过多文件到内存  
@方块白菜 --协助调试在联发科X10平台ZRAM相关功能  
@Simple9 --协助诊断在Magisk低于19.0的不兼容问题  
@〇MH1031 --协助诊断位于/system/bin二进制工具集的不兼容问题  
@yc9559 -- Obvious credits that I forgot to put, SkyScene only exists because of him, the GOAT of the 2018-2020 modules      
@Iamlooper -- For the magisk MMT Reborn template. Thanks to the template, I was able to replace the old qti-mem-opt template and keep all the features without extra additions! Also now the cpu usage of the module has reduced by 2%, little but useful      
