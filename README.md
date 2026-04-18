# 🎮 Counter-Strike 2 Optimization Guide & Performance Benchmarks

Comprehensive guide and data-driven analysis of CS2 performance across CPU scheduling, Windows configurations, and graphical settings.

---

## 📌 Table of Contents
1. [🔬 Methodology & Test Environment](#-methodology--test-environment)
2. [⚙️ Section 1: CPU Scheduling (Affinity vs CPU Sets)](#-section-1-cpu-scheduling)
3. [🖥️ Section 2: Windows Settings & Optimizations](#-section-2-windows-settings)
4. [🚀 Section 3: CS2 Launch Options](#-section-3-launch-options)
5. [📺 Section 4: Display Modes (Full Screen vs Borderless)](#-section-4-display-modes)
6. [📏 Section 5: Resolutions Comparison](#-section-5-resolutions-comparison)
7. [🛡️ Section 6: FACEIT Anti-Cheat Impact & Optimization](#-section-6-faceit-anti-cheat-impact)
8. [🏎️ Section 7: Latency Technologies (Anti-Lag 2.0 / Reflex)](#-section-7-latency-technologies)
9. [📊 Section 8: Graphics Settings Performance Impact](#-section-8-graphics-impact)
10. [🖼️ Section 9: Visual Comparison & Visibility Guide](#-section-9-visual-comparisons)
11. [🏆 Section 10: Summary & Recommended Settings](#-section-10-summary)
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
This section analyzes the impact of AMD Anti-Lag 2.0 (the equivalent of Nvidia Reflex) on overall framerates and frametime stability. These technologies work by pacing the CPU to prevent it from running too far ahead of the GPU, which minimizes the render queue and reduces input latency. However, this synchronization process can sometimes introduce a slight performance overhead, especially in extremely high-FPS, CPU-bound scenarios.

---

### ⚙️ Test Case 1: CS2 - Anti-Lag 2.0 Off

#### 📈 FPS Results (Frames Per Second)

| Metric | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE |
|---|---|---|---|---|
| **Average FPS** | 906.0 | 908.2 | 906.4 | **906.9** |
| **P1 (1%)** | 300.3 | 302.5 | 300.1 | **301.0** |
| **P0.1 (0.1%)** | 267.7 | 268.4 | 270.2 | **268.8** |
| **1% Low Average** | 282.8 | 285.4 | 283.8 | **284.0** |
| **0.1% Low Average** | 240.0 | 243.2 | 244.7 | **242.6** |

#### ⏱️ Frametime Results (ms)

| Metric | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE |
|---|---|---|---|---|
| **Average ms** | 1.1 | 1.1 | 1.1 | **1.1** |
| **1% High Avg ms** | 3.5 | 3.3 | 3.5 | **3.5** |
| **0.1% High Avg ms** | 4.2 | 4.1 | 4.1 | **4.1** |

#### 📝 Notes & Analysis
With latency reduction disabled, the system runs unrestricted, pushing past 900 Average FPS. This serves as our baseline to see how much overhead the Anti-Lag 2.0 algorithm introduces. 

---

### ⚙️ Test Case 2: CS2 - Anti-Lag 2.0 On

#### 📈 FPS Results (Frames Per Second)

| Metric | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE |
|---|---|---|---|---|
| **Average FPS** | 875.7 | 869.3 | 870.8 | **871.9** |
| **P1 (1%)** | 301.4 | 293.8 | 298.5 | **298.1** |
| **P0.1 (0.1%)** | 267.5 | 263.7 | 269.2 | **266.0** |
| **1% Low Average** | 285.0 | 278.3 | 283.8 | **282.1** |
| **0.1% Low Average** | 246.1 | 240.2 | 248.7 | **244.9** |

#### ⏱️ Frametime Results (ms)

| Metric | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE |
|---|---|---|---|---|
| **Average ms** | 1.1 | 1.2 | 1.1 | **1.1** |
| **1% High Avg ms** | 3.5 | 3.6 | 3.3 | **3.5** |
| **0.1% High Avg ms** | 4.1 | 4.2 | 4.0 | **4.1** |

#### 📝 Notes & Analysis
Enabling Anti-Lag 2.0 results in a measurable drop in maximum framerate, lowering the Average FPS from ~907 to ~872 (about a 3.8% decrease). This is expected behavior; the engine is pacing the frames rather than rendering them as fast as theoretically possible. Interestingly, the absolute lowest dips (0.1% Low Average) actually slightly *improved* from 242.6 to 244.9 FPS, indicating excellent frame pacing stability.

---

### 🏆 Latency Technologies Conclusion

**Should you use Anti-Lag 2.0 (or Nvidia Reflex)? Yes.**

While enabling Anti-Lag 2.0 costs you roughly 35 Average FPS, it is important to remember context: this is a drop from 900 FPS down to 870 FPS. At this tier of performance, the visual difference of those lost frames is non-existent. 

What you gain in return is a mathematically shorter render queue and lower end-to-end system latency (click-to-photon). Furthermore, the data shows that the 1% and 0.1% frametime lows remain entirely unaffected (and even slightly more stable). For competitive play, prioritizing input responsiveness over a purely cosmeticly high Average FPS number is always the correct choice.

</details>

---
<details>
<summary><h2>📊 Section 5: Graphics Settings Impact</h2></summary>

### Overview
This section isolates each graphical setting to determine its exact performance cost. The baseline for every test is the absolute lowest setting possible (all Low/Disabled/None), which yields an average of **979,5 FPS**. We then raise individual settings one by one to see how heavily they impact the framerate and the 1% / 0.1% lows. 

*(Note: We are purely analyzing performance impact and technical behavior here. Visual comparisons are covered in Section 6).*

---

### Multisampling Anti-Aliasing Mode
| Setting | Avg FPS | P1 FPS | 1% Low Avg | P0.1 FPS | 0.1% Low Avg |
|---|---|---|---|---|---|
| None | 979,5 | 301,5 | 284,7 | 267,1 | 249,3 |
| CMAA2 | 968,3 | 303,3 | 288,0 | 273,3 | 253,8 |
| 2x msaa | 941,0 | 300,5 | 284,8 | 270,3 | 248,3 |
| 4x msaa | 924,7 | 297,6 | 282,7 | 267,0 | 248,3 |
| 8x msaa | 865,6 | 300,2 | 284,2 | 268,1 | 245,5 |

**Technical Impact Analysis:** MSAA (Multisample Anti-Aliasing) physically renders the geometry edges at a higher resolution to eliminate jagged lines. Because of this, it is one of the heaviest settings in the game. Scaling up to 8x MSAA introduces a massive performance penalty, dropping the average framerate by roughly 114 FPS compared to the baseline. 
CMAA2 (Conservative Morphological Anti-Aliasing), on the other hand, is a post-processing filter. It smooths the final image after it has been rendered, meaning it has almost zero negative impact, costing only ~11 FPS while actually maintaining slightly higher and more stable lows than "None".

---

### Boost Player Contrast
| Setting | Avg FPS | P1 FPS | 1% Low Avg | P0.1 FPS | 0.1% Low Avg |
|---|---|---|---|---|---|
| Disabled | 979,5 | 301,5 | 284,7 | 267,1 | 249,3 |
| Enabled | 978,6 | 308,0 | 292,0 | 275,9 | 257,5 |

**Technical Impact Analysis:** This setting applies a post-processing edge-detect filter that generates a subtle halo around character models to make them stand out against dark or complex backgrounds. Because it is a lightweight 2D screen-space effect, it has virtually no negative impact on the average FPS (a difference of less than 1 FPS). Interestingly, enabling it shows a measurable positive impact on the 1% and 0.1% lows, stabilizing the frame pacing.

---

### Global Shadow Quality
| Setting | Avg FPS | P1 FPS | 1% Low Avg | P0.1 FPS | 0.1% Low Avg |
|---|---|---|---|---|---|
| Low | 979,5 | 301,5 | 284,7 | 267,1 | 249,3 |
| Medium | 961,3 | 302,2 | 287,1 | 270,8 | 250,9 |
| High | 932,3 | 297,0 | 281,7 | 266,2 | 244,9 |
| Very High | 879,3 | 301,1 | 284,3 | 266,8 | 248,4 |

**Technical Impact Analysis:** This setting dictates the resolution of shadow maps and the distance at which shadow cascades are rendered. This is a major performance sink. Pushing shadows to "Very High" forces the engine to render extremely crisp shadows from far away, introducing a severe penalty that strips exactly 100 FPS from the average compared to "Low".

---

### Dynamic Shadows
| Setting | Avg FPS | P1 FPS | 1% Low Avg | P0.1 FPS | 0.1% Low Avg |
|---|---|---|---|---|---|
| Sun Only | 979,5 | 301,5 | 284,7 | 267,1 | 249,3 |
| All | 973,3 | 301,6 | 286,3 | 270,9 | 252,2 |

**Technical Impact Analysis:** This controls which light sources allow entities to cast shadows. "Sun Only" restricts shadows to the main global lighting of the map. "All" allows local lights (such as lamps, fires, or muzzle flashes) to also generate dynamic shadows. The performance difference is minimal, costing merely ~6 FPS on the average while keeping the 1% and 0.1% lows completely intact.

---

### Model / Texture Detail
| Setting | Avg FPS | P1 FPS | 1% Low Avg | P0.1 FPS | 0.1% Low Avg |
|---|---|---|---|---|---|
| Low | 979,5 | 301,5 | 284,7 | 267,1 | 249,3 |
| medium | 949,8 | 307,9 | 291,6 | 276,0 | 252,7 |
| high | 926,1 | 304,4 | 287,5 | 269,7 | 249,0 |

**Technical Impact Analysis:** This setting determines the mipmap level (resolution) of textures loaded into the GPU's VRAM, as well as the geometric complexity of certain world objects. Increasing texture complexity carries a moderate performance cost. Moving to "High" increases VRAM utilization and drops the average framerate by roughly 53 FPS compared to the baseline.

---

### Texture Filtering Mode
| Setting | Avg FPS | P1 FPS | 1% Low Avg | P0.1 FPS | 0.1% Low Avg |
|---|---|---|---|---|---|
| Bilinear | 979,5 | 301,5 | 284,7 | 267,1 | 249,3 |
| Trilinear | 953,5 | 303,3 | 266,1 | 272,9 | 146,8 |
| Anisotropic 2x | 975,5 | 309,5 | 294,3 | 279,0 | 257,5 |
| Anisotropic 4x | 964,4 | 298,2 | 283,9 | 269,7 | 250,6 |
| Anisotropic 8x | 971,7 | 300,4 | 284,5 | 270,8 | 247,7 |
| Anisotropic 16x | 970,7 | 301,3 | 285,4 | 270,0 | 246,4 |

**Technical Impact Analysis:** Filtering determines how textures look when viewed at sharp, oblique angles. Bilinear is the most basic. Anisotropic Filtering (AF) mathematically calculates the texture perspective, keeping it sharp at a distance, and is essentially "free" on modern GPU architectures, costing less than 10 FPS for the maximum 16x setting. 
**Crucial Note:** "Trilinear" filtering introduces a severe engine anomaly in CS2. While the average FPS seems fine, it heavily degrades the 0.1% Low Average (cratering down to 146,8 FPS), causing massive micro-stuttering. Avoid Trilinear at all costs.

---

### Shader Detail
| Setting | Avg FPS | P1 FPS | 1% Low Avg | P0.1 FPS | 0.1% Low Avg |
|---|---|---|---|---|---|
| Low | 979,5 | 301,5 | 284,7 | 267,1 | 249,3 |
| High | 964,9 | 300,5 | 285,3 | 270,2 | 249,9 |

**Technical Impact Analysis:** Shader Detail dictates the complexity of surface lighting, material reflections (such as shiny weapon skins), and minor environmental effects. Despite the visual upgrade to weapon models, "High" has a surprisingly low impact on performance, dropping the average by only ~15 FPS without noticeably affecting the 1% or 0.1% lows.

---

### Particle Detail
| Setting | Avg FPS | P1 FPS | 1% Low Avg | P0.1 FPS | 0.1% Low Avg |
|---|---|---|---|---|---|
| Low | 979,5 | 301,5 | 284,7 | 267,1 | 249,3 |
| Medium | 941,4 | 303,7 | 288,7 | 274,1 | 254,6 |
| High | 940,3 | 300,3 | 278,2 | 253,5 | 229,0 |
| Very High | 885,8 | 292,8 | 271,8 | 246,6 | 227,9 |

**Technical Impact Analysis:** This controls the resolution, density, and rendering volume of particle effects like smoke grenades, molotov flames, and HE explosions. It places a heavy load on the CPU and GPU bandwidth. Pushing it to "Very High" results in a massive 93 FPS drop in the average. Furthermore, both "High" and "Very High" introduce a noticeable negative impact on the 0.1% Lows, significantly reducing frame stability during intense executes with multiple grenades.

---

### Ambient Occlusion
| Setting | Avg FPS | P1 FPS | 1% Low Avg | P0.1 FPS | 0.1% Low Avg |
|---|---|---|---|---|---|
| Disabled | 979,5 | 301,5 | 284,7 | 267,1 | 249,3 |
| Medium | 970,6 | 303,9 | 288,7 | 273,5 | 253,0 |
| High | 971,6 | 303,7 | 288,3 | 273,4 | 251,7 |

**Technical Impact Analysis:** Ambient Occlusion (AO) adds realistic soft contact shadows in corners and areas where objects meet, giving the map more depth. Because CS2 uses an optimized screen-space occlusion technique, it has a very minor performance penalty. Both Medium and High settings cost less than 10 FPS on average and do not disturb frametime stability.

---

### High Dynamic Range
| Setting | Avg FPS | P1 FPS | 1% Low Avg | P0.1 FPS | 0.1% Low Avg |
|---|---|---|---|---|---|
| Performance | 979,5 | 301,5 | 284,7 | 267,1 | 249,3 |
| High | 968,2 | 303,6 | 288,3 | 274,6 | 252,1 |

**Technical Impact Analysis:** HDR settings in CS2 do not refer to HDR monitor output, but rather the internal mathematical precision of color blending and bloom effects. Changing HDR from "Performance" (lower 16-bit float precision) to "High" (32-bit float precision) carries an almost negligible cost on modern GPUs, lowering the average by just ~11 FPS while removing color banding in the skybox.

---

### 📊 Performance Impact Summary

Based on the isolated testing above, we can clearly categorize the settings by their performance cost.

**🔴 Heaviest Performance Hits (Largest FPS Drops):**
* **8x MSAA:** Over -110 Average FPS penalty. Heavy GPU geometry load.
* **Global Shadow Quality (Very High):** Over -100 Average FPS penalty.
* **Particle Detail (Very High):** Over -90 Average FPS penalty, with significant degradation to 0.1% Lows during heavy action.
* **Model / Texture Detail (High):** Moderate penalty of ~53 Average FPS.

**🟢 Lowest Performance Impact ("Free" or Cheap Settings):**
* **Boost Player Contrast:** Zero FPS penalty; actually slightly stabilizes frametimes.
* **Texture Filtering (Anisotropic 16x):** Less than -10 FPS penalty. *(Note: Avoid Trilinear due to severe micro-stutter and massive 0.1% low drops).*
* **Dynamic Shadows (All):** Less than -10 FPS penalty.
* **Ambient Occlusion (High):** Less than -10 FPS penalty.
* **High Dynamic Range (High):** ~11 FPS penalty.
* **Anti-Aliasing (CMAA2):** ~11 FPS penalty.
* **Shader Detail (High):** ~15 FPS penalty.

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
