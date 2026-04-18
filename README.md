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
<summary><h2>⚙️ Section 1: CPU Scheduling (Affinity vs CPU Sets)</h2></summary>

### Overview
This section explores the performance impact of CPU thread management on the Ryzen 7 7800X3D. We compare the baseline (STOCK) performance against two different methods of thread restriction:
1. **Hard CPU Affinity:** Forcing the process to use or ignore specific logical processors.
2. **Windows CPU Sets:** A "softer" OS-level suggestion that guides threads away from specific cores without strictly locking them, which is generally safer for anti-cheat software.

We test disabling **Core 0** (to isolate the game from heavy Windows background tasks) and disabling **SMT/Hyper-Threading** (to prevent the game from using slower virtual threads).

---

### ⚙️ Test Case 1: CS2 - STOCK

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 827.8 | 825.8 | 828.6 | **827.4** |
| **P1 (1%)** | 270.2 | 274.9 | 272.2 | **272.5** |
| **P0.1 (0.1%)** | 235.5 | 241.0 | 239.5 | **237.9** |
| **1% Low Average** | 252.2 | 257.9 | 255.8 | **255.2** |
| **0.1% Low Average** | 217.9 | 223.8 | 222.8 | **221.3** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.2 | 1.2 | 1.2 | **1.2** |
| **1% High Avg ms** | 3.9 | 3.8 | 3.9 | **3.9** |
| **0.1% High Avg ms** | 4.5 | 4.4 | 4.4 | **4.5** |

#### 📝 Notes & Analysis
Baseline standard configuration without any core modifications. The 7800X3D delivers a very strong overall average (~827 FPS), but the 0.1% lows hover around ~221 FPS. This is our primary reference point to see how much we can stabilize the frametimes through process isolation.

---

### ⚙️ Test Case 2: CS2 - CPU Affinity - Core 0 OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 862.9 | 860.7 | 863.3 | **862.3** |
| **P1 (1%)** | 293.0 | 294.2 | 294.6 | **294.0** |
| **P0.1 (0.1%)** | 263.3 | 251.4 | 264.4 | **260.3** |
| **1% Low Average** | 276.6 | 272.4 | 279.8 | **276.2** |
| **0.1% Low Average** | 236.5 | 213.5 | 247.5 | **230.7** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.2 | 1.2 | 1.2 | **1.2** |
| **1% High Avg ms** | 3.6 | 3.7 | 3.6 | **3.6** |
| **0.1% High Avg ms** | 4.2 | 4.7 | 4.0 | **4.3** |

#### 📝 Notes & Analysis
By applying a strict hard affinity mask to disable Core 0, we see a noticeable performance uplift. The average FPS increases by ~35 frames, and the 1% Lows jump from ~255 to ~276 FPS. This confirms that preventing the game from sharing a core with heavy OS background interrupts significantly stabilizes frametimes.

---

### ⚙️ Test Case 3: CS2 - CPU Affinity - SMT/HT OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 841.1 | 833.2 | 839.1 | **837.8** |
| **P1 (1%)** | 276.5 | 274.9 | 279.7 | **277.0** |
| **P0.1 (0.1%)** | 241.7 | 242.4 | 245.5 | **243.0** |
| **1% Low Average** | 258.1 | 257.0 | 261.2 | **258.7** |
| **0.1% Low Average** | 220.1 | 220.7 | 225.8 | **222.1** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.2 | 1.2 | 1.2 | **1.2** |
| **1% High Avg ms** | 3.9 | 3.9 | 3.8 | **3.9** |
| **0.1% High Avg ms** | 4.5 | 4.5 | 4.4 | **4.5** |

#### 📝 Notes & Analysis
Here, Hyper-Threading (SMT) is disabled via hard affinity, meaning the game only uses physical cores, but Core 0 remains active for the game. We see a slight improvement over STOCK (+10 FPS average), but it falls significantly behind the "Core 0 OFF" config. Removing virtual threads helps, but failing to isolate the game from the OS main core remains a bottleneck.

---

### ⚙️ Test Case 4: CS2 - CPU Affinity - SMT/HT OFF + Core 0 OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 900.6 | 897.2 | 900.3 | **899.4** |
| **P1 (1%)** | 301.3 | 302.4 | 307.4 | **303.7** |
| **P0.1 (0.1%)** | 265.2 | 269.2 | 274.0 | **268.6** |
| **1% Low Average** | 283.0 | 285.9 | 290.7 | **286.3** |
| **0.1% Low Average** | 239.0 | 249.9 | 247.7 | **245.1** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.110 | 1.115 | 1.111 | **1.1** |
| **1% High Avg ms** | 3.534 | 3.497 | 3.441 | **3.5** |
| **0.1% High Avg ms** | 4.2 | 4.0 | 4.0 | **4.1** |

#### 📝 Notes & Analysis
The "brute force" maximum performance approach. By disabling SMT and completely isolating the game from Core 0 using hard affinity, the average FPS skyrockets to nearly 900 (a massive ~72 FPS jump from STOCK). The 1% Lows become exceptionally tight (~286 FPS). This proves that eliminating virtual threads while protecting the game from background OS interruptions yields the absolute highest performance scaling.

---

### ⚙️ Test Case 5: CS2 - CPU Sets - Core 0 OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 863.6 | 859.0 | 866.3 | **863.0** |
| **P1 (1%)** | 292.3 | 290.3 | 294.1 | **292.3** |
| **P0.1 (0.1%)** | 260.0 | 256.0 | 266.5 | **260.2** |
| **1% Low Average** | 275.6 | 273.5 | 279.9 | **276.3** |
| **0.1% Low Average** | 235.6 | 233.4 | 245.7 | **237.8** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.158 | 1.164 | 1.154 | **1.2** |
| **1% High Avg ms** | 3.628 | 3.657 | 3.573 | **3.6** |
| **0.1% High Avg ms** | 4.245 | 4.285 | 4.070 | **4.2** |

#### 📝 Notes & Analysis
Shifting to the Windows CPU Sets API (soft scheduling), we parked Core 0. The results are remarkably similar to Test Case 2 (Hard Affinity). It demonstrates that the Windows scheduler respects the soft limits imposed by CPU Sets perfectly, delivering the same ~863 Average FPS and solid stability.

---

### ⚙️ Test Case 6: CS2 - CPU Sets - SMT/HT OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 845.1 | 847.4 | 847.0 | **846.5** |
| **P1 (1%)** | 277.3 | 278.5 | 282.4 | **279.4** |
| **P0.1 (0.1%)** | 241.5 | 245.2 | 247.8 | **244.5** |
| **1% Low Average** | 258.9 | 261.3 | 264.5 | **261.4** |
| **0.1% Low Average** | 225.8 | 230.0 | 230.3 | **228.4** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.2 | 1.2 | 1.2 | **1.2** |
| **1% High Avg ms** | 3.9 | 3.8 | 3.8 | **3.8** |
| **0.1% High Avg ms** | 4.4 | 4.3 | 4.3 | **4.4** |

#### 📝 Notes & Analysis
Using CPU Sets to disable SMT without isolating Core 0 yields results nearly identical to Test Case 3. Removing virtual threads is beneficial, but the system is still hindered by OS background noise on the primary core.

---

### ⚙️ Test Case 7: CS2 - CPU Sets - SMT/HT OFF + Core 0 OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 894.3 | 896.8 | 900.5 | **897.2** |
| **P1 (1%)** | 302.6 | 298.9 | 302.6 | **301.3** |
| **P0.1 (0.1%)** | 269.4 | 263.3 | 270.7 | **267.9** |
| **1% Low Average** | 283.7 | 281.0 | 286.7 | **283.7** |
| **0.1% Low Average** | 236.8 | 237.4 | 248.8 | **240.6** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.118 | 1.115 | 1.111 | **1.1** |
| **1% High Avg ms** | 3.525 | 3.559 | 3.488 | **3.5** |
| **0.1% High Avg ms** | 4.2 | 4.2 | 4.0 | **4.2** |

#### 📝 Notes & Analysis
Using the Windows CPU Sets API to simultaneously disable SMT and prevent the game from using Core 0. The performance scales incredibly well, achieving ~897 Average FPS and highly stable frametimes. 

---

### 🏆 CPU Scheduling Conclusion: The Optimal Setup

Based on the benchmark data, **Test Case 7 (CPU Sets - SMT/HT OFF + Core 0 OFF)** is definitively the optimal configuration.

**Why CPU Sets wins over Hard Affinity:**
While Test Case 4 (Hard Affinity) peaked slightly higher at 899 FPS compared to CPU Sets' 897 FPS, the difference is completely negligible and falls within the margin of error. However, the architectural difference between the two methods is massive for competitive gaming:
* **Anti-Cheat Compatibility:** Hard Affinity strictly locks threads. Aggressive kernel-level anti-cheats (such as **Faceit AC**) often block or conflict with hard affinity masks, leading to game crashes or input stutter. 
* **The "Soft" Advantage:** Windows CPU Sets acts as a "soft" suggestion to the OS scheduler. It effectively routes threads away from parked cores and SMT logic without violating AC integrity checks, providing the massive ~70 FPS uplift and buttery smooth 1% lows while remaining completely safe to use on third-party matchmaking platforms.

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
<summary><h2>📺 Section 3: Display Modes - Fullscreen vs Borderless</h2></summary>

### Overview
Testing the performance difference between traditional Exclusive Fullscreen and Borderless Windowed modes. Historically, Fullscreen was mandatory for minimal input lag and maximum FPS. However, modern Windows 11 features ("Optimizations for windowed games") aim to close this gap, allowing for seamless alt-tabbing without performance penalties.

---

### ⚙️ Test Case 1: CS2 - Borderless Windowed

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE |
|---|---|---|---|---|
| **Average FPS** | 900.7 | 901.5 | 895.0 | **899.1** |
| **P1 (1%)** | 300.5 | 303.6 | 297.5 | **300.5** |
| **P0.1 (0.1%)** | 269.4 | 272.1 | 266.3 | **269.2** |
| **1% Low Average** | 284.6 | 287.5 | 282.6 | **284.8** |
| **0.1% Low Average** | 246.7 | 248.4 | 247.6 | **247.4** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE |
|---|---|---|---|---|
| **Average ms** | 1.1 | 1.1 | 1.1 | **1.1** |
| **1% High Avg ms** | 3.5 | 3.5 | 3.5 | **3.5** |
| **0.1% High Avg ms** | 4.1 | 4.0 | 4.0 | **4.0** |

#### 📝 Notes & Analysis
Running the game in Borderless mode delivers exceptional performance, maintaining nearly 900 Average FPS. Surprisingly, the 0.1% Low Average is incredibly stable at ~247 FPS, showing that modern OS window management does not introduce significant micro-stutter on this hardware.

---

### ⚙️ Test Case 2: CS2 - Fullscreen

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE |
|---|---|---|---|---|
| **Average FPS** | 906.0 | 908.2 | 906.4 | **906.9** |
| **P1 (1%)** | 300.3 | 302.5 | 300.1 | **301.1** |
| **P0.1 (0.1%)** | 267.7 | 268.4 | 270.2 | **268.4** |
| **1% Low Average** | 282.8 | 285.4 | 283.8 | **284.0** |
| **0.1% Low Average** | 240.0 | 243.2 | 244.7 | **242.7** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE |
|---|---|---|---|---|
| **Average ms** | 1.1 | 1.1 | 1.1 | **1.1** |
| **1% High Avg ms** | 3.5 | 3.3 | 3.5 | **3.4** |
| **0.1% High Avg ms** | 4.2 | 4.1 | 4.1 | **4.1** |

#### 📝 Notes & Analysis
Traditional Exclusive Fullscreen provides a minor boost to peak Average FPS (~907 FPS vs ~899 FPS in Borderless). However, the extreme lows (0.1% Low Average) are marginally lower than in Borderless mode (~243 FPS vs ~247 FPS). The frametime variance is virtually identical.

---

### 🏆 Display Modes Conclusion

**Fullscreen vs Borderless is practically a tie on Windows 11.** While **Fullscreen** yields a strictly mathematical advantage in maximum Average FPS (+8 FPS), **Borderless** actually provides marginally better and tighter 0.1% Lows (+5 FPS). 

For players using modern hardware and Windows 11 (with "Optimizations for windowed games" enabled), **Borderless Windowed** is highly recommended if you frequently Alt-Tab. You are losing less than 1% of total performance while gaining massive quality-of-life benefits. Purists seeking the absolute highest theoretical peak can stick to Fullscreen, but the difference is imperceptible in actual gameplay.

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
