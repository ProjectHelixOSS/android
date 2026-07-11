ProjectHelix
===========

Getting started
---------------

To get started with ProjectHelix, you'll need to get familiar with [Source Control Tools](https://source.android.com/setup/develop).

## Initialization and Syncing:
1. Initialize your local repository:
    ```bash
    repo init --no-repo-verify --git-lfs -u https://github.com/ProjectHelixOSS/android.git -b lineage-23.2 -g default,-mips,-darwin,-notdefault
    ```
   Or If you wish to save some system space and don't care about repo history depths:
    ```bash
    repo init --depth=1 --no-repo-verify --git-lfs -u https://github.com/ProjectHelixOSS/android.git -b lineage-23.2 -g default,-mips,-darwin,-notdefault
    ```
2. Sync up with the remote repository:
    ```bash
    repo sync -c --no-clone-bundle --no-tags --optimized-fetch --prune --force-sync -j$(nproc --all)
    ```

## ProjectHelix OS Device Properties

ProjectHelix supports custom properties for "About phone" and system optimization.  
Set these in your device tree:

```make
# Camera information (multiple sensors supported)
HELIX_FRONT_CAMERA := 16
HELIX_BACK_CAMERA := 50+50+8

# Maintainer name 
HELIX_MAINTAINER := GokuSudoku

# Processor name
HELIX_PROCESSOR := MediaTek Dimensity 810

# Maintainer related info
HELIX_MAINTAINER_AVATAR := device/xiaomi/everpal/helix/avatar.png (change location wherever /avatar.png is stored)
HELIX_MAINTAINER_GITHUB := himanshuksr0007
HELIX_MAINTAINER_TELEGRAM := GOkuSudoku
```
---


## Device Tree Setup

Optional flags:

- **Enable blur effects | DEFAULT: False**  
  ```make
  TARGET_ENABLE_BLUR := true
  ```

- **Enable debugging -- Implementation: [AxionAOSP](https://github.com/AxionAOSP)**  
  ```make
  add in product overrides or set using console: adb shell setprop persist.sys.helix_debug_enabled 1 
  persist.sys.helix_debug_enabled=1
  ```
  (Disabled by default. Meant for debugging purposes - bootloop, aidl/hardware dependency by sepolicy failure, etc)  
---

## Helix Prebuilts

Prebuilts apps that comes with the rom, use below flags 

- **Enable [BCR](https://github.com/chenxiaolong/BCR)**
  ```make
  TARGET_INCLUDE_BRC := true
  ```
  (Disabled by default.)
- **Enable [IntallerX](https://github.com/wxxsfxyzm/InstallerX-Revived/)**
  ```make
  TARGET_INCLUDE_INSTALLERX := true
  ```
  (Enabled by default.)

- **Note:** None of the above apps are developed by ProjectHelix, they belongs to there respective owners mentioed in them.  
---

## ScrollOptimizer

ScrollOptimizer is an AxionOS feature that optimizes frame pacing and buffer handling during UI scroll and fling operations.
It improves touch responsiveness and reduces rendering latency, ported from Linaro’s proprietary implementation.

### Properties

```make
# Enable or disable ScrollOptimizer globally
persist.sys.perf.scroll_opt = true

# Heavy app handling mode
# 0 - Disable heavy app classification
# 1 - Enable dynamic detection (based on frame duration and buffer load)
# 2 - Treat all apps as heavy for performance
persist.sys.perf.scroll_opt.heavy_app = 2
```
- **Source:** [AxionAOSP](https://github.com/AxionAOSP/android) | [ScrollOptimizer.java](https://github.com/AxionAOSP/android_frameworks_base/blob/lineage-23.2/core/java/com/android/internal/util/ScrollOptimizer.java)
---

