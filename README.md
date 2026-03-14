# LMKD PSI Activation

## An efficient system, stable — even under pressure or when it needs to act

An extension of the SkyScene Add-on, where it achieves the effect of preventing background apps from dying by modifying memory management mechanisms (lmk, psi). And by improving background process management, it's possible to achieve a smoother and more energy-efficient system

If you want an optimization that improves the kernel's memory management behavior, check out the [SkyScene Add-on](https://github.com/WeirdMidas/SkySceneAddon), it specifically handles this aspect, such as swapping, reclaim, and others

### Features
- Pure background memory management optimization module (lmk, psi), without other side effects or placebos, and compatible with all major platforms, from Qualcomm to Mediatek, Unisoc, and others. It only requires using lmkd as the primary LMK module in the ROM
- Utilize lmkd's modern pressure mechanism, PSI (pressure stall information), allowing lmkd to kill background processes based on whether the system can handle keeping them running in memory. It doesn't depend on fixed minfree thresholds or anything like that
  - Follow Google's guidelines and standards, allowing older devices to benefit from a modern LMKD PSI in an older environment, depending on the available parameters
- Make the LMKD PSI as accurate as possible, based on various checks and variables. By doing this, we make our LMKD PSI more accurate because we already recognize the limitations and efficiency of our hardware
- Avoid stalls as much as possible, in addition to maintaining efficient and stable multitasking, reducing lmkd interventions and energy costs for each killing action by being as precise as possible, the PSI can be a professional killer based on how much each device tolerates stalls
- First and foremost: RESPECT THE HARDWARE! Don't push multitasking or process management beyond what the user's hardware can handle. If it can handle X number of processes, don't push the limits beyond that; the user NEEDS to know that not everything can be the way they want it
- SELinux can still be enabled

## Requirement

- Compatible with ARM64 and standard ARM
- Magisk, KSU or Apatch, the most up-to-date version possible if you can
- Android 10 or higher. Not compatible with versions below 10
- It needs compatibility with PSI; kernels without PSI will not be able to use the module even if they have lmkd
- You need at least 3GB of RAM to use it. Modern Android requires this as a minimum amount of RAM. However, it is still compatible with devices that have less RAM
- It is recommended to use an additional busybox module for situations where the module cannot use the busybox from Magisk or the ROM
- Depending on the ROM or kernel you are using on your device, you may experience compatibility issues if they are heavily modified

## Installation

- Install this module, restart your phone, wait 20 seconds before the final optimizations are applied, and voila, you can have fun with your device
- For LMKD, these algorithms have these compression rates to allow it to better see the amount of memory saved by ZRAM:
  - lz4, lzo, lzo-rlt, lz4kd, lz4k: 3x compression
  - Lz4hc: 4x compression
  - Zstd, Zstdn: 5x compression
  - Other algorithms: 2x compression
- Simple LMK is currently not supported
- Per-Process LMK is currently not supported
- Old LMK is currently not supported
- Other customizable LMKs are not compatible, only lmkd is compatible
- Devices with 2GB of RAM or less are GO devices, 3GB-4GB of RAM are low-memory, 6GB-8GB is mid-tier, and 12GB or more is high-performance

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
