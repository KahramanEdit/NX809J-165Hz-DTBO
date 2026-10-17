# 📱 RedMagic 11 Pro (NX809J) – 165Hz Display Overclock (DTBO)

![Android](https://img.shields.io/badge/Android-14%2B-green)
![Snapdragon](https://img.shields.io/badge/SoC-Snapdragon%208%20Elite-red)
![Display](https://img.shields.io/badge/Display-165Hz%20Stable-blue)

This repository provides the modified DTBO (Device Tree Blob Overlay) image to unlock the display refresh rate of the **RedMagic 11 Pro (NX809J)** from the stock **144Hz** to a stable **165Hz**.

While the Snapdragon 8 Elite and the RM692H5 panel physically support up to 180Hz (and the kernel can be patched to recognize it), ZTE's proprietary UI framework restricts the display to a maximum of 165Hz. Therefore, this 165Hz mod is the absolute sweet spot for stability, power consumption, and thermal management.

> ⚠️ **DISCLAIMER:** 
> *Modifying system partitions voids your warranty. A bad DTBO flash will cause a bootloop. You MUST have TWRP installed and a full backup of your stock `dtbo_b` before proceeding. Proceed at your own risk.*

---

## ⚙️ Technical Details

The display refresh rate is tied to the `qcom,mdss-mdp-transfer-time-us` property in the device tree.
*   **Stock 144Hz:** `6235 µs` (0x185b) -> Byte Clock: ~132.5 MHz
*   **Modded 165Hz:** `5454 µs` (0x154e) -> Byte Clock: ~150.0 MHz

By reducing the MDP transfer time and injecting a new `timing@4` node, the Qualcomm driver automatically recalculates the DSI clock. Because the panel's DCS `0x2f` register is set to `0x00` (Auto/Max), the DDIC automatically steps up to 165Hz. No extra DCS commands are required.

*   **File provided:** `dtbo_165safe.img`
*   **MD5 Hash:** `2caea2e0f0f03d0d528f3f8da5fb9785`

---

## 🛠️ Prerequisites

1.  **Unlocked Bootloader** (Required for TWRP).
2.  **TWRP Custom Recovery** installed.
3.  **Root Access** (Magisk or KernelSU) - *If flashing via Termux.*
4.  **Or PC with Fastboot** - *If flashing via PC.*

---

## 🚀 Installation Guide

### Method 1: PC / Fastboot (Recommended)
1. Download `dtbo_165safe.img` from the **Releases** tab.
2. Reboot your device to bootloader:
   ```bash
   adb reboot bootloader
