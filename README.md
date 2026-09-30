# OrangeFox Recovery Project for Infinix Hot 10 (X682C)

![OrangeFox Logo](https://orangefox.tech/icon.png)

This repository contains the device tree and GitHub Actions workflow for building [OrangeFox Recovery](https://orangefox.download/) for the Infinix Hot 10 (X682C). 

> ***Disclaimer:*** *Your warranty is now void. I am not responsible for bricked devices, dead SD cards, thermonuclear war, or you getting fired because the alarm app failed. Please do some research if you have any concerns about features included in this recovery before flashing it! YOU are choosing to make these modifications.*

## 📱 Device Specifications

| Feature | Specification |
| :--- | :--- |
| **Device** | Infinix Hot 10 |
| **Codename** | X682C |
| **Chipset** | MediaTek Helio G70 (12 nm) |
| **CPU** | Octa-core (2x2.0 GHz Cortex-A75 & 6x1.7 GHz Cortex-A55) |
| **GPU** | Mali-G52 2EEMC2 |

## 🛠️ Automated Build (GitHub Actions)

This repository is configured to compile the recovery automatically using GitHub Actions, avoiding the need for a massive local build environment. 

1. Fork this repository.
2. Go to the **Actions** tab in your forked repo.
3. Select the **Build OrangeFox Recovery** workflow on the left.
4. Click **Run workflow**.
5. The automated compiler will allocate a 12GB swap file and build the recovery. Once completed (usually ~45-60 minutes), the `recovery.img` will be available as a downloadable artifact at the bottom of the workflow summary.

## 💻 Local Build Instructions

If you prefer to build locally on an Ubuntu machine, ensure you have at least 16GB of RAM/Swap and 100GB of free disk space.

### 1. Set up the build environment
Install the necessary dependencies:
```bash
sudo apt-get update
sudo apt-get install -y git-core gnupg flex bison build-essential zip curl zlib1g-dev libc6-dev-i386 x11proto-dev libx11-dev lib32z1-dev libgl1-mesa-dev libxml2-utils xsltproc unzip fontconfig python3 python-is-python3 openjdk-11-jdk rsync bc cpio libssl-dev lzop schedtool

2. Sync the OrangeFox 12.1 Source
mkdir ~/fox_12.1
cd ~/fox_12.1
git clone [https://gitlab.com/OrangeFox/sync.git](https://gitlab.com/OrangeFox/sync.git)
cd sync
./orangefox_sync.sh --branch 12.1 --path ~/fox_12.1

3. Clone the Device Tree
cd ~/fox_12.1
git clone [https://github.com/sysmar3x-glitch/Infinix-hot-10-custom-recovery.git](https://github.com/sysmar3x-glitch/Infinix-hot-10-custom-recovery.git) device/infinix/X682C

4. Compile the Recovery
cd ~/fox_12.1
source build/envsetup.sh
export ALLOW_MISSING_DEPENDENCIES=true
export FOX_BUILD_DEVICE=X682C
export LC_ALL="C"
lunch twrp_X682C-eng
mka recoveryimage
```
Your compiled recovery will be output to: out/target/product/X682C/recovery.img

## ⚡ Installation Guide

 * Unlock your device's bootloader.
 * Reboot your device into Fastboot/Bootloader mode.
 * Connect your device to your PC.
 * Flash the compiled recovery image via fastboot:
   fastboot flash recovery recovery.img
 * Reboot directly into recovery to prevent the stock ROM from overwriting OrangeFox:
   fastboot reboot recovery

## 🐛 Bug Reports & Contributions

If you encounter bugs, please open an issue in this repository. Pull requests for device tree improvements are always welcome!

## 🙏 Credits & Acknowledgments

 * TeamWin for TWRP Recovery
 * OrangeFox Recovery Project for the custom recovery UI and features
 * All contributors and testers

