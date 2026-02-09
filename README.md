# Lmkdopt Add-on
An extension for SkyScene Add-on that optimizes LMKD and Old LMK. It modernizes memory management to prioritize dynamic multitasking over aggressive killing, tailoring performance to both legacy and modern device capabilities.

If you want an optimization that improves the kernel's memory management behavior, check out the [SkyScene Add-on](https://github.com/WeirdMidas/SkySceneAddon), it specifically handles this aspect, such as swapping, reclaim, and others.

### Features

#### LMKD-Side (Modern Solution)
- Use PSI as the main killing method for LMKD. Abandon solutions like Minfree and focus on dynamic solutions that can respect the multitasking needs of modern devices with fewer false positives. With this, our LMKD has as few false positives as possible, reducing the need for LMKD intervention and allowing kswapd/ZRAM to handle memory management for longer (as the SkyScene Add-on proposes in its readme).
- By opting for the full use of the PSI mechanism, adapt the parameters of light and full stalls, thrashing, and other parameters based on the processor's capacity. This means that processors with small core clocks (which will be the measure used) below 1.7GHz, even if they are "high performance," can tolerate the same amount of crashes as a 1.9GHz "low memory" processor. This means that PSI adapts according to the processor's capacity to handle the number of processes requesting memory, always avoiding noticeable and irritating crashes, which is our goal: to tolerate multitasking before the user gets annoyed.
- Change the LMKD thrashing parameters based on two variables:
  - Whether the device has MGLRU.
  - Whether the device has 6GB or less RAM.
- Based on this, we can adapt our thrashing parameters based on how efficient the swapping management is, making LMKD less likely to interfere with system apps as the swapping management is able to handle the situation.
- It's preferable to kill the most resource-intensive processes as needed to shorten their lifespan and free up memory faster, as is the case with low-memory devices. On high-performance devices, it's better to kill processes gradually, since with ample memory, killing the most memory-intensive process becomes less necessary (and even detrimental).

#### Old LMK-Side (Old Solution)
- Make the minfree margin smoother and more predictable, avoid generating free memory abruptly, allowing older devices to use as much memory as possible before needing to clear everything, favoring the longevity of multitasking.
- Avoid using the adaptive Old LMK; it is unpredictable and can generate more false positives than it necessarily allows for better memory management.
  - Disable batch kill methods and other OEM functionalities, reducing the need for LMK to act in a stupid and naive way.
  
## Requirement

- Compatible with ARM64 and standard ARM
- Magisk, KSU or Apatch, the most up-to-date version possible if you can
- Android 8 or higher. Not compatible with versions below 8
- You need at least 3GB of RAM to use it. Modern Android requires this as a minimum amount of RAM. However, it is still compatible with devices that have less RAM
- It is recommended to use an additional busybox module for situations where the module cannot use the busybox from Magisk or the ROM
- Depending on the ROM or kernel you are using on your device, you may experience compatibility issues if they are heavily modified

## Installation

- Simply install the module and enjoy; optimizations will be applied automatically according to your device's capabilities. Currently, there are no configuration options via the control panel, but perhaps that will be available in the future.
- Simple LMK is currently not supported.
- Per-Process LMK is currently not supported.

## FAQ

### Sources

- Official information about [LMKD (Low Memory Killer Daemon)](https://source-android-com.translate.goog/docs/core/perf/lmkd?_x_tr_sl=en&_x_tr_tl=pt&_x_tr_hl=pt&_x_tr_pto=tc) provided by Google.
- Studies in psychology involving the human perception of "instantaneous" and the perception of "fluid continuity" in ordinary people and/or telephone users.

### Suggestions for Complementary Modules

- [A1Memory](https://github.com/OneB1ank/A1Memory): A memory management module that implements an OEM-style memory management framework in the system server, allowing you to control certain parts of memory management more efficiently than modern Android. Exclusive to Android 8-14.

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
