### ⚙️ Test Case: CS2 STOCK (Baseline)

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 827.8 | 825.8 | 828.6 | **827.4** |
| **P1 (1%)** | 270.2 | 274.9 | 272.2 | **272.4** |
| **P0.2 (0.2%)** | 243.7 | 249.5 | 247.7 | **247.0** |
| **1% Low Average** | 253.4 | 259.0 | 256.8 | **256.4** |
| **0.1% Low Average** | 220.4 | 225.8 | 225.0 | **223.7** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.208 | 1.211 | 1.207 | **1.209** |
| **1% High Avg ms** | 3.965 | 3.877 | 3.910 | **3.917** |
| **0.1% High Avg ms** | 4.590 | 4.469 | 4.489 | **4.516** |

#### 📝 Notes / Wnioski
**[ENG]** Baseline standard configuration (STOCK) performance without core affinity modifications. Strong overall average, though the 0.1% lowest frame dips hover around ~223 FPS. This serves as the primary reference point for comparing the effectiveness of core isolation and Process Core Optimizer settings.
**[PL]** Konfiguracja bazowa (STOCK) bez modyfikacji koligacji rdzeni. Bardzo wysoka średnia ogólna, jednak najgłębsze spadki (0.1% Low) oscylują w okolicach ~223 FPS. Jest to główny punkt odniesienia, względem którego będziemy weryfikować skuteczność izolacji rdzeni i ustawień Process Core Optimizera w kolejnych testach.

### ⚙️ Test Case: Core Affinity - Core 0 Disabled (Core -0)

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 862.9 | 860.7 | 863.3 | **862.3** |
| **P1 (1%)** | 293.0 | 294.2 | 294.6 | **293.9** |
| **P0.2 (0.2%)** | 271.8 | 266.6 | 273.1 | **270.5** |
| **1% Low Average** | 278.1 | 275.5 | 280.7 | **278.1** |
| **0.1% Low Average** | 241.5 | 222.1 | 249.6 | **237.7** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.159 | 1.162 | 1.158 | **1.160** |
| **1% High Avg ms** | 3.615 | 3.671 | 3.574 | **3.620** |
| **0.1% High Avg ms** | 4.227 | 4.693 | 4.040 | **4.320** |

#### 📝 Notes / Wnioski
**[ENG]** Disabling Core 0 using the Process Core Optimizer yields a noticeable performance uplift over the STOCK configuration. The average FPS increased by ~35 frames (from 827.4 to 862.3), and the 1% Low Average improved from 256.4 to 278.1 FPS. This confirms that preventing the game from using the primary OS-loaded core reduces interruptions and stabilizes frametimes significantly on the 7800X3D.
**[PL]** Wyłączenie rdzenia 0 (Core 0) za pomocą Process Core Optimizer przynosi zauważalny wzrost wydajności względem konfiguracji STOCK. Średni FPS wzrósł o ok. 35 klatek (z 827.4 do 862.3), a wynik 1% Low Average poprawił się z 256.4 do 278.1 FPS. Potwierdza to, że izolacja gry od pierwszego rdzenia (często obciążonego przez system operacyjny) redukuje mikroprzycięcia i znacząco stabilizuje czasy renderowania klatek (frametime) na procesorze 7800X3D.

### ⚙️ Test Case: Core Affinity - OFF (No Affinity Binding)

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 841.1 | 833.2 | 839.1 | **837.8** |
| **P1 (1%)** | 276.5 | 274.9 | 279.7 | **277.0** |
| **P0.2 (0.2%)** | 250.9 | 249.7 | 253.0 | **251.2** |
| **1% Low Average** | 259.5 | 258.3 | 262.4 | **260.0** |
| **0.1% Low Average** | 223.1 | 224.7 | 228.8 | **225.5** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.189 | 1.200 | 1.192 | **1.194** |
| **1% High Avg ms** | 3.874 | 3.892 | 3.829 | **3.865** |
| **0.1% High Avg ms** | 4.549 | 4.536 | 4.429 | **4.505** |

#### 📝 Notes / Wnioski
**[ENG]** In this scenario, core affinity manipulation was completely disabled (`AFFINITY OFF`). The results show a slight improvement over the pure STOCK configuration (around +10 FPS on the average), but it falls significantly behind the `Core -0` configuration in both Average FPS (~838 vs ~862) and 1% Lows. This demonstrates that leaving thread management entirely to the OS/Game scheduler without protecting it from the primary Core 0 overhead is sub-optimal for the 7800X3D.
**[PL]** W tym scenariuszu wyłączono wszelkie modyfikacje koligacji rdzeni (`AFFINITY OFF`). Wyniki pokazują minimalną poprawę względem czystej konfiguracji STOCK (ok. +10 FPS średnio), ale zauważalnie odstają od konfiguracji wyłączającej rdzeń zerowy (`Core -0`) - zarówno w średnim FPS (~838 względem ~862), jak i wartościach 1% Low. Dowodzi to, że pozostawienie zarządzania wątkami wyłącznie systemowi i grze, bez izolacji pierwszego rdzenia (Core 0), daje na procesorze 7800X3D suboptymalne rezultaty.

### ⚙️ Test Case: Hyper-Threading (SMT) OFF + Core 0 Disabled

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 900.6 | 897.2 | 900.3 | **899.4** |
| **P1 (1%)** | 301.3 | 302.4 | 307.4 | **303.7** |
| **P0.2 (0.2%)** | 275.3 | 278.2 | 284.6 | **279.4** |
| **1% Low Average** | 284.6 | 287.0 | 292.2 | **287.9** |
| **0.1% Low Average** | 242.9 | 252.2 | 252.3 | **249.1** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.110 | 1.115 | 1.111 | **1.112** |
| **1% High Avg ms** | 3.534 | 3.497 | 3.441 | **3.491** |
| **0.1% High Avg ms** | 4.188 | 4.002 | 4.041 | **4.077** |

#### 📝 Notes / Wnioski
**[ENG]** In this configuration, in-game settings were left untouched. Instead, the custom Process Core Optimizer application was used to disable Hyper-Threading (SMT) for the process and isolate it from the primary OS core (`Core 0`). The results are spectacular. The Average FPS skyrocketed to nearly 900 (a massive ~72 FPS jump from the STOCK baseline), while maintaining exceptionally tight 1% Lows (~288 FPS). This proves that eliminating virtual threads and protecting the game from background OS interruptions on the primary core yields the highest performance scaling on the 7800X3D.
**[PL]** W tej konfiguracji ustawienia samej gry pozostały nietknięte. Zamiast tego, przy użyciu autorskiego programu Process Core Optimizer, dla procesu gry wyłączono hiperwątkowość (SMT) oraz całkowicie odcięto dostęp do głównego rdzenia systemowego (`Core 0`). Wyniki są spektakularne. Średni FPS poszybował w okolice 900 klatek (skok o ok. 72 FPS względem czystego STOCK), przy zachowaniu niezwykle stabilnych ułamków 1% Low (~288 FPS). Dowodzi to, że eliminacja wirtualnych wątków oraz ochrona gry przed przerwaniami systemowymi w tle daje najlepsze możliwe skalowanie wydajności na procesorze 7800X3D.

### ⚙️ Test Case: Windows CPU Sets - Core 0 Disabled

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 863.6 | 859.0 | 866.3 | **863.0** |
| **P1 (1%)** | 292.3 | 290.3 | 294.1 | **292.3** |
| **P0.2 (0.2%)** | 269.6 | 266.6 | 275.1 | **270.5** |
| **1% Low Average** | 277.0 | 274.8 | 280.9 | **277.6** |
| **0.1% Low Average** | 239.8 | 236.7 | 248.4 | **241.6** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.158 | 1.164 | 1.154 | **1.159** |
| **1% High Avg ms** | 3.628 | 3.657 | 3.573 | **3.619** |
| **0.1% High Avg ms** | 4.245 | 4.285 | 4.070 | **4.200** |

#### 📝 Notes / Wnioski
**[ENG]** This test utilizes the Windows "CPU Sets" mechanism instead of strict hard affinity to park Core 0. The results are remarkably similar to the hard affinity test (`Core Affinity - Core 0 Disabled`). The average FPS sits solidly around ~863, providing a tangible boost over the STOCK configuration while matching the stability of hard affinity. It demonstrates that the Windows scheduler respects the soft limits imposed by CPU Sets perfectly in this scenario.
**[PL]** W tym teście wykorzystano mechanizm Windows "CPU Sets" zamiast "twardej" koligacji (Hard Affinity), aby odciążyć rdzeń 0 (Core 0). Wyniki są uderzająco podobne do testu twardej koligacji (`Core Affinity - Core 0 Disabled`). Średnia liczba FPS wynosi stabilne ~863 klatki, zapewniając wyraźny wzrost wydajności w stosunku do konfiguracji bazowej (STOCK), jednocześnie dorównując stabilnością klasycznej koligacji. Pokazuje to, że w tym scenariuszu systemowy scheduler idealnie respektuje "miękkie" limity narzucane przez mechanizm CPU Sets.

### ⚙️ Test Case: Windows CPU Sets - Hyper-Threading (SMT) OFF

#### 📈 FPS Results (Frames Per Second)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average FPS** | 845.1 | 847.4 | 847.0 | **846.5** |
| **P1 (1%)** | 277.3 | 278.5 | 282.4 | **279.4** |
| **P0.2 (0.2%)** | 249.5 | 252.9 | 255.7 | **252.7** |
| **1% Low Average** | 260.0 | 262.2 | 265.6 | **262.6** |
| **0.1% Low Average** | 227.8 | 232.1 | 232.8 | **230.9** |

#### ⏱️ Frametime Results (ms)

| Metric / Parametr | Run 1 | Run 2 | Run 3 | 🏆 AVERAGE / ŚREDNIA |
| :--- | :--- | :--- | :--- | :--- |
| **Average ms** | 1.183 | 1.180 | 1.181 | **1.181** |
| **1% High Avg ms** | 3.862 | 3.828 | 3.781 | **3.824** |
| **0.1% High Avg ms** | 4.429 | 4.348 | 4.343 | **4.373** |

#### 📝 Notes / Wnioski
**[ENG]** In this scenario, the custom application uses the Windows CPU Sets mechanism to disable Hyper-Threading (SMT) for the game, but without isolating it from the primary Core 0. The performance improves over the baseline STOCK configuration (~846 FPS vs ~827 FPS), proving that removing virtual threads is beneficial. However, it falls significantly short of the ~900 FPS achieved when Core 0 is simultaneously disabled. This highlights that while SMT removal helps, the critical bottleneck on the 7800X3D is OS background interference on the primary core.
**[PL]** W tym scenariuszu aplikacja wykorzystuje mechanizm Windows CPU Sets do wyłączenia hiperwątkowości (SMT) dla procesu gry, ale bez izolowania go od głównego rdzenia (Core 0). Wydajność wzrasta względem bazowej konfiguracji STOCK (~846 FPS vs ~827 FPS), co dowodzi, że usunięcie wirtualnych wątków przynosi korzyści. Wynik ten jest jednak znacznie niższy od potężnych ~900 FPS osiągniętych, gdy rdzeń zerowy był równocześnie wyłączony. Wyraźnie podkreśla to fakt, że choć wyłączenie SMT pomaga, głównym "wąskim gardłem" na 7800X3D są procesy i przerwania systemowe działające w tle na pierwszym rdzeniu.


