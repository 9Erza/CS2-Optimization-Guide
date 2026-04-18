# 🎮 Counter-Strike 2 Optimization Guide & Performance Benchmarks

Comprehensive guide and data-driven analysis of CS2 performance across CPU scheduling, Windows configurations, and graphical settings.

---

## 📌 Table of Contents / Spis Treści
1. [🔬 Methodology & Test Environment](#-methodology--test-environment)
2. [⚙️ Section 1: CPU Scheduling (Affinity vs CPU Sets)](#-section-1-cpu-scheduling)
3. [🖥️ Section 2: Windows Settings & Optimizations](#-section-2-windows-settings)
4. [📺 Section 3: Full Screen vs Borderless Window](#-section-3-display-modes)
5. [🏎️ Section 4: Input Lag Tech (Anti-Lag 2.0 / Reflex)](#-section-4-latency-technologies)
6. [📊 Section 5: Graphics Settings Performance Impact](#-section-5-graphics-impact)
7. [🖼️ Section 6: Visual Comparison & Visibility Guide](#-section-6-visual-comparisons)
8. [🏆 Section 7: Summary & Recommended Settings](#-section-7-summary)

---

## 🔬 Methodology & Test Environment

### 📅 General Info
**Date of Testing:** 17.04.2026 (Main PC Benchmarks)

The benchmarks were conducted in a strictly controlled environment to ensure repeatability.
* **Isolation:** Only Steam (Offline Mode), CapFrameX (Capture Tool), and Process Core Optimizer were active in the background.
* **Procedure:** Each test case consists of 3 identical benchmark runs to calculate a reliable average.
* **Launch Options:** `-allow_third_party_software` (required for CapFrameX). No other parameters used.
* **Thread Scheduling:** All core affinity and CPU Sets modifications were handled exclusively via [Process Core Optimizer](https://github.com/9Erza/ProcessCoreOptimizer).
  * *Software Disclaimer:* This is a hobbyist project. Professional alternatives like **Process Lasso** can achieve similar results.

### 🖥️ Main System Specifications
* **CPU:** AMD Ryzen 7 7800X3D
* **Cooling:** DARKFLASH Twister DX-360 V2.6 ARGB
* **GPU:** ASRock Radeon RX 9070 XT Steel Legend 16 GB
* **RAM:** ADATA XPG Lancer Blade RGB 32GB (2x16GB) DDR5 6000MT/s CL30
* **Storage:** WD Blue SN580 2TB SSD
* **PSU:** MSI MAG A850GL 850W 80 Plus Gold
* **OS:** Windows 11 Pro (Build 26200) | HAGS: Enabled | Game Mode: Enabled

### 🎮 In-Game Graphical Baseline
The following settings were used for **all tests** (except Section 5, where settings are varied).
> **Note:** These settings were chosen because they are the most popular among the community/pro players, not necessarily because they are the most optimal. Finding the optimum is the goal of this guide.

| Setting | Value |
| :--- | :--- |
| **Resolution** | 1280x960 (4:3 Stretched) |
| **Display Mode** | Fullscreen |
| **Boost Player Contrast** | Enabled |
| **V-Sync** | Disabled |
| **AMD Anti-Lag 2.0** | Disabled |
| **Multisampling Anti-Aliasing** | 4X MSAA |
| **Global Shadow Quality** | Low |
| **Dynamic Shadows** | All |
| **Model / Texture Detail** | Low |
| **Texture Filtering Mode** | Bilinear |
| **Shader Detail** | Low |
| **Particle Detail** | Low |
| **Ambient Occlusion** | Disabled |
| **High Dynamic Range** | Quality |
| **FidelityFX Super Resolution** | Disabled (Native) |

---

<details>
<summary><h2>⚙️ Section 1: CPU Scheduling</h2></summary>

### Overview
Comparison between STOCK settings, Core Affinity (Hard binding), and Windows CPU Sets.

*(Place for benchmarks and analysis)*

</details>

---

<details>
<summary><h2>🖥️ Section 2: Windows Settings</h2></summary>

### Overview
Testing the impact of system-level features.
* Windows Game Mode (On vs Off)
* Core Isolation / VBS
* Hardware-Accelerated GPU Scheduling (HAGS)
* Power Plans (Balanced vs High Performance)

*(Place for benchmarks and analysis)*

</details>

---

<details>
<summary><h2>📺 Section 3: Display Modes</h2></summary>

### Overview
Full Screen vs. Borderless Windowed. Does the modern Windows 11 optimization for windowed games close the gap?

*(Place for benchmarks and analysis)*

</details>

---

<details>
<summary><h2>🏎️ Section 4: Latency Technologies</h2></summary>

### Overview
Impact of AMD Anti-Lag 2.0 on Frametimes and Input Delay. (Future update: Nvidia Reflex).

*(Place for benchmarks and analysis)*

</details>

---

<details>
<summary><h2>📊 Section 5: Graphics Settings Impact</h2></summary>

### Overview
Granular testing of every single graphics option. How many FPS do you actually gain by switching from High to Low?

*(Place for benchmarks and analysis)*

</details>

---

<details>
<summary><h2>🖼️ Section 6: Visual Comparison</h2></summary>

### Overview
Visual guide on how specific settings (Shadows, MSAA, Texture Filtering) affect visibility in competitive spots.

*(Place for comparison images and descriptions)*

</details>

---

<details>
<summary><h2>🏆 Section 7: Summary</h2></summary>

### Final Conclusions
* **Optimal Windows Config:** ...
* **Optimal CPU Config:** ...
* **Optimal Graphics Config:** ...

### Suggested Settings Table
*(Place for final suggested settings)*

</details>

---

*Copyright (c) 2026 9Erza. Personal testing and benchmarks.*
