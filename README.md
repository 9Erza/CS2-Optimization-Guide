# 🎮 Counter-Strike 2 Optimization Guide & Performance Benchmarks

This repository documents comprehensive performance testing and optimization strategies for Counter-Strike 2. The focus is on CPU scheduling, core affinity, and system-level tweaks using the custom **Process Core Optimizer** to achieve the lowest possible latency and highest framerate stability.

## 🔬 Methodology & Test Environment

**Date of Testing:** 17.04.2026 (Main PC Benchmarks)

The benchmarks were conducted in a strictly controlled environment to ensure repeatability.
* **Isolation:** Only Steam (Offline Mode), CapFrameX (Capture Tool), and Process Core Optimizer were active in the background.
* **Procedure:** Each test case consists of 3 identical benchmark runs to calculate a reliable average.
* **In-Game Settings:** Strictly identical across all runs. No settings or in-game affinity mechanics were modified between test cases.
* **CS2 Launch Options:** `-allow_third_party_software` (strictly required for CapFrameX benchmarking). Absolutely NO other launch parameters were used.
* **Thread Scheduling:** All core affinity and CPU Sets modifications were handled exclusively via a custom-built utility: [Process Core Optimizer](https://github.com/9Erza/ProcessCoreOptimizer). 
  * *Software Disclaimer:* This optimizer is a personal/hobbyist project tailored for these specific tweaks. Users seeking established, commercial-grade alternatives can achieve similar scenarios using software like **Process Lasso**.
* **OS Configuration:** HAGS (Hardware-Accelerated GPU Scheduling) Enabled, Windows Game Mode Enabled.
* **Future Roadmap:** Tests on a secondary platform (Ryzen 7 5700X + RTX 2080 + 32GB 3600MHz CL16) and various combinations of in-game graphical settings are planned for future updates.

### 🖥️ Main System Specifications
* **CPU:** AMD Ryzen 7 7800X3D
* **Cooling:** DARKFLASH Twister DX-360 V2.6 ARGB
* **Motherboard:** GIGABYTE B650 Eagle AX
* **RAM:** ADATA XPG Lancer Blade RGB 32GB (2x16GB) DDR5 6000MT/s CL30
* **GPU:** ASRock Radeon RX 9070 XT Steel Legend 16 GB
* **Storage:** WD Blue SN580 2TB SSD
* **PSU:** MSI MAG A850GL 850W 80 Plus Gold
* **OS:** Windows 11 Pro (Build 26200)

### ⚙️ Current CS2 In-Game Settings
<details>
<summary>🖼️ View In-Game Settings / Zobacz ustawienia w grze (Rozwiń)</summary>
<br>
<p align="center">
  <img src="https://github.com/9Erza/CS2-Optimization-Guide/blob/main/images/video-settings/screen-settings.jpg?raw=true" width="32%" alt="Screen Settings">
  <img src="https://github.com/9Erza/CS2-Optimization-Guide/blob/main/images/video-settings/graphics-settings-1.jpg?raw=true" width="32%" alt="Graphics Settings 1">
  <img src="https://github.com/9Erza/CS2-Optimization-Guide/blob/main/images/video-settings/graphics-settings-2.jpg?raw=true" width="32%" alt="Graphics Settings 2">
</p>

</details>

<details>
<summary>🇵🇱 Metodologia i Środowisko Testowe (Rozwiń)</summary>

**Data testów:** 17.04.2026 (Benchmarki głównego PC)

Pomiary zostały przeprowadzone w ściśle kontrolowanych warunkach, aby zapewnić pełną powtarzalność.
* **Izolacja:** W tle działały tylko Steam (Tryb Offline), CapFrameX oraz autorski program Process Core Optimizer.
* **Procedura:** Każdy scenariusz opiera się na 3 identycznych przejazdach testowych w celu wyciągnięcia wiarygodnej średniej.
* **Ustawienia w grze:** Identyczne we wszystkich przejazdach. W żadnym z testów nie zmieniano ustawień graficznych ani nie używano wbudowanych w grę mechanizmów koligacji.
* **Opcje startowe CS2:** `-allow_third_party_software` (niezbędne, by CapFrameX mógł zliczać klatki). Nie użyto absolutnie żadnych innych parametrów startowych.
* **Zarządzanie wątkami:** Wszelkie modyfikacje koligacji (Affinity) oraz mechanizmu CPU Sets były wymuszane z zewnątrz, wyłącznie z poziomu autorskiej aplikacji: [Process Core Optimizer](https://github.com/9Erza/ProcessCoreOptimizer).
  * *Nota o oprogramowaniu:* Jest to autorski projekt stworzony na własny użytek. Użytkownicy poszukujący komercyjnych, w pełni profesjonalnych rozwiązań mogą osiągnąć podobne rezultaty korzystając z programów takich jak **Process Lasso**.
* **Konfiguracja OS:** HAGS (Hardware-Accelerated GPU Scheduling) włączone, Tryb Gry (Game Mode) włączony.
* **Plany na przyszłość:** W późniejszym czasie w repozytorium pojawią się testy na starszej platformie (Ryzen 7 5700X + RTX 2080 + 32GB DDR4 3600MHz CL16) oraz sprawdzenie różnych kombinacji ustawień graficznych wewnątrz gry CS2.

</details>

---

### ⚙️ Test Case 1: CS2 - STOCK

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 827.8 | 825.8 | 828.6 | **827.4** |
| **P1 (1%)** | 270.2 | 274.9 | 272.2 | **272.4** |
| **P0.1 (0.1%)** | 235.5 | 241.0 | 239.5 | **238.6** |
| **1% Low Average** | 252.2 | 257.9 | 255.8 | **255.3** |
| **0.1% Low Average** | 217.9 | 223.8 | 222.8 | **223.5** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.208 | 1.211 | 1.207 | **1.209** |
| **1% High Avg ms** | 3.965 | 3.877 | 3.910 | **3.917** |
| **0.1% High Avg ms** | 4.590 | 4.469 | 4.489 | **4.516** |

#### 📝 Notes / Wnioski
**[ENG]** Baseline standard configuration (STOCK) performance without core affinity modifications. Strong overall average, though the 0.1% lowest frame dips hover around ~223 FPS. This serves as the primary reference point for comparing the effectiveness of core isolation and Process Core Optimizer settings.

<details>
<summary>🇵🇱 Wersja polska (Rozwiń)</summary>

**[PL]** Konfiguracja bazowa (STOCK) bez modyfikacji koligacji rdzeni. Bardzo wysoka średnia ogólna, jednak najgłębsze spadki (0.1% Low) oscylują w okolicach ~223 FPS. Jest to główny punkt odniesienia, względem którego będziemy weryfikować skuteczność izolacji rdzeni i ustawień Process Core Optimizera w kolejnych testach.
</details>

---

### ⚙️ Test Case 2: CS2 - CPU Affinity - Core 0 OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 862.9 | 860.7 | 863.3 | **862.3** |
| **P1 (1%)** | 293.0 | 294.2 | 294.6 | **293.9** |
| **P0.1 (0.1%)** | 263.3 | 251.4 | 264.4 | **259.7** |
| **1% Low Average** | 276.6 | 272.4 | 279.8 | **276.2** |
| **0.1% Low Average** | 236.5 | 213.5 | 247.5 | **232.5** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.159 | 1.162 | 1.158 | **1.160** |
| **1% High Avg ms** | 3.615 | 3.671 | 3.574 | **3.620** |
| **0.1% High Avg ms** | 4.227 | 4.693 | 4.040 | **4.320** |

#### 📝 Notes / Wnioski
**[ENG]** Disabling Core 0 using the Process Core Optimizer yields a noticeable performance uplift over the STOCK configuration. The average FPS increased by ~35 frames (from 827.4 to 862.3), and the 1% Low Average improved from 255.3 to 276.2 FPS. This confirms that preventing the game from using the primary OS-loaded core reduces interruptions and stabilizes frametimes significantly on the 7800X3D.

<details>
<summary>🇵🇱 Wersja polska (Rozwiń)</summary>

**[PL]** Wyłączenie rdzenia 0 (Core 0) za pomocą Process Core Optimizer przynosi zauważalny wzrost wydajności względem konfiguracji STOCK. Średni FPS wzrósł o ok. 35 klatek (z 827.4 do 862.3), a wynik 1% Low Average poprawił się z 255.3 do 276.2 FPS. Potwierdza to, że izolacja gry od pierwszego rdzenia (często obciążonego przez system operacyjny) redukuje mikroprzycięcia i znacząco stabilizuje czasy renderowania klatek (frametime) na procesorze 7800X3D.
</details>

---

### ⚙️ Test Case 3: CS2 - CPU Affinity - SMT/HT OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 841.1 | 833.2 | 839.1 | **837.8** |
| **P1 (1%)** | 276.5 | 274.9 | 279.7 | **277.1** |
| **P0.1 (0.1%)** | 241.7 | 242.4 | 245.5 | **243.2** |
| **1% Low Average** | 258.1 | 257.0 | 261.2 | **258.7** |
| **0.1% Low Average** | 220.1 | 220.7 | 225.8 | **222.2** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.189 | 1.200 | 1.192 | **1.194** |
| **1% High Avg ms** | 3.874 | 3.892 | 3.829 | **3.865** |
| **0.1% High Avg ms** | 4.549 | 4.536 | 4.429 | **4.505** |

#### 📝 Notes / Wnioski
**[ENG]** In this scenario, a strict CPU Affinity mask was applied to disable Hyper-Threading (SMT) for the game process, but without isolating it from Core 0. The results show a slight improvement over the pure STOCK configuration (around +10 FPS on the average). However, it falls significantly behind the `Core 0 OFF` configuration, demonstrating that simply removing virtual threads without protecting the process from the primary OS core overhead is sub-optimal for the 7800X3D.

<details>
<summary>🇵🇱 Wersja polska (Rozwiń)</summary>

**[PL]** W tym scenariuszu zastosowano sztywną maskę koligacji (CPU Affinity), aby wyłączyć hiperwątkowość (SMT) dla procesu gry, ale bez odcinania go od rdzenia zerowego. Wyniki pokazują minimalną poprawę względem czystej konfiguracji STOCK (ok. +10 FPS średnio). Odstają one jednak zauważalnie od konfiguracji wyłączającej rdzeń zerowy (`Core 0 OFF`), co dowodzi, że samo wyłączenie wirtualnych wątków, bez ochrony gry przed obciążeniem ze strony systemu operacyjnego, daje suboptymalne rezultaty na procesorze 7800X3D.
</details>

---

### ⚙️ Test Case 4: CS2 - CPU Affinity - SMT/HT OFF + Core 0 OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 900.6 | 897.2 | 900.3 | **899.4** |
| **P1 (1%)** | 301.3 | 302.4 | 307.4 | **303.7** |
| **P0.1 (0.1%)** | 265.2 | 269.2 | 274.0 | **269.4** |
| **1% Low Average** | 283.0 | 285.9 | 290.7 | **286.5** |
| **0.1% Low Average** | 239.0 | 249.9 | 247.7 | **245.5** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.110 | 1.115 | 1.111 | **1.112** |
| **1% High Avg ms** | 3.534 | 3.497 | 3.441 | **3.491** |
| **0.1% High Avg ms** | 4.188 | 4.002 | 4.041 | **4.077** |

#### 📝 Notes / Wnioski
**[ENG]** Using the custom Process Core Optimizer application, a hard affinity mask was used to disable Hyper-Threading (SMT) and completely isolate the game from the primary OS core (`Core 0`). The results are spectacular. The Average FPS skyrocketed to nearly 900 (a massive ~72 FPS jump from the STOCK baseline), while maintaining exceptionally tight 1% Lows (~286 FPS). This proves that eliminating virtual threads while simultaneously protecting the game from background OS interruptions yields the highest performance scaling on the 7800X3D.

<details>
<summary>🇵🇱 Wersja polska (Rozwiń)</summary>

**[PL]** Przy użyciu autorskiego programu Process Core Optimizer zastosowano sztywną maskę koligacji, aby wyłączyć hiperwątkowość (SMT) oraz całkowicie odciąć grę od głównego rdzenia systemowego (`Core 0`). Wyniki są spektakularne. Średni FPS poszybował w okolice 900 klatek (skok o ok. 72 FPS względem czystego STOCK), przy zachowaniu niezwykle stabilnych ułamków 1% Low (~286 FPS). Dowodzi to, że jednoczesna eliminacja wirtualnych wątków oraz ochrona gry przed przerwaniami systemowymi w tle daje najlepsze możliwe skalowanie wydajności na procesorze 7800X3D.
</details>

---

### ⚙️ Test Case 5: CS2 - CPU Sets - Core 0 OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 863.6 | 859.0 | 866.3 | **863.0** |
| **P1 (1%)** | 292.3 | 290.3 | 294.1 | **292.3** |
| **P0.1 (0.1%)** | 260.0 | 256.0 | 266.5 | **260.8** |
| **1% Low Average** | 275.6 | 273.5 | 279.9 | **276.3** |
| **0.1% Low Average** | 235.6 | 233.4 | 245.7 | **238.2** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.158 | 1.164 | 1.154 | **1.159** |
| **1% High Avg ms** | 3.628 | 3.657 | 3.573 | **3.619** |
| **0.1% High Avg ms** | 4.245 | 4.285 | 4.070 | **4.200** |

#### 📝 Notes / Wnioski
**[ENG]** This test utilizes the Windows "CPU Sets" mechanism instead of strict hard affinity to park Core 0. The results are remarkably similar to the hard affinity test (`Test Case 2`). The average FPS sits solidly around ~863, providing a tangible boost over the STOCK configuration while matching the stability of hard affinity. It demonstrates that the Windows scheduler respects the soft limits imposed by CPU Sets perfectly in this scenario.

<details>
<summary>🇵🇱 Wersja polska (Rozwiń)</summary>

**[PL]** W tym teście wykorzystano mechanizm Windows "CPU Sets" zamiast "twardej" koligacji (Hard Affinity), aby odciążyć rdzeń 0 (Core 0). Wyniki są uderzająco podobne do analogicznego testu z twardą koligacją (`Test Case 2`). Średnia liczba FPS wynosi stabilne ~863 klatki, zapewniając wyraźny wzrost wydajności w stosunku do konfiguracji bazowej (STOCK), jednocześnie dorównując stabilnością klasycznej koligacji. Pokazuje to, że w tym scenariuszu systemowy scheduler idealnie respektuje "miękkie" limity narzucane przez mechanizm CPU Sets.
</details>

---

### ⚙️ Test Case 6: CS2 - CPU Sets - SMT/HT OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 845.1 | 847.4 | 847.0 | **846.5** |
| **P1 (1%)** | 277.3 | 278.5 | 282.4 | **279.4** |
| **P0.1 (0.1%)** | 241.5 | 245.2 | 247.8 | **244.8** |
| **1% Low Average** | 258.9 | 261.3 | 264.5 | **261.5** |
| **0.1% Low Average** | 225.8 | 230.0 | 230.3 | **228.7** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.183 | 1.180 | 1.181 | **1.181** |
| **1% High Avg ms** | 3.862 | 3.828 | 3.781 | **3.824** |
| **0.1% High Avg ms** | 4.429 | 4.348 | 4.343 | **4.373** |

#### 📝 Notes / Wnioski
**[ENG]** In this scenario, the application uses the Windows CPU Sets mechanism to instruct the scheduler to avoid Hyper-Threading (SMT) logical cores for the game, without isolating it from the primary Core 0. Performance improves over the baseline STOCK configuration (~846 FPS vs ~827 FPS), proving that removing virtual threads is beneficial. However, it falls short of the ~900 FPS achieved when Core 0 is simultaneously disabled.

<details>
<summary>🇵🇱 Wersja polska (Rozwiń)</summary>

**[PL]** W tym scenariuszu aplikacja wykorzystuje mechanizm Windows CPU Sets, instruując system, aby omijał logiczne wątki SMT dla procesu gry, ale bez izolowania go od głównego rdzenia (Core 0). Wydajność wzrasta względem bazowej konfiguracji STOCK (~846 FPS vs ~827 FPS), co dowodzi korzyści płynących z usunięcia wirtualnych wątków. Wynik ten jest jednak niższy od potężnych ~900 FPS osiągniętych, gdy rdzeń zerowy zostaje równocześnie wyłączony.
</details>

---

### ⚙️ Test Case 7: CS2 - CPU Sets - SMT/HT OFF + Core 0 OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 894.3 | 896.8 | 900.5 | **897.2** |
| **P1 (1%)** | 302.6 | 298.9 | 302.6 | **301.3** |
| **P0.1 (0.1%)** | 269.4 | 263.3 | 270.7 | **267.8** |
| **1% Low Average** | 283.7 | 281.0 | 286.7 | **283.8** |
| **0.1% Low Average** | 236.8 | 237.4 | 248.8 | **241.0** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.118 | 1.115 | 1.111 | **1.115** |
| **1% High Avg ms** | 3.525 | 3.559 | 3.488 | **3.524** |
| **0.1% High Avg ms** | 4.223 | 4.212 | 4.023 | **4.153** |

#### 📝 Notes / Wnioski
**[ENG]** This scenario uses the Windows CPU Sets API to disable Hyper-Threading (SMT) and prevent the game from using Core 0 simultaneously. The performance is nearly identical to the Hard Affinity variant (`Test Case 4`), achieving a massive ~897 Average FPS (a ~70 FPS uplift over STOCK) and rock-solid 1% Lows (~284 FPS). This confirms that Windows CPU Sets is highly effective on the 7800X3D, offering maximum performance scaling without the strict thread-locking behavior of traditional hard affinity.

<details>
<summary>🇵🇱 Wersja polska (Rozwiń)</summary>

**[PL]** W tym wariancie wykorzystano API Windows CPU Sets, aby jednocześnie wyłączyć dla gry hiperwątkowość (SMT) oraz uniemożliwić jej dostęp do rdzenia zerowego (Core 0). Wydajność jest niemal identyczna jak w przypadku twardej koligacji (`Test Case 4`) – uzyskujemy potężną średnią ~897 FPS (skok o ok. 70 FPS względem STOCK) oraz niezwykle stabilne 1% Low (~284 FPS). Potwierdza to, że mechanizm CPU Sets działa na 7800X3D znakomicie, oferując maksymalne skalowanie wydajności bez restrykcyjnego blokowania wątków charakterystycznego dla klasycznej koligacji.
</details>

---

## 💡 Final Summary & Conclusions

**The Recommended Configuration:** Based on the data gathered, **CS2 - CPU Sets - SMT/HT OFF + Core 0 OFF** is definitively the most optimal setting.

**Why?**
1. **Identical Peak Performance:** The results are virtually identical to strict "Hard Affinity" binding (only marginally lower in margin-of-error territory), securing a massive ~70 FPS uplift over STOCK settings.
2. **Anti-Cheat Compatibility:** Unlike Hard Affinity, which strictly locks threads and is known to cause conflicts or be blocked by aggressive Anti-Cheats (e.g., **FaceitAC**), Windows CPU Sets acts as a "soft" suggestion to the OS scheduler. It effectively routes threads away from parked cores without violating Anti-Cheat integrity checks.
3. **Frametime Stability:** Completely isolating the game from OS background interrupts running on Core 0 ensures the smoothest frametimes and completely eliminates micro-stuttering on the 7800X3D architecture.

### ⚠️ Disclaimer
All data presented in this repository comes from private benchmarking on a specific, optimized hardware configuration. Every PC behaves differently due to varying components, background tasks, and OS conditions.
* **Test it yourself:** You are highly encouraged to use these settings as a strong guideline, but always verify them with your own testing.
* **Liability:** Do not copy settings blindly. All modifications and system tweaks are done entirely at your own risk.

<details>
<summary>🇵🇱 Podsumowanie i Wnioski (Rozwiń)</summary>

**Rekomendowana konfiguracja:** Analiza zgromadzonych danych bezsprzecznie wskazuje, że ustawienie **CS2 - CPU Sets - SMT/HT OFF + Core 0 OFF** jest najbardziej optymalnym wyborem.

**Dlaczego?**
1. **Maksymalna wydajność:** Wyniki są w zasadzie identyczne jak przy stosowaniu sztywnego "Hard Affinity" (różnice mieszczą się w granicy błędu pomiarowego), co daje potężny skok wydajności o około 70 FPS względem czystego STOCKa.
2. **Zgodność z Antycheatami:** W przeciwieństwie do Hard Affinity, które "na twardo" blokuje wątki i bywa odrzucane przez rygorystyczne antycheaty (takie jak **FaceitAC**), mechanizm CPU Sets to miękka sugestia dla systemu Windows. Skutecznie przesuwa wątki z dala od wyłączonego rdzenia, nie naruszając przy tym integralności sprawdzanej przez zabezpieczenia gier.
3. **Stabilność frametime'ów:** Izolacja procesu gry od systemowych przerwań odbywających się w tle na rdzeniu zerowym drastycznie poprawia płynność i eliminuje mikroprzycięcia (stuttering) charakterystyczne dla architektury 7800X3D.

### ⚠️ Zastrzeżenie
Wszystkie dane przedstawione w tym repozytorium to wyniki prywatnych testów wykonanych na konkretnej, zoptymalizowanej jednostce. Każdy komputer może reagować inaczej ze względu na odmienne podzespoły, działające w tle programy czy stan systemu.
* **Przeprowadź własne testy:** Gorąco zachęcam do traktowania powyższych wyników jako bardzo mocnej sugestii, jednak ostateczną wydajność zawsze weryfikuj na własnym sprzęcie.
* **Odpowiedzialność:** Nie ustawiaj parametrów w ciemno. Wszelkie modyfikacje wykonujesz wyłącznie na własną odpowiedzialność.
</details>
