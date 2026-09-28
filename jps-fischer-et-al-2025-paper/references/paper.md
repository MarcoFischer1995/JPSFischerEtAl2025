# How degradation of lithium-ion batteries impacts capacity fade and resistance increase: A systematic, correlative analysis

Marco Fischer<sup>a,∗</sup>, Martin Johannes Brand<sup>a,b</sup>, Alexander Karger<sup>a</sup>, Manuel Rubio Gomez<sup>a</sup>, Mathias Rehm<sup>a</sup>, Johannes Natterer<sup>a,c</sup>, Andreas Jossen<sup>a</sup>

<sup>a</sup> *Technical University of Munich (TUM), TUM School of Engineering and Design; Department of Energy and Process Engineering, Chair of Electrical Energy Storage Technology (EES), Arcisstr. 21, 80333 Munich, Germany*<br><sup>b</sup> *Li.plus GmbH, Bergmannstr. 49, 80339 Munich, Germany*<br><sup>c</sup> *Infineon Technologies AG, Am Campeon 1-15, 85579 Neubiberg, Germany*

## Highlights

- 814-cell aging dataset covering NMC, NCA, and LFP chemistries.

- Capacity-resistance correlation below −0.8 for 97 % of tested cells.

- Power-law correlation fits capacity fade within ±2.5 % error.

- DC-pulse resistance more robust than frequency-domain features.

- Load-profile mapping enables accurate capacity fade prediction.

## Graphical abstract

[Graphical abstract](../assets/figure/graphical-abstract.jpg)

## Article info

*Keywords:* Lithium-ion battery; Aging; Correlation; Capacity; Resistance; Large-scale dataset

∗ Corresponding author.

_E-mail address:_ marco.fischer@tum.de (M. Fischer).

https://doi.org/10.1016/j.jpowsour.2025.237921

Received 2 April 2025; Received in revised form 3 June 2025; Accepted 15 July 2025

0378-7753/© 2025 The Authors. Published by Elsevier B.V. This is an open access article under the CC BY license ( http://creativecommons.org/licenses/by/4.0/ ).

## Abstract

Lithium-ion batteries play an essential role in a wide range of applications. It is, therefore, crucial to accurately determine their state of health, which is characterized by capacity fade and resistance increase. Their interdependency has received limited attention and this study places special emphasis on their linkage. We analyzed aging studies incorporating over 814 cells featuring NMC, NCA, and LFP chemistries and found a strong negative Pearson’s correlation coefficient (*r* < −0.8) for capacity fade and resistance increase in over 97 % of the cells investigated. This confirms that aging mechanisms affect both indicators simultaneously. We developed a power-law fit that accurately captures capacity fade with root mean square errors below ±2.5 % up to at least a state-of-health of 70 %. Additionally, our findings integrate multiple aging pathways into a single analytical framework, offering a practical tool for determining battery life and improving reliability in modern power applications. We show that both resistance and impedance are closely related to aging. Therefore, evaluating either one of them in experimental studies for performance analysis and incorporating them into machine learning feature sets should be mandatory for a comprehensive investigation of battery aging.

## 1. Introduction

Over the last two decades, lithium-ion batteries (LIBs) have become integral to a broad range of applications, including mobile devices, stationary home storage systems, and other emerging fields of e-mobility. In particular, sales of plug-in hybrid electric vehicles (PHEVs) and battery electric vehicles (BEVs) have rapidly increased in response to governmental regulations aimed at mitigating global warming. In Germany, the total number of registered electric vehicles increased from 18,948 in 2015 to 1,013,009 in 2023 [1]. This significant growth is mirrored across other sectors utilizing LIBs, highlighting the increasing demand for reliable and efficient state estimation. In 2024, the European Union enacted the EURO 7 regulation [2], which requires 5% accuracy in state of health (SOH) monitoring for all traction batteries. Consequently, the ongoing expansion of LIBs and the introduction of stricter regulations across diverse industries highlight the importance of effective methods for determining the capacity related state of health (SOH<sub>C</sub>).

Typically, determining the SOH<sub>C</sub> involves fully charging and discharging the battery or partially cycling through at least a range of 70% to 80% state of charge (SOC) [3,4] to extract diagnostic features. While these methods can provide accurate assessments, they are time-consuming, energy-intensive, and impractical for continuous monitoring, or the SOC range is too small for reliable feature extraction [3]. Consequently, faster, more robust, and more energy-efficient approaches for capacity related state of health determination in real-world applications are needed.

### 1.1. Aging: Definition, mechanisms, and impact on capacity and resistance

Understanding LIB degradation is essential for developing reliable and efficient methods to monitor battery health. Its measurable effects on the cell level, besides others, are capacity fade expressed in SOH<sub>C</sub> and relative resistance increase represented as *R*<sub>incr.</sub>. Both metrics are calculated as the ratio of the actual capacity *C*<sub>actual</sub> or resistance *R*<sub>actual</sub> to the nominal or initially determined values *C*<sub>N,t=0</sub> and *R*<sub>N,t=0</sub>. To isolate the increase in *R*<sub>incr.</sub>, we subtract 1 from the relative resistance. Additionally, battery usage can be quantified using equivalent full cycles (EFCs), defined as the cumulative charge throughput *Q*<sub>charge throughput</sub> divided by twice the nominal capacity *C*<sub>N</sub>. Thus, one EFC corresponds to the throughput associated with fully charging and discharging the cell at its nominal capacity:

[Eqs. (1.1)–(1.3)](../assets/figure/equations-1-1-to-1-3.jpg)

Eq. (1.1): SoH<sub>C</sub> = *C*<sub>actual</sub> / *C*<sub>N,t=0</sub><br>Eq. (1.2): *R*<sub>incr.</sub> = 1 − *R*<sub>actual</sub> / *R*<sub>N,t=0</sub><br>Eq. (1.3): EFC = *Q*<sub>charge throughput</sub> / (2 ⋅ *C*<sub>N</sub>)

The end of life (EOL) of a lithium-ion battery is often defined as reaching a specific threshold, typically between 70% to 80% for SOH<sub>C</sub> or between 50% to 100% for relative resistance increase (*R*<sub>incr.</sub>) [5–9]. As both, changes in SOH<sub>C</sub> and *R*<sub>incr.</sub>, are caused by the same underlying degradation mechanisms, resistance increase could be a simple and fast indicator of capacity fade. However, identifying a causal link requires a material-level understanding on how each degradation mechanism causes capacity fade and resistance increase.

Vetter et al. [10] systematically grouped these mechanisms by examining graphite anodes, lithium metal oxide cathodes, and electrode–electrolyte interfaces, leading to degradation modes loss of lithium inventory (LLI) and loss of active material (LAM) for both electrodes. LAM reduces the electrode surface area available for charge transfer, resulting in increased overpotentials and, consequently, to resistance increase [11]. LLI can result from isolated lithium in inactive areas [10, 12], lithium plating [13,14], or passivation-layer growth on both electrodes [12,15], which also increase resistance. Dubarry et al. [16] combined these degradation modes into a diagnostic-prognostic framework based on electrode open circuit potentials (OCPs) alignment, and Birkl et al. [15] experimentally refined the concept by including usage-dependent factors.

Passivation-layer growth, depleting lithium inventory and electrolyte species, has been identified by various studies as a significant degradation mechanism [3,17,18]. Edge et al. [12] introduced electrolyte degradation as a secondary degradation mechanism causing both LLI and loss of electrolyte (LE). Although LE cannot be quantified with the approach introduced by Dubarry et al. [16], it strongly affects capacity and resistance by (re-)forming solid electrolyte interface (SEI) at the anode and cathode electrolyte interphase (CEI) [12,19–22]. Below 1.4 V vs. Li/Li<sup>+</sup>, the anode potential falls outside of the typical electrolyte’s thermodynamic stability window [19,23], while nickel-rich cathodes can exceed 4.3 V to 4.5 V, leading to electrolyte oxidation and CEI growth [24,25]. These cathodes are also susceptible to surface phase transformations into spinel or rock-salt structures, exacerbating lithium diffusion constraints and resistance [26–30]. Ultimately, degradation mechanisms alter the availability of lithium inventory, active material, and electrolyte, leading to capacity fade and resistance increase [12,15,31,32]. Fig. 1 summarizes the connection between measurable aging effects, categorized by degradation modes and driven by aging mechanisms resulting from usage-dependent utilization.

At begin of life (BOL), atypical effects can occur. Capacity can increase and resistance can decrease due to anode overhang effects [33, 34], internal pressure buildup [35,36], SEI transformation at low potentials [37], particle cracking in the electrodes [38], or half-cell stoichiometry shifts triggered by LLI [39]. Although these behaviors typically appear only during initial cycles or early calendar aging, they should be acknowledged in comprehensive aging analyses.

### 1.2. Overview of existing research on the linkage of capacity fade and resistance increase

Several studies have investigated the correlation between capacity fade and resistance increase. Schuster et al. [40] observed continuous increases in high- and mid-frequency impedance during aging, maintaining a linear correlation even as the capacity trajectory shifts from linear to accelerated decline. Schmitt et al. [41] confirmed these trends in calendar-aged cells and reported that time-domain pulse resistance also increases with aging. Several groups have exploited the linkage empirically to determine SOH<sub>C</sub> using impedance or resistance measurements in laboratory and on-board applications [42–44].

Recent machine-learning approaches also highlight the importance of resistance for enhancing capacity fade estimations [45–47]. Growing open-source datasets [48–50] now support data-driven frameworks that can capture the complexity of stress profiles and aging more effectively. For instance, Paulson et al. [51] analyzed 396 features from over 300 pouch cells, representing more than 40 distinct pouch cell builds with varying capacities, chemistries, and electrolyte compositions. They found that two of the fifteen most relevant features involved resistance features. These findings emphasize the feasibility of resistance-based capacity assessments, where a strong correlation between increasing resistance and capacity fade enables fast SOH<sub>C</sub> determination. They also form the basis of predictive methods that integrate resistance data into empirical and machine-learning models.

Despite this well-documented correlation between capacity fade and resistance increase, gaps remain on whether such a relationship exists universally across various chemistries, formats, and measurement methods. Moreover, a systematic evaluation of which resistance measurement correlates best with capacity fade is still lacking. To this end, this study aims to determine how a systematic correlation between capacity fade and resistance increase can be established and exploited across different chemistries, cell formats, and measurement constraints for accurate, practical SOH<sub>C</sub> determination.

This publication is structured as follows. Section 2 outlines the underlying dataset, including the applied aging conditions, reference performance tests (RPTs), the methodology for Pearson correlation and *p*-value significance, and data preprocessing, fitting, and evaluation metrics. Section 3 presents the results of the preprocessing steps and the correlation analysis, concluding with fits that investigate the determination quality of resistance and impedance measurements. Finally, Section 4 summarizes these findings and suggests improvements for future investigations into the interdependency of capacity fade and resistance increase.

[Fig. 1](../assets/figure/figure-1.jpg)

**Fig. 1.** Summary of measurable aging effects in LIBs, categorized by degradation modes and driven by the underlying aging mechanisms resulting from usage-dependent utilization. _Source:_ Adapted from [12,15].

To the best of our knowledge, this is the first study to show that a closed-form power-law expression reliably links capacity fade to the 10 s direct current (DC)-pulse resistance increase across a dataset of 814 commercial cells. The cells span three chemistries (nickel manganese cobalt (NMC), nickel cobalt aluminum (NCA), and lithium iron phosphate (LFP)), capacities from 1.95 Ah to 120 Ah, and 14 independent ageing studies that cover calendar aging, constant current (CC)/constant current constant voltage (CCCV) cycling, and realistic drive-cycle profiles. More than 98% of the cells exhibit a strong negative Pearson correlation (*r* < −0.8). Of the three analytical expressions introduced in this work (linear, exponential, and power-law) the power-law achieves the best fit, attaining a cross-validated root mean square error (RMSE) below 2.5% down to a SOH<sub>C</sub> of 70%, thereby comfortably satisfying the 5% accuracy demanded by the EU Euro 7 regulation [2]. Even for the 152 cells that reach an early knee point, the residuals remain within ± 2.5%. Crucially, the model needs only one easily accessible feature (*R*<sub>incr.,DC,10s</sub>) and can run in real time on standard battery management system (BMS) microcontrollers using the battery pack’s existing current and voltage sensors. The approach therefore provides a robust, chemistry-independent way to on-board SOH<sub>C</sub> estimation in electric vehicles (EVs) and battery energy-storage systems.

## 2. Experimental

### 2.1. Dataset overview

In this study, we analyze available data from previous aging studies associated with our chair and in collaboration with research partners between 2015 and today. An overview is provided in Table 1, which includes references to previously utilized data from earlier publications, along with information about the manufacturers and cell specifications. In total, we analyze 14 datasets comprising 814 cells.

The data includes commercially available cells from various manufacturers, featuring cathodes made of NMC, NCA, and LFP, as well as anodes composed of graphite or silicon-graphite. It includes different form factors and designs with capacities ranging between 1.95 Ah to 120 Ah. Each cell type is labeled with its ID for better identification; if the same battery type has been used in different studies, an index in the dataset ID is added. The aging conditions for each dataset are depicted in Table 2, including information on the employed RPTs.

Five datasets include both, calendar and cycle aging, while nine datasets only include cycle aging. Calendar aging tests were conducted at temperatures ranging between 0 °C to 60 °C and across the entire SOC range. The VTC5A and FTC1 datasets encompass a more refined SOC range, while the other datasets focus on specific levels. Cycle aging tests were also conducted at temperatures ranging between 0 °C to 60 °C. For all datasets, the depth of discharge (DOD) ranges from 1% to 108% except for MJ1₁ and 50E₂, which solely cycled their cells with a DOD of 100%. 108% DOD is included due to a specific test condition in the cycle aging of the A dataset, investigating the aging behavior when cycling the cells up to 4.3 V. For most datasets, the investigated C-rates are below 2 C, except for the VTC5A, where currents up to 14 C were investigated. The protocols used for charging/discharging within the given boundaries differ between normal CC, CCCV cycling, or cycling with application-oriented load profiles.

The cells in the MJ1₂ dataset alternate between two phases: an application phase and a continuous cycling phase. In the application phase, cells are discharged using a worldwide harmonized light-duty vehicles test procedure (WLTP) current profile and then recharged with a 0.5 C CCCV protocol. This is followed by an eight-day continuous cycling phase. During this second phase, eight cells were CCCV charged with 0.5 C and discharged either at 1 C with varying voltage windows or according to the dynamic WLTP profile. Meanwhile, two cells remain at open circuit to serve as calendar aging references, as detailed by Schmitt et al. [3]. Additionally, datasets with the IDs VTC6A, M50L, M48, M50A, P42A, 48X2, and 50E₁, provided by the associated research partner HERO MotoCorp, were aged using a proprietary, application-oriented drive cycle. This drive cycle simulates rapid acceleration, regenerative braking, and partial SOC swings typical of two-wheel EV operations. By including these dynamic profiles alongside conventional CC and CCCV protocols, as well as various cell types, we are able to evaluate the correlation between capacity fade and resistance increase over a broad spectrum of use cases. Overall, we assume that the variety of applied aging conditions and the different cells investigated provide a comprehensive basis for analyzing the correlation between capacity fade and resistance increase.

**Table 1**

General specifications of the investigated cells, including battery name, anode and cathode materials, nominal voltage (*U*<sub>N</sub>), capacity (*C*<sub>N</sub>), resistance (*R*<sub>N</sub>)/impedance (*Z*<sub>N</sub>) given by the manufacturer’s datasheet, and the number of cells aged (*n*<sub>cells</sub>). If available, a reference to the origin of the data is provided.

[Table 1](../assets/table/table-1.csv)

| Ref | Dataset ID | Cell | Manufacturer | U_N | Anode | Cathode | Z_N/R_N | C_N | n_cells |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| [40] | A | IHR18650A | Molicel | 3.70 V | Gr | NMC | – | 1.95 Ah | 63 |
| – | PHEV2 | PHEV2 | Samsung SDI | 3.68 V | Gr | NMC | – | 120 Ah | 56 |
| [52] | MJ1₁ | INR18650 MJ1 | LG-Chem Ltd | 3.635 V | Gr–Si | NMC | Z^a ≤40 mΩ | 3.50 Ah | 37 |
| [3] | MJ1₂ | INR18650 MJ1 | LG-Chem Ltd | 3.635 V | Gr–Si | NMC | Z^a ≤40 mΩ | 3.50 Ah | 10 |
| – | 48X2 | INR21700 48X2 | Samsung SDI | 3.64 V | Gr | NMC | Z^a ≤13 ± 5 mΩ | 4.80 Ah | 40 |
| – | M50L | INR21700 M50L | LG-Chem Ltd | 3.69 V | Gr–Si | NMC | Z^a ≤15 ± 6 mΩ / R_DC^c ≤23 ± 6 mΩ | 4.80 Ah | 40 |
| – | M48 | INR21700 M48 | LG-Chem Ltd | 3.68 V | Gr–Si | NMC | Z^a ≤17 mΩ / R_DC^c ≤23 ± 6 mΩ | 4.60 Ah | 41 |
| – | VTC6A | US21700 VTC6A | Murata | 3.60 V | Gr | NCA | Z^a = 5 mΩ–15 mΩ; 9.7 mΩ Typ. | 4.10 Ah | 35 |
| – | M50A | INR21700 M50A | Molicel | 3.60 V | Gr | NCA | Z^b = 15 mΩ / R_DC^d = 25 mΩ | 5.00 Ah | 39 |
| – | P42A | INR21700 P42A | Molicel | 3.60 V | Gr | NCA | Z^b ≤10 mΩ / R_DC^e = 16 mΩ | 4.20 Ah | 40 |
| – | 50E₁ | INR21700 50E | Samsung SDI | 3.63 V | Gr–Si | NCA | Z^a = 13 ± 5 mΩ | 4.90 Ah | 38 |
| [53] | VTC5A | US18650 VTC5A | Murata | 3.60 V | Gr–Si | NCA | Z^a = 7 mΩ–15 mΩ; 13 mΩ Typ. | 2.60 Ah | 164 |
| – | 50E₂ | INR21700 50E | Samsung SDI | 3.63 V | Gr–Si | NCA | Z^a = 13 ± 5 mΩ | 4.90 Ah | 54 |
| [54,55] | FTC1 | US26650 FTC1 | Murata | 3.20 V | Gr | LFP | Z^b = 12 mΩ–22 mΩ; 18 mΩ Typ. | 3.00 Ah | 157 |
|  |  |  |  |  |  |  |  | Total: | 814 |

<sup>a</sup> *Z*<sub>1 kHz</sub>, SOC = 100%.<br><sup>b</sup> *Z*<sub>1 kHz</sub>.<br><sup>c</sup> *R*<sub>DC,10 s</sub>, SOC = 50%, 0.5 C.<br><sup>d</sup> *R*<sub>DC,10 s</sub>, 2 C.<br><sup>e</sup> *R*<sub>DC,1 s</sub>, 2.5 C.

**Table 2**

Summary of aging and reference performance test conditions applied for each dataset ID. The aging information is divided into cycle and calendar and further subdivided into specific conditions. Additionally, the conditions for determining the capacity, resistance, and impedance in the RPT are specified.

[Table 2](../assets/table/table-2.csv)

| Section | Subsection | Parameter | A | PHEV2 | MJ1₁ | MJ1₂ | Various^a | VTC5A | 50E₂ | FTC1 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Aging | Calendar | T/°C | 35, 50 | 10, 25, 40, 50, 60 | – | 25 | – | 5^b, 20, 35, 50, 60 | – | 0, 10, 25, 40, 60 |
| Aging | Calendar | SOC/% | 0, 10, 50, 90 | 30, 50, 80, 100 | – | 50 | – | 0, 10, 30, 40, 45^b, 50^b, 55, 60, 65, 70, 75, 80, 85, 90, 95, 100 | – | 0, 12.5, 25, 37.5, 50, 62.5, 75, 87.5, 100 |
| Aging | Cyclic | T/°C | 25, 35, 50 | 0, 5, 15, 25, 35, 45 | 0, 10, 25, 40 | 25 | 26, 35, 43 | 5^b, 20, 35^b, 50^b, 60^b | 25 | 25, 40 |
| Aging | Cyclic | DOD/% | 80, 100, 108 | 25, 50, 75, 80, 100 | 100 | 30, 80, 100 | 53, 61, 65, 69, 77 | 0^b, 5, 20^b, 30, 40, 60, 80, 90, 100^b | 100 | 1, 5, 10, 20, 40, 60, 80, 100 |
| Aging | Cyclic | C-rate/h^−1 | 0.2, 0.5, 1, 2 | 0.1, 0.2, 0.5, 1, 1.5, 2 | 0.5, 1 | 0.5, 1 | 0.5, 1.3 | 0.2, 0.5, 1^b, 1.5^b, 2, 2.5, 4, 5, 10, 11, 14 | 0.5 | 0.2, 0.5, 1, 2 |
| Aging | Cyclic | Ch. mode | CC, CCCV | CCCV | CCCV | CCCV | CCCV | CC^b | CC | CC |
| Aging | Cyclic | Dis. mode | CC, CCCV | CC | CC, CCCV | CC + Drive cycles | Drive cycles | CC^b | CC | CC |
| Reference performance test |  | T/°C | 25 | 25 | 25 | 25 | 26, 35, 43 | 20 | 25 | 25 |
| Reference performance test | Capacity | Dis. mode | CCCV | CC | CCCV | CCCV | CCCV | CCCV | CCCV | CCCV |
| Reference performance test | Capacity | C-rate/h^−1 | 1 | 0.3 | 0.2 | 0.2 | 0.3 | 1 | 0.5 | 1 |
| Reference performance test | Capacity | Term./h^−1 | 0.05 | – | 0.01 | 0.01 | 0.05 | 0.02 | 0.01 | 0.15 |
| Reference performance test | Resistance | SOC/% | 50 | 50 | 50 | 50 | 50 | 20, 50, 100 | 50 | 50 |
| Reference performance test | Resistance | Mean ch./dis. | Yes | n.d. | Yes | Yes | Discharge | Yes | Yes | Yes |
| Reference performance test | Resistance | C-rate/h^−1 | 1 | 1 | 1 | 1 | 0.5 | 1 | 0.33, 0.66, 1 | 1 |
| Reference performance test | Resistance | Duration/s | 10 | 10 | 10 | 10 | 10 | 0.1, 1, 10 | 0.01, 1, 5, 10 | 10 |
| Reference performance test | Impedance | SOC/% | 50 | – | 50 | – | – | – | – | 50 |
| Reference performance test | Impedance | f_min–f_max/Hz | 10^−2–10^4 | – | 10^−2–10^4 | – | – | – | – | 10^−2–10^4 |

<sup>a</sup> Aging conditions resp. RPTs have been applied for the following dataset IDs: VTC6A, M50L, M48, M50A, P42A, 48X2, 50E₁.<br><sup>b</sup> In addition, these aging conditions have been used to investigate the path dependence of LIBs via a combination of calendar and cyclic condition phases.

Repetitive RPTs were primarily conducted at 25 °C, except for the IDs noted as<sup>1</sup> in Table 2. In these cases, the RPTs were conducted at the same temperature used during the aging phase. Although the resistance and impedance are highly temperature-dependent [56,57], assessing them at a constant temperature only reflects the relative increase in resistance.

Capacity determination involved C-rates ranging from 0.2 C to 1.0 C across the cell’s usable voltage range, concluding with a constant voltage (CV) phase. The termination criterion for this phase was set between 0.01 C to 0.15 C. The only exception to this procedure is the PHEV2 dataset, which did not include a CV phase during discharge. However, since these cells were cycled at a relatively low C-rate of 0.3 C, their capacity determination is still considered independent of resistance-related effects.

Focusing on resistance determination, all investigated aging studies conducted resistance/impedance measurements at a SOC of 50%. Additionally, the VTC5A-cells were also assessed regarding resistance at SOC levels of 20% and 100%. The aging studies investigated typically employed a pulse-pair approach, which allowed for determining both charge and discharge resistance. When both values were obtained, the average was taken to improve accuracy and minimize potential systematic measurement errors. The resistances are calculated using Ohm’s law, as indicated in Eq. (2). The DC-pulse resistance is determined by the ratio of the difference in voltage and current at the beginning and end of a pulse, defined by the pulse duration *Δt*.

[Eq. (2)](../assets/figure/equation-2.jpg)

Eq. (2): *R*<sub>DC,Δt</sub> = Δ*U* / Δ*I* = (*u*(*t*<sub>0</sub> + Δ*t*) − *u*(*t*<sub>0</sub>)) / (*i*(*t*<sub>0</sub> + Δ*t*) − *i*(*t*<sub>0</sub>))

DC-pulse resistance measurements were conducted at 1 C and additionally at 0.33 C and 0.67 C for ID 50E₂ dataset. Resistances were evaluated for a pulse duration of 10 s with additional durations of 0.1 s, 1 s and 0.01 s, 1 s, and 5 s for the VTC5A, and 50E₂ datasets, respectively. For the PHEV2 dataset, it remained undefined whether a charge or discharge pulse was used for the resistance determination. Furthermore, the VTC6A, M50L, M48, M50A, P42A, 48X2, and 50E₁ datasets included only a discharge pulse at 0.5 C.

The RPTs in the A, MJ1₁, and FTC1 datasets additionally involve impedance measurements conducted across a frequency range of 1 ⋅ 10<sup>−2</sup> Hz to 1 ⋅ 10<sup>4</sup> Hz at a SOC of 50%. Due to varying evaluation methods, two key characteristics of the impedance’s real part are examined in detail. The first characteristic is the zero-crossing, denoted as *R*<sub>zc</sub>, which arises where the imaginary part of capacitive and inductive effects balance each other [56,58]. The second characteristic focuses on the impedance at the frequency range, marking both the onset of zero-crossing and the beginning of the diffusion-dominated region, which we refer to as polarization resistance *R*<sub>pl</sub>. This is often characterized by the charge-transfer, SEI and CEI resistance [56,58,59].

### 2.2. Data preparation and requirements

We applied a Hampel filter with a window size of 5 data points and a threshold factor of 2 to filter outliers in the resistance and impedance values. The Hampel filter is a moving median-based technique that relies on the median and the median absolute deviation (MAD), providing a more robust approach to outlier detection than other mean-based approaches [60]. This filter evaluates each data point within its sliding window and flags points as outliers if their absolute deviation from the median exceeds a MAD-based threshold. The chosen threshold *τ* = 2 corresponds to a ±2 *σ* band for normally distributed data, retaining about 95% of points while theoretically removing at most 5% [60]. Visual inspection of several random trajectories confirmed that this setting eliminated the obvious resistance artefacts yet preserved genuine electrochemical behavior. A higher threshold, e.g. *τ* = 3 left clear artefacts untouched, whereas a lower value *τ* = 1.5 began to suppress valid data. Hence, *τ* = 2 offered the best practical balance between sensitivity and specificity for our datasets. Further technical details are provided in Appendix A.

In addition to the Hampel filter, any measurement with a resistance exceeding 500 mΩ was classified as an outlier. For a specific subset of data in the VTC6A, M50L, M48, M50A, P42A, 48X2, and 50E₁ datasets, where consecutive identical resistance measurements were observed, we retained only the first occurrence and marked all subsequent identical values as outliers.

On top of this filtering, we established two criteria for individual cell data to be included in the correlation analysis: a minimum ΔSOH<sub>C</sub> of 3% and the availability of at least five RPT measurements. After the correlation analysis, we prepared the remaining data for normalization as provided in Eqs. (1.1) and (1.2). As discussed in Section 1.1, capacity and resistance could exhibit opposing trends at BOL. We exclude previously determined RPTs until the resistance reaches its global minimum to account for this atypical behavior and ensure modeling requirements. The normalization was then referenced to the first valid RPT instance, where both capacity and resistance measurements were available. To facilitate comparisons over aging, we additionally interpolated the data in increments of 1% ΔSOH<sub>C</sub> between BOL and end of test (EOT). Consequently, analyzing different intervals, such as from 100% to 90% SOH<sub>C</sub> or from 90% to 80% SOH<sub>C</sub>, yields an equivalent number of data points.

Fig. 2 summarizes the resulting dataset after preprocessing. Since all aging studies included the *R*<sub>DC,10s</sub> in their RPTs, we present findings related to this resistance. Fig. 2 (a) shows the results of the outlier detection process with the Hampel filter on an exemplary cell from the 50E₁ dataset. The black dots represent the original raw data, while the dashed lines mark the filter’s thresholds. Data points falling outside these thresholds are flagged as outliers (red circles), and those within are accepted as valid measurements (green dots). In Fig. 2 (b), the SOH<sub>C</sub> histogram depicts the SOH<sub>C</sub> at which the relative capacity trajectory is normalized to, as given in Eq. (1.1). This value corresponds to the capacity at which the 10 s DC-pulse resistance has its global minimum. Over 90% of the cells trajectories are normalized within the first 5% of capacity fade, indicating only a minor fraction of the overall data experiences RPT exclusions. Furthermore, 343 cells did not experience any exclusion. Lastly, Fig. 2 (c) presents the scatter plot of the complete preprocessed dataset, illustrating how capacity and resistance evolve under aging in terms of SOH<sub>C</sub> and *R*<sub>incr.</sub>.

814 cells were considered in the study, of which 87 were excluded for having fewer than five valid capacity measurements (60 cells) or exhibiting less than 3% capacity fade (27 cells), leaving 727 cells for the subsequent correlation analysis. Across all 814 cells, 20225 RPTs were conducted, of which 2448 (12%) were removed during preprocessing. Despite these exclusions, the pronounced scatter in Fig. 2 (c) confirms a relationship between capacity and resistance, although the precise correlation varies with the specific stress conditions and LIBs investigated. Initial observations indicate that SOH<sub>C</sub> could be determined through a quick resistance measurement, consistent with the degradation mechanisms discussed in Section 1.1.

### 2.3. Correlation analysis, fitting and evaluation metrics

To investigate the relationship between capacity fade and resistance increase, both in terms of direction and strength, we determine the Pearson’s correlation coefficient (PCC), as defined by Pearson in [61]:

[Eq. (3)](../assets/figure/equation-3.jpg)

Eq. (3): *r*(*x*, *y*) = COV<sub>x,y</sub> / (*σ*<sub>x</sub> ⋅ *σ*<sub>y</sub>) = Σ<sub>i=1</sub><sup>n</sup> (*x*<sub>i</sub> − *x̄*) ⋅ (*y*<sub>i</sub> − *ȳ*) / √(Σ<sub>i=1</sub><sup>n</sup> (*x*<sub>i</sub> − *x̄*)<sup>2</sup> ⋅ Σ<sub>i=1</sub><sup>n</sup> (*y*<sub>i</sub> − *ȳ*)<sup>2</sup>)

The PCC quantifies the linear relationship between two variables *x* and *y*. It is defined as the covariance between *x* and *y* divided by the product of their standard deviations *σ*<sub>x</sub> and *σ*<sub>y</sub>. In this context, *x̄* and *ȳ* denote the means of the variables *x* and *y*, respectively. The coefficient, *r*, ranges from −1 to 1, with values near these extremes indicating a strong linear correlation (either negative or positive), while values close to zero suggest a weak or nonexistent linear relationship. In this study, the variables *x* and *y* are relative capacity SOH<sub>C</sub> and relative resistance increase *R*<sub>incr.</sub>. Given the known aging behavior of LIBs with decreasing capacity and increasing resistance, we anticipate a negative correlation between these variables. However, a perfect correlation |*r*| = 1 is not expected due to the inherent variability in experimental data. To offer qualitative guidance on different PCC values, we refer to the recommendations in [40,62,63], which are summarized in Table 3.

To assess the statistical significance of the observed PCC, we determine the *p*-value. This *p*-value reflects the magnitude of the PCC while considering the sample size. It is derived from a hypothesis test based on the null hypothesis, which assumes no linear relationship between the two variables [62]. A *p*-value greater than the significance level *α* of 5% suggests that the PCC is not significant, whereas a *p*-value below this threshold indicates significance. For a stricter assessment, *α* can be set to 1%, resulting in a more robust determination of significance for the PCC.

Assuming a linear expression is a simple initial step in describing the interdependence between capacity fade and resistance increase, particularly when the PCC is strongly negative. However, the scatter observed in Fig. 2 (c) shows that a high PCC does not automatically render the linear expression an optimal candidate for fitting the correlation. Building on the strong negative correlation observed in Fig. 4, three analytical expressions are thus benchmarked. First, a purely linear dependence (see Eq. (4.2)) is employed as the baseline. Secondly, we test an exponential relationship (see Eq. (4.3)). A conceptually similar but inverted form has been used for impedance-capacity estimation by Xiong et al. [64]. Thirdly, many studies model calendar or cycle-induced capacity fade using a power-law expression in time or charge throughput, frequently approximating a square-root law [41]. We generalize that idea by expressing capacity as a power-law of the resistance increase (see Eq. (4.4)). To the best of our knowledge, this is the first study to link capacity fade directly to a single resistance feature via a power-law expression. When the exponent *β*<sub>2</sub> = 1, the power-law expression naturally collapses to the linear expression, so the linear case is nested within the more flexible formulation.

[Eqs. (4.1)–(4.4)](../assets/figure/equations-4-1-to-4-4.jpg)

Eq. (4.1): SOH<sub>C</sub> = *f*(*R*<sub>incr.</sub>)<br>Eq. (4.2): SOH<sub>C</sub> = 1 − *β*<sub>1</sub> ⋅ *R*<sub>incr.</sub><br>Eq. (4.3): SOH<sub>C</sub> = exp(*β*<sub>1</sub> ⋅ *R*<sub>incr.</sub>)<br>Eq. (4.4): SOH<sub>C</sub> = 1 − *β*<sub>1</sub> ⋅ (*R*<sub>incr.</sub>)<sup>*β*<sub>2</sub></sup>

We evaluate the quality of these fits using the RMSE as defined in Eq. (5):

[Eq. (5)](../assets/figure/equation-5.jpg)

Eq. (5): RMSE = √((1/*N*) Σ<sub>i=1</sub><sup>N</sup> (*y*<sub>i</sub> − *ŷ*<sub>i</sub>)<sup>2</sup>)

*N* represents the total number of observations, *y*<sub>i</sub> is the *i*th measurement, and *ŷ*<sub>i</sub> is the corresponding estimate. We also determine the adjusted coefficient of determination (*R*<sup>2</sup><sub>adj</sub>), which takes into account the total number of parameters, as further defined in Appendix B in Eq. (B.4). The *R*<sup>2</sup><sub>adj</sub> quantifies how well the model fits the observations on a scale from 0 to 1, where 1 indicates a perfect fit. In addition, we examine the distribution of the residuals to gain deeper insight into the accuracy of each fit and potential biases.

[Fig. 2](../assets/figure/figure-2.jpg)

**Fig. 2.** Overview of data preprocessing and the resulting dataset. (a) Resistance trajectory of a cell from the 50E₁ dataset serves as an example for illustrating outlier detection using the Hampel filter across EFCs. The black dots represent the raw data points, while the green markers highlight the valid points identified after outlier detection. The red circles indicate the outliers. (b) Histogram depicting the SOH<sub>C</sub> at which the relative capacity trajectory is normalized to *C*<sub>Rglobal,min</sub>, see Eq. (1.1). This value corresponds to the capacity at which the 10 s DC-pulse resistance has its global minimum. (c) Post-preprocessing scatter plot of *R*<sub>incr.,DC,10s</sub> against SOH<sub>C</sub> for all investigated cells. Horizontal lines at 100%, 80%, and 70% SOH<sub>C</sub> serve as reference levels, illustrating how capacity and resistance degrade interdependently as aging progresses. (For interpretation of the references to color in this figure legend, the reader is referred to the web version of this article.)

**Table 3**

Gradations of PCC values based on [40,62,63].

[Table 3](../assets/table/table-3.csv)

| Gradations | Range of \|r(x, y)\| |
| --- | --- |
| Weak/none | <0.4 |
| Moderate | 0.4 < \|r(x, y)\| < 0.8 |
| Strong | 0.8 < \|r(x, y)\| < 1.0 |
| Perfect | =1.0 |

All models are fitted and evaluated on the complete trajectories of RPTs available for every cell, specifically from BOL to the individual EOT. For clarity with respect to common industrial limits, we also report residual statistics in three univeral SOH<sub>C</sub> intervals (100% to 90%, 90% to 80%, and 80% to 70%), but no data are discarded from the fits themselves. In 152 of 727 cells (≈21%), the capacity fade begins to accelerate, a phenomenon commonly referred to as the knee-point [20,65]. The distribution of these identified cells that experience accelerated fade is as follows: 45 cells from dataset A, 9 cells from dataset MJ1₁, 9 cells from dataset 50E₁, 2 cells from dataset 48X2, 20 cells from dataset M50L, 7 cells from dataset M48, 6 cells from dataset M50A, and 50 cells from dataset 50E₂. All measurements collected after the knee are retained, ensuring that the fits are challenged throughout the full aging spectrum, including the accelerated fade regime.

[Fig. 3](../assets/figure/figure-3.jpg)

**Fig. 3.** Boxplots of the normalized capacity (a) and 10 s DC-pulse resistance (b) for all investigated LIBs at BOL (blue) and EOT (red) after preprocessing. The capacity *C* is normalized to the nominal capacity *C*<sub>N</sub> (see Table 1), and the resistance *R*<sub>DC,10s</sub> is normalized to the mean BOL resistance *R̄*<sub>DC,10s,BoL</sub> of each cell type. For reference, horizontal lines indicate both the nominal capacity and the mean BOL resistance (solid lines) as well as commonly used EOL criteria: *C* ∕ *C*<sub>N</sub> = *C*<sub>rel.</sub> = 80% (dashed), 70% (dotted), *R*<sub>DC,10s</sub>∕ *R̄*<sub>DC,10s,BoL</sub> = *R*<sub>rel.</sub> = 150% (dashed), and 200% (dotted). (For interpretation of the references to color in this figure legend, the reader is referred to the web version of this article.)

## 3. Results and discussion

### 3.1. Overview of preprocessed dataset

Fig. 3 compares capacity (a) and resistance (b) distributions at both BOL and EOT for each dataset ID. Values for capacity are normalized to the nominal capacity *C*<sub>N</sub>, while the resistance is normalized to the mean initial resistance *R̄*<sub>DC,10s,BoL</sub> of each dataset. The solid horizontal lines indicate nominal capacity and mean BOL resistance. Dashed and dotted lines denote commonly proposed EOL thresholds, i.e., 80% or 70% for SOH<sub>C</sub> and 150% and 200% for relative resistance. The coefficients of variation for capacity and *R*<sub>DC,10s</sub> at BOL and EOT, along with the PCC for these time points are provided in Table 4. The coefficient of variation is determined by dividing the standard deviation by the mean value within each dataset ID, either at BOL or EOT. The EOT is defined as the final measurement taken once a predefined stopping criterion or specified duration is reached for each aging condition.

**Table 4**

Coefficient of variation for capacity and *R*<sub>DC,10s</sub> along with the PCC at both BOL and EOT for each preprocessed dataset.

[Table 4](../assets/table/table-4.csv)

| Dataset ID | σ_C/μ_C / % (BOL) | σ_C/μ_C / % (EOT) | σ_R/μ_R / % (BOL) | σ_R/μ_R / % (EOT) | r(C, R_DC,10s) (BOL) | r(C, R_DC,10s) (EOT) |
| --- | --- | --- | --- | --- | --- | --- |
| A | 1.31 | 32.6 | 3.49 | 30.2 | −0.84** | −0.87** |
| PHEV2 | 0.30 | 7.55 | 2.22 | 18.7 | −0.13 | −0.92** |
| MJ1₁ | 1.98 | 7.26 | 5.03 | 12.8 | −0.66** | −0.51 |
| MJ1₂ | 1.42 | 21.5 | 1.85 | 30.5 | 0.74 | −0.98** |
| 48X2 | 1.75 | 4.85 | 8.69 | 10.3 | −0.13 | −0.78** |
| M50L | 2.56 | 20.3 | 9.21 | 26.0 | 0.18 | −0.96** |
| M48 | 1.58 | 13.4 | 5.12 | 38.0 | −0.45 | −0.66** |
| VTC6A | 8.11 | 12.5 | 13.9 | 31.8 | −0.20 | −0.61* |
| M50A | 5.48 | 11.6 | 16.3 | 25.7 | −0.72** | −0.69** |
| P42A | 4.21 | 8.91 | 12.8 | 32.2 | −0.25 | −0.74** |
| 50E₁ | 6.44 | 14.9 | 10.9 | 18.3 | 0.14 | −0.69** |
| VTC5A | 2.58 | 9.20 | 3.15 | 29.1 | 0.29* | −0.79** |
| 50E₂ | 1.03 | 10.2 | 1.16 | 19.3 | −0.77** | −0.90** |
| FTC1 | 2.16 | 10.9 | 2.77 | 12.5 | 0.57** | −0.57** |

\* Significant correlation for *α* = 5%: p-value < 5%.<br>\*\* Strong significant correlation for *α* = 1%: p-value < 1%

Capacity values in most datasets have a coefficient of variation below 2.6% at BOL, except for the VTC6A, M50A, P42A, and 50E₁ datasets, with the VTC6A dataset reaching 8.1%. Notably, those datasets with a median BOL capacity near 100% exhibit less variation than those below this threshold. We pinpoint this behavior to the exclusion of early RPTs before the global minimum resistance is reached, allowing more capacity divergence among cells that have experienced distinct aging. By EOT, the capacity variation becomes far more pronounced and up to 25 times higher for specific datasets. This reflects how different aging conditions cause widely varying capacity fades once a stopping criterion is met. The median SOH<sub>C</sub> for most datasets at EOT reaches or exceeds 80%, providing enough range to explore the interdependency between capacity fade and resistance increase.

*R*<sub>DC,10s</sub> values in most datasets have a coefficient of variation between 1% and 5% at BOL, except for the 48X2, M50L, M48, VTC6A, M50A, P42A, and 50E₁ datasets. We assume that this higher variation is attributed to diverse temperatures during the RPT, along with the strong temperature dependence of capacity and resistance, where the dependence of resistance is significantly greater than that of capacity [57]. As with capacity, preprocessing introduces minor additional variation due to the possible exclusion of early RPTs. By EOT, the resistance typically increases up to 50% to 100%, aligning with standard EOL limits.

Summarizing the above: At BOL, we consider the variations in capacity and resistance small, with higher spreads being attributed to temperature dependency and data preprocessing. By EOT, both capacity and resistance vary significantly within a given ID, showing a clear pattern: more substantial capacity fade generally corresponds to a more pronounced resistance rise, consistent with degradation mechanisms described in Section 1.1.

However, in the literature, it remains unclear whether a correlation between capacity and resistance is evident already at BOL or becomes apparent only after specific degradation mechanisms start to establish [63,66,67]. To explore this, Table 4 presents the PCC values at both BOL and EOT for each dataset.

While a strong negative correlation is absent at BOL, most datasets show a strong and statistically significant negative correlation at EOT, indicating that capacity fade generally correlates with resistance increase. Notable exceptions (VTC6A, MJ1₁) exhibit moderate correlations that are less significant or even weaker at EOT. Despite these outliers, the dominant trend supports that capacity decline is accompanied by a resistance increase, as anticipated from established aging behavior.

### 3.2. Correlation analysis of capacity fade and resistance increase

In the previous Section 3.1, we summarized the preprocessed dataset and provided an initial PCC analysis at both BOL and EOT. We observed a consistently strong and statistically significant negative PCC for nearly all datasets at EOT, complemented by an investigation of dominant degradation mechanisms/modes in Section 1.1. This establishes a strong basis for exploring the interdependency between capacity fade and resistance increase throughout aging.

Here, we extend the analysis by examining each battery’s PCC over its aging trajectory. Fig. 4 summarizes the correlation coefficients in histograms, capturing their dominant gradation. In total, 3242 capacity vs. resistance combinations were analyzed in Fig. 4 (a). Fig. 4 (b) focuses exclusively on capacity vs. *R*<sub>DC,10s</sub>, resulting in 727 cells after preprocessing.

Nearly all parameter combinations exhibit a strong, significant negative PCC (I). A smaller subset shows moderate correlation (II), and only a few display weak or no correlation (III). Of the total combinations, 3026 (≈93%) lie in region I, indicating a strongly negative relationship. 1552 of these show an almost perfect linear dependence, with a PCC in the range of −1.0 and −0.98, suggesting that a linear fit can effectively describe SOH<sub>C</sub> as a function of resistance/impedance. Meanwhile, 177 combinations (≈5.5%) belong to region II, and 39 (≈1.2%) to region III.

[Fig. 4](../assets/figure/figure-4.jpg)

**Fig. 4.** PCC histograms depicting 3242 possible combinations of SOH<sub>C</sub> and *R*<sub>incr.</sub> as detailed in Table 2, and after preprocessing. This includes: (a) all PCC between capacity fade and resistance/impedance increase during aging for each cell and (b) PCC of capacity fade and *R*<sub>incr.,DC,10s</sub> (*n*<sub>cells</sub> = 727). Both histograms are categorized into three gradations, as introduced in Table 3: **I** strong correlation, **II** moderate correlation, and **III** weak or no correlation.

Identical trends emerge when focusing on the distinct correlation of capacity fade and *R*<sub>incr.,DC,10s</sub>, as illustrated in Fig. 4 (b). Of the 727 cells, 710 cells (≈98%) lie in region I, indicating a strong, significant, and negative correlation. Within that gradation, 416 cells (≈57%) exhibit an almost perfect linear dependence with a PCC between −1.0 and −0.98. Only 14 cells (≈2%) fall into region II, and 2 cells are assigned to region III, displaying a weak or no correlation at −0.33 and −0.34.

Both outliers originate from the FTC1 dataset under identical aging conditions of 20% DOD, 50% average SOC, a 1 C charge and discharge rate, and 25 °C. Spingler et al. [55] showed that this shallow cycling protocol triggers an unusual capacity recovery effect, in which capacity increases while DC-pulse resistance decreases. Another 12 FTC1 cells, cycled at DOD < 40% with the same mean SOC, a 1 C C-rate (three cells at 2 C) and 40 °C, exhibit only a moderate correlation and show the same behavior. For LFP cells with a flat open circuit voltage (OCV), extensive shallow cycling suppresses the potential gradients that would normally drive lithium redistribution. Pronounced lithium-concentration inhomogeneities can therefore accumulate within the electrodes. During subsequent relaxation, these heterogeneities relax, resulting in the observed capacity recovery and concomitant resistance decrease. Such alterations in the relationship between capacity and resistance, combined with the inhomogeneities that develop during prolonged shallow cycling, can lead to overestimated aging parameters [68]. Additionally, partial recovery of capacity and resistance further complicates the measured correlation [68]. Hence, capacity and resistance should be recorded only after sufficient relaxation or after a low-rate homogenization cycle, so that the values reflect true ageing rather than transient inhomogeneity. The remaining 4 cells include those from the 50E₁ and PHEV2 datasets, all aged under comparatively mild conditions and experienced almost no loss in capacity.

Overall, these findings confirm a strong interconnection between capacity and resistance, making their correlation a promising basis for fast and straightforward SOH<sub>C</sub> determination. They also underscore the necessity of sufficient relaxation time to mitigate inhomogeneity after extensive LIB usage. In LFP-based cells, a flat OCV trajectory complicates homogenization caused by the absence of local potential gradients driven by different concentrations.

### 3.3. Fitting evaluation and selection

We begin by analyzing the datasets with IDs MJ1₁, MJ1₂, VTC5A, and FTC1, which feature NMC, NCA, and LFP chemistry systems. Fig. 5 illustrates the evolution of SOH<sub>C</sub> (a, d) and *R*<sub>incr.,DC,10s</sub> (b, e) over the course of both calendar and cycle aging, as well as their correlation and the fits (c, f). The stress conditions for calendar aging include a storage SOC of 50% at a temperature of 25 °C for the MJ1₂ and FTC1 cells. The VTC5A cell experiences a storage temperature of 20 °C. For cycle aging (d–f), the cells additionally experience a DOD of 100% and a C-rate of 1 C for both charging and discharging.

[Fig. 5](../assets/figure/figure-5.jpg)

**Fig. 5.** Exemplary aging trajectories for both calendar (a–c) and cycle (d–f) aging. The first and second columns display the SOH<sub>C</sub> and *R*<sub>incr.</sub>, respectively. For the calendar aging studies, the data is plotted against time (a) and (b), whereas for the cyclic aging, the trajectories are visualized against EFC (d) and (e). The third column (c) and (f) illustrates the relationship between SOH<sub>C</sub> and *R*<sub>incr.</sub> for each selected cell and test point. Linear (dashed lines), exponential (dash-dotted lines), and power-law (dotted lines) fits are included. MJ1₁ and MJ1₂ (blue) represent a NMC, VTC5A (turquoise) represents NCA, and FTC1 (orange) represents an LFP LIB. These cells were specifically chosen because they experienced nearly identical aging conditions: during calendar aging, they were stored at temperatures ranging from 20 °C to 25 °C with a SOC of 50%. For the cyclic aging, the same temperature and average SOC were maintained, with a DOD of 100% at a C-rate of 1 C for both charging and discharging. (For interpretation of the references to color in this figure legend, the reader is referred to the web version of this article.)

Observing the calendar aging results, it becomes evident that applying nearly identical stress conditions to different cells leads to distinct behaviors in capacity fade and resistance increase. This confirms that the correlation between capacity fade and resistance increase is highly cell-dependent, complicating the generalization of a single fit across different cell types. The MJ1₂ dataset exhibits a capacity fade of almost 10% after approximately 500 d, with a 10% resistance increase at EOT. In contrast, the VTC5A cell shows about half of that capacity fade and resistance increase, while the FTC1 cell experiences comparable fade and increase but over a longer period of 868 d. Fig. 5 (c) shows SOH<sub>C</sub> as a function of *R*<sub>incr.,DC,10s</sub>, together with the three proposed expressions. The linear fit is drawn as a dashed line, the exponential fit as a dash-dotted line, and the power-law fit as a dotted line. For VTC5A and FTC1, the correlation appears almost linear, and all three fits capture the data effectively. The respective values regarding the RMSE and *R*<sup>2</sup><sub>adj</sub> are depicted in Table 5 as well as for the cycle aging. However, the power-law fit provides a better description for MJ1₂, which experiences a rapid early capacity fade with a minor resistance increase, followed by a more pronounced linear increase in resistance. Cycle aging shows comparable results. When focusing on capacity fade and resistance increase over EFC, the LFP-based FTC1 cell achieves a much longer lifetime under identical conditions, reaching 7000 EFCs at 80% SOH<sub>C</sub> compared to about 400 EFCs for MJ1₂. For VTC5A at 90% SOH<sub>C</sub> and MJ1₂ at 80% SOH<sub>C</sub>, the resistance rises to 110% and 150%, respectively. In contrast, FTC1 only shows a minor resistance increase of 10% at 80% SOH<sub>C</sub>.

Overall, while the linear and exponential fits struggle to accurately capture the initial correlation between capacity fade and resistance increase, the power-law fit effectively addresses this gap and accurately reflects early-stage behavior. As shown in Table 5, the RMSE often distinguishes the fits more effectively than *R*<sup>2</sup><sub>adj</sub>, as identical *R*<sup>2</sup><sub>adj</sub> values can obscure differences in fit quality, particularly evident in the FTC1 cycle condition case. Even if two models share a similar *R*<sup>2</sup><sub>adj</sub>, they can still produce notably different RMSEs because *R*<sup>2</sup><sub>adj</sub> is derived from the ratio of error variance to total variance, whereas RMSE directly measures the size of the residuals on the original data scale. More information can be found in Appendix B. Hence, both RMSE and residuals are used in further investigations to determine which expression best represents the entire dataset.

[Fig. 6](../assets/figure/figure-6.jpg)

**Fig. 6.** Fitting evaluation was conducted for all tested combinations of capacity fade and resistance/impedance increase (a–c), with a specific focus on *R*<sub>incr.,DC,10s</sub> (d–f). Panels (a) and (d) present the RMSE distributions as histograms, while panels (b) and (e) visualize the overall distribution of residuals. Additionally, panels (c) and (f) illustrate the error distributions within three SOH<sub>C</sub> intervals: 100% to 90%, 90% to 80%, 80% to 70%. The linear, exponential, and power-law fits are represented by the colors red, blue, and green, respectively. (For interpretation of the references to color in this figure legend, the reader is referred to the web version of this article.)

**Table 5**

RMSE and *R*<sup>2</sup><sub>adj</sub> for the different models under calendar and cyclic aging depicted in Fig. 5.

[Table 5](../assets/table/table-5.csv)

| Dataset ID | Condition | Model | RMSE/% | R²_adj |
| --- | --- | --- | --- | --- |
| VTC5A | Calendar | Linear | 0.8 | 0.81 |
| VTC5A | Calendar | Exponential | 0.5 | 0.94 |
| VTC5A | Calendar | Power | 0.5 | 0.93 |
| VTC5A | Cyclic | Linear | 1.0 | 0.91 |
| VTC5A | Cyclic | Exponential | 1.0 | 0.86 |
| VTC5A | Cyclic | Power | 0.3 | 0.99 |
| FTC1 | Calendar | Linear | 0.2 | 0.99 |
| FTC1 | Calendar | Exponential | 0.2 | 0.98 |
| FTC1 | Calendar | Power | <0.01 | 0.99 |
| FTC1 | Cyclic | Linear | 1.1 | 0.99 |
| FTC1 | Cyclic | Exponential | 0.2 | 0.99 |
| FTC1 | Cyclic | Power | 0.3 | 0.99 |
| MJ1₁, MJ1₂ | Calendar | Linear | 1.1 | 0.89 |
| MJ1₁, MJ1₂ | Calendar | Exponential | 1.2 | 0.79 |
| MJ1₁, MJ1₂ | Calendar | Power | 0.2 | 0.99 |
| MJ1₁, MJ1₂ | Cyclic | Linear | 3.7 | 0.87 |
| MJ1₁, MJ1₂ | Cyclic | Exponential | 3.5 | 0.76 |
| MJ1₁, MJ1₂ | Cyclic | Power | 0.8 | 0.99 |

An overview of the fitting metrics incorporating all data combinations of SOH<sub>C</sub> and *R*<sub>incr.</sub> is provided in Fig. 6 (a–c), while (d–f) focuses again on the fits utilizing exclusively *R*<sub>incr.,DC,10s</sub>. The metrics of the linear fit are illustrated in red, the exponential fit in blue, and the power-law fit in green. The first column in Fig. 6 (a, d) depicts the achieved RMSE for all fits, and the second (b, e) the probability density distribution including the mean and standard deviation of the fitting error. Lastly, (c, f) summarizes the residuals regarding SOH<sub>C</sub> within intervals of 100% to 90%, 90% to 80%, and 80% to 70%.

We first analyze the achieved RMSEs to select the most promising expression. The power-law fit outperforms the other fitting expressions across all combinations of capacity and resistance, as well as for those using only *R*<sub>incr.,DC,10s</sub>. Specifically, for all combinations, 3015 (≈93%) achieve an RMSE below 2.5%, while 666 (≈92%) accomplish the same for *R*<sub>incr.,DC,10s</sub>. The RMSE for the other fitting expressions peak between 0.5% to 1% and gradually decreases as the RMSE increases.

When we examine the probability density distribution of the residuals for each fitting expression, it becomes evident that, with the exception of the power-law fit, the other fits do not have their means centered around 0% and exhibit a higher standard deviation. Additionally, the mean errors of these fits are slightly shifted to the left, indicating an underestimation of the actual SOH<sub>C</sub>. This trend was previously identified in Fig. 5 (c, f), where the power-law fit more accurately describes early-stage aging for the MJ1₁ and MJ1₂ cells. Contrary, the power-law fit demonstrates a mean of 0% and the lowest standard deviations of 1.76% and 1.54% for all data combinations and *R*<sub>incr.,DC,10s</sub>, respectively.

Fig. 6 (c, f) illustrates the fitting error distributions across three SOH<sub>C</sub> intervals, leading to a similar conclusion. During the early aging stage, the linear and exponential error distribution exhibit a variability of approximately 6.7% and 6.1% for all combinations and about 6.3% and 5.5% when focusing specifically on *R*<sub>incr.,DC,10s</sub>. As aging progresses, we observe an increasing variability in the remaining two buckets, though the exponential fit shows a less pronounced increase, while the median approaches 0%. This suggests that the overall fit tries to adequately represent the data but fails to capture the early stages of aging.

[Fig. 7](../assets/figure/figure-7.jpg)

**Fig. 7.** Fitting evaluation utilizing the *R*<sub>DC,10s</sub> and determined impedance features *R*<sub>zc</sub> and *R*<sub>pl</sub>. Each graph depicts the SOH<sub>C</sub> measured vs. estimated using the power-law expression. A dotted line represents a perfect fit, while dashed lines indicate the ±5 % tolerance defined by the EURO 7 regulation [2]. Each row (a–c), (d–f), and (g–i) evaluates the dataset IDs A, MJ1₁, and FTC1, respectively. Each column focuses on the different resistances/impedances, starting with *R*<sub>DC,10s</sub> (a, d, g), followed by *R*<sub>zc</sub> (b, e, h) and concluding with *R*<sub>pl</sub> (c, f, i).

In contrast, the error distribution variability for the power-law fit remains under 2.5% across all three intervals and for both data subsets, even for the 152 cells that exhibit a knee-point. Thus, the power-law fit effectively describes the correlation between SOH<sub>C</sub> and *R*<sub>incr.</sub> during aging and will be further utilized in Section 3.4 to identify optimal resistance/impedance candidates for characterizing capacity fade.

### 3.4. Identifying optimal candidates for capacity fade determination and possible real-world approaches

Based on previous findings, we have identified that the power-law fit is the most suitable expression for describing capacity fade in relation to resistance increase. In this section, we identify optimal resistance or impedance features capable of serving as reliable, rapid, and easily accessible indicators for capacity fade assessment. Specifically, we compare the DC-pulse resistance, as illustrated in Fig. 7 (a, d, g), with impedance-based features derived from electrochemical impedance spectroscopy (EIS) measurements. The analysis utilizes the datasets A (a–c), MJ1₁ (d–f), and FTC1 (g–i), each incorporating impedance data within their respective RPTs. Due to variations in evaluation methodologies, as described in Section 2.1, we focus on two characteristic impedance features extracted from the real part: *R*<sub>incr.,zc</sub> (b, e, h) and *R*<sub>incr.,pl</sub> (c, f, i).

The feature *R*<sub>incr.,DC,10s</sub> integrates all relevant internal processes of a LIB, including ohmic, charge-transfer, and diffusion-related contributions, spanning from short- to long-term electrochemical phenomena.

[Fig. 8](../assets/figure/figure-8.jpg)

**Fig. 8.** Global power-law fit approach between 10 s DC-pulse resistance (*R*<sub>incr.,DC,10s</sub>) and SOH<sub>C</sub> for the VTC5A dataset. Panels represent distinct aging conditions: (a, b) pure calendar or cycle aging; (c) a combination of sequentially switched calendar and cycle condition following each RPT; (d, e) sequentially switched calendar or cycle conditions after each RPT; and (f) overall dataset. Dashed lines indicate the global fit derived from data down to 70% SOH<sub>C</sub>, with dotted lines showing a tolerance of ±5%. Predictive accuracy is evaluated via ten repeated random splits (70% training, 30% validation), reporting the mean RMSE along with the standard deviation *σ*.

As degradation mechanisms distinctly affect overpotentials across different time constants, the selected 10 s DC-pulse resistance effectively captures these combined processes. Consequently, this resistance robustly reflects aging effects, with most experimental determinations lying within a tolerance of approximately ±5 %. The global RMSE for capacity fade determination based on this parameter ranges from 0.64% to 1.82%, considering all measured points within the examined aging studies.

In contrast, impedance-derived features exhibit higher global RMSE values. Several studies indicate that the polarization resistance *R*<sub>pl</sub> is significantly influenced by temperature and SOC variations [46,56, 69,70]. Such sensitivities lead to substantial variability, resulting in higher determination uncertainties. Accordingly, global RMSE values for *R*<sub>incr.,pl</sub> reach 2.16%, 2.51%, and 3.07% for the datasets A, MJ1₁, and FTC1, respectively. Meanwhile, the zero-crossing impedance feature, *R*<sub>incr.,zc</sub>, occupies an intermediate position in determination performance. Dataset MJ1₁ achieves a global RMSE of 0.90%, whereas dataset A yields a considerably higher error of 3.44%. For the FTC1 dataset, the feature *R*<sub>incr.,zc</sub> provides a notably favorable global RMSE of 1.28%, demonstrating comparable determination accuracies to the DC-pulse resistance. These results highlight the viability of the zero-crossing impedance feature as an alternative measure of capacity fade, contingent upon maintaining consistent and suitable measurement conditions. Such conditions must isolate aging-induced changes while minimizing the influence of temperature, SOC, and other interfering factors.

The power-law model employing the 10 s DC-pulse resistance allows accurate SOH<sub>C</sub> determination, consistently delivering a global RMSE below 2.5% across all datasets and varied aging conditions. This robust approach proves particularly useful in practical applications where aging conditions or load profiles can be clearly defined or categorized. Fig. 8 illustrates these findings, exemplified by the application to the VTC5A dataset utilizing *R*<sub>incr.,DC,10s</sub>. Even when exact matching of aging conditions is impractical, applying this methodology to subsets of similar aging profiles can still substantially benefit predictive accuracy.

The VTC5A dataset, after preprocessing, comprises 154 cells featuring diverse aging scenarios. These scenarios include distinct calendar or cycle aging conditions (a, b), sequentially alternating calendar and cycle conditions after each RPT (c), sequentially switched calendar-only or cycle-only conditions (d, e), as well as the comprehensive set including all scenarios (f). A global power-law fit, represented by dashed lines, is established based on these subsets, encompassing all measured trajectories down to their EOT or to a SOH<sub>C</sub> of 70%, with a tolerance interval of ±5 % indicated by dotted lines. To robustly assess the model’s predictive performance, a repeated random-splitting validation approach was adopted. Specifically, we performed ten independent iterations, each time randomly splitting the dataset into a training set containing 70% of the data and a validation set with the remaining 30%. For every iteration, the model was fitted exclusively on the training data and subsequently validated against the unseen validation data. Model accuracy is quantified by the mean RMSE and its standard deviation *σ* across these iterations. Additionally, a summary documenting subset compositions, cell counts, global fitting parameters, and respective cross-validation RMSEs is provided.

These comprehensive aging datasets facilitate robust SOH<sub>C</sub> assessment through a unified global-fit approach, owing to the consistent correlation between capacity fade and resistance increase within specific cell types. Despite variations in underlying aging mechanisms, the fitted parameters *β*<sub>1</sub> and *β*<sub>2</sub> consistently range between 0.24 to 0.37 and 0.50 to 0.63, respectively. Utilizing all available test points, the global-fit approach achieves an overall cross-validated RMSE of 2.36%, indicating a high reliability in capacity fade determination. Furthermore, when load profiles can be effectively categorized into subsets of similar aging characteristics, such as predominantly calendar or cycle aging Fig. 8 (a, b), further improved accuracy is attainable. Specifically, RMSEs of 1.52% and 2.26%, each with a standard deviation of 0.05%, can be obtained. It should also be noted that the approach’s accuracy strongly depends on the available data volume. For instance, subset (c), incorporating sequentially switched calendar and cycle aging trajectories of only five cells, results in a comparatively higher RMSE of 2.78 ± 0.21%. Although still capable, this highlights the necessity for sufficient data to improve accuracy. Correspondingly, subsets (d) and (e), which include 15 and 22 cells, exhibit improved performance, achieving RMSEs of 1.52 ± 0.14% and 1.37 ± 0.05%, respectively.

These results affirm that the power-law expression reliably captures the complex interdependencies between capacity fade and resistance increase for the VTC5A dataset, even though the exact aging conditions are unknown. Similar results appear in the other datasets in Table C.6, which reports the global-fit results for all additional test sets. While two subsets have a cross-validated RMSE exceeding 4%, the remaining 14 subsets are below 3.5%, demonstrating the robustness of this approach for assessing battery health. Currently, the subsets primarily represent calendar or cycle aging for each dataset ID. By refining these subsets to better align with specific user profiles, it may be possible to further lower the RMSE.

Among the investigated methods, the 10 s DC-pulse resistance measurement, conducted at 50% SOC and 1 C, consistently delivers the highest accuracy, maintaining a global prediction error below 2.5%. Conversely, impedance-based methods, particularly the *R*<sub>incr.,pl</sub> feature, are more susceptible to uncertainties arising from temperature fluctuations, shifts in half-cell SOC, and relaxation effects [39,56,71]. Nonetheless, the high-frequency impedance feature *R*<sub>incr.,zc</sub> presents a reliable alternative, achieving predictive performance comparable to the DC-pulse resistance measurement.

## 4. Conclusion

The aging of LIBs, caused by either calendar or cycle aging, provokes various degradation mechanisms, quantifiable in degradation modes, resulting in measurable effects, such as capacity fade and increased resistance. This understanding lays the groundwork for examining the correlation between capacity and resistance/impedance throughout aging.

To conduct this investigation, we collected a comprehensive dataset from 14 aging studies, which included 814 distinct cells subjected to various aging conditions stemming from both calendar and cycle aging. To harmonize these different datasets, we applied data preprocessing, excluding cells with fewer than five RPTs or those showing a capacity fade of less than 3%. Additionally, a Hampel filter was utilized to eliminate resistance outliers, leading to the exclusion of a total of 87 cells and 2448 RPTs.

Subsequently, we determined the PCC for a wide range of resistances/impedances, focusing particularly on the 10 s DC-pulse resistance. Our analysis revealed that over 93% of all data combinations, the PCC was below −0.8, and for over 98% of the cases pertaining to *R*<sub>incr.,DC,10s</sub>, a strong and significant correlation was determined. The remaining cases were associated with cells exhibiting capacity recovery and resistance decrease, resulting in atypical correlation behavior and a lower PCC. Across the entire aging window captured in the individual aging studies, from 100% SOH<sub>C</sub> down to each cell’s individual EOT, which is about 20% for the A dataset, the PCC remains monotonic and strongly negative.

The power-law expression emerged as the most effective expression, accommodating early-stage behavior characterized by minor resistance increases and more pronounced capacity fade, as well as behaviors beyond the knee-point, where both capacity fade and resistance increase accelerate. We observed errors of less than 2.5% during aging, well within the 5% tolerance required by the EU’s EURO 7 regulation. Additionally, we evaluated optimal candidates for fitting the correlation using various resistances and impedance features, concluding that the *R*<sub>incr.,DC,10s</sub> at a SOC equal to 50% and a C-rate of 1 C provides accurate determinations. Even when the precise aging conditions are unknown, a subset of similar conditions combined with a global fit approach can be employed to determine capacity fade with a RMSE less than 2.4%.

The simplicity of the 10 s DC-pulse and the closed-form power-law expression make the proposed approach well suited for embedded implementation. In a BMS, a 10 s pulse pair can be issued after each charge, once the battery pack has thermally and electrochemically stabilized. Utilizing the existing current and voltage sensing hardware, the BMS computes the *R*<sub>DC,10s</sub>. Additionally, on-board measurements of temperature, SOC, and C-rate enable the normalization of resistance to the reference conditions used during model calibration. This resistance is then mapped to the current SOH<sub>C</sub> through a look-up table. The calculation requires only a few arithmetic operations, making it feasible for real-time execution on standard microcontrollers in EVs as well as in battery energy storage systems.

Future work could include a more detailed examination of the resistances or impedance characteristics, potentially quantifying the degradation modes LLI, LE, and LAM for both electrodes. Nevertheless, a 10 s DC-pulse stimulates all types of overpotential, including purely ohmic, charge-transfer, and diffusion-related processes, thereby capturing all degradation mechanisms and leading to a reliable SOH<sub>C</sub> determination.

## CRediT authorship contribution statement

**Marco Fischer:** Writing – review & editing, Validation, Investigation, Conceptualization, Visualization, Methodology, Data curation, Writing – original draft, Software, Formal analysis. **Martin Johannes Brand:** Methodology, Writing – review & editing, Conceptualization, Data curation. **Alexander Karger:** Writing – review & editing, Data curation. **Manuel Rubio Gomez:** Writing – review & editing. **Mathias Rehm:** Writing – review & editing. **Johannes Natterer:** Writing – review & editing. **Andreas Jossen:** Supervision, Writing – review & editing, Funding acquisition, Project administration.

## Declaration of AI and AI-assisted technologies in the writing process

During the preparation of this work, the authors used Grammarly and ChatGPT for individual sections to improve language and readability. After using these tools, the authors reviewed and edited the content as needed and take full responsibility for the publication’s content.

## Declaration of competing interest

The authors declare that they have no known competing financial interests or personal relationships that could have appeared to influence the work reported in this paper.

## Acknowledgments

This research was financially supported by the German Federal Ministry for Economic Affairs and Energy (BMWE), Germany in the project accuRate (03ETE032C). The responsibility for this publication rests with the authors. We would like to thank Simon Schuster, Julius Schmitt, Markus Schindler, Alexander Karger, Philipp Jocher, Maik Naumann, and the associate partner Hero MotoCorp for providing the aging data for this publication. The fruitful discussions with Marcel Rogge are gratefully acknowledged.

## Appendix A. Hampel-filter

To identify and mitigate the influence of outliers in the data set, we employed a Hampel filter [72,73]. This robust technique detects deviations based on the median and the scaled MAD rather than the mean and standard deviation [60]. When considering a data point *x*<sub>i</sub> within a sliding window {*x*<sub>i−k</sub>, …, *x*<sub>i</sub>, …, *x*<sub>i+k</sub>}, we define *m* as the median of the window. The scaled MAD is calculated as follows:

[Eqs. (A.1)–(A.2)](../assets/figure/equations-a-1-to-a-2.jpg)

Eq. (A.1): MAD<sub>scaled</sub> = *κ* ⋅ median(|*x*<sub>j</sub> − *m*|)<br>where *κ* is defined as:<br>Eq. (A.2): *κ* = −1 / (√2 ⋅ erfcinv(3/2)) = 1 / (√2 ⋅ 0.4769) ≈ 1.4826

A data point is classified as an outlier if its absolute deviation from *m* exceeds the threshold defined by the scaled MAD multiplied by a user-defined threshold factor *τ*:

[Eq. (A.3)](../assets/figure/equation-a-3.jpg)

Eq. (A.3): |*x*<sub>i</sub> − *m*| > *τ* ⋅ MAD<sub>scaled</sub>

If an outlier is detected, the corresponding data point is excluded from further dataset analysis and fitting. Furthermore, at the edges of the data set, the window is truncated to ensure that it does not extend beyond the available data.

## Appendix B. Adjusted coefficient of determination

The following is a concise introduction to the *R*<sup>2</sup><sub>adj</sub> statistic, which measures how well a fitted model explains the underlying data set [57,74]. To determine *R*<sup>2</sup><sub>adj</sub>, the following equations are required. The sum of squared errors (SSE) in Eq. (B.1) measures the total deviation of the predicted responses *ŷ*<sub>i</sub> from the corresponding measured response values *y*<sub>i</sub>:

[Eq. (B.1)](../assets/figure/equation-b-1.jpg)

Eq. (B.1): SSE = Σ<sub>i=1</sub><sup>n</sup> (*y*<sub>i</sub> − *ŷ*<sub>i</sub>)<sup>2</sup>

The total sum of squares (SST) as presented in Eq. (B.2) represents the total deviation of the measured response values *y*<sub>i</sub> from their mean *ȳ*:

[Eq. (B.2)](../assets/figure/equation-b-2.jpg)

Eq. (B.2): SST = Σ<sub>i=1</sub><sup>n</sup> (*y*<sub>i</sub> − *ȳ*)<sup>2</sup>

The R-Square (*R*<sup>2</sup>) statistic, defined in Eq. (B.3), indicates how much of the variation in the data is explained by the fit. Its value ranges from 0 to 1, with higher values indicating that the model explains a larger fraction of the variance:

[Eq. (B.3)](../assets/figure/equation-b-3.jpg)

Eq. (B.3): *R*<sup>2</sup> = 1 − SSE / SST

However, when investigating different models with varying numbers of fitted parameters, as seen in Eqs. (4.2), (4.3), and (4.4), the *R*<sup>2</sup> value may increase simply due to the addition of parameters, regardless of whether the quality of the fit genuinely improves. To account for this, the *R*<sup>2</sup><sub>adj</sub> can be calculated using Eq. (B.4):

[Eq. (B.4)](../assets/figure/equation-b-4.jpg)

Eq. (B.4): *R*<sup>2</sup><sub>adj</sub> = 1 − (1 − *R*<sup>2</sup>) ⋅ (*n*−1)/(*n*−*m*) = 1 − (SSE/SST) ⋅ (*n*−1)/(*n*−*m*)

Here, the factor (*n*−1)/(*n*−*m*) accounts for the degrees of freedom, where *n* represents the number of response values and *m* denotes the number of fitted parameters. As well as the *R*<sup>2</sup>, the *R*<sup>2</sup><sub>adj</sub> cannot exceed 1.

## Appendix C. Results of the global power-law fit for the other datasets investigated

See Table C.6.

**Table C.6**

Summary of the global power-law fit between the 10 s DC-pulse resistance *R*<sub>incr.,DC,10s</sub> and SOH<sub>C</sub> for the other datasets investigated. When applicable, each dataset is subdivided into calendar- or cycle-based aging conditions and evaluated under a 70;30% training and test split, repeated ten times. The table includes the dataset ID, main aging condition, cell count, and the mean RMSE along with the standard deviation across these repeated splits.

[Table C.6](../assets/table/table-c6.csv)

| Dataset ID | Aging condition | n_cells | RMSE ± σ / % |
| --- | --- | --- | --- |
| A | Calendar | 30 | 3.32 ± 0.14 |
| A | Cycle | 29 | 4.29 ± 0.15 |
| PHEV2 | Calendar | 10 | 1.77 ± 0.20 |
| PHEV2 | Cycle | 33 | 1.93 ± 0.14 |
| MJ1₁ | Cycle | 34 | 2.89 ± 0.14 |
| MJ1₂ | Cycle | 10 | 1.78 ± 0.11 |
| 48X2 | Cycle | 39 | 1.67 ± 0.08 |
| M50L | Cycle | 37 | 3.05 ± 0.12 |
| M48 | Cycle | 37 | 3.53 ± 0.21 |
| VTC6A | Cycle | 24 | 4.57 ± 0.27 |
| M50A | Cycle | 34 | 3.03 ± 0.11 |
| P42A | Cycle | 16 | 2.35 ± 0.12 |
| 50E₁ | Cycle | 32 | 3.15 ± 0.24 |
| 50E₂ | Cycle | 54 | 0.84 ± 0.07 |
| FTC1 | Calendar | 44 | 1.28 ± 0.10 |
| FTC1 | Cycle | 61 | 3.02 ± 0.23 |

## Data availability

Data will be made available on request.

## References

- [1] Bestand an kraftfahrzeugen und kraftfahrzeuganhängern nach bundesländern, fahrzeugklassen und ausgewählten merkmalen, 2024, URL: https://www.kba.de/DE/Statistik/Fahrzeuge/Bestand/Vierteljaehrlicher_Bestand/viertelj%C3%A4hrlicher_bestand_node.html.

- [2] REGULATION (EU) 2024/1257 OF THE EUROPEAN PARLIAMENT AND OF THE COUNCIL, On type-approval of motor vehicles and engines and of systems, components and separate technical units intended for such vehicles, with respect to their emissions and battery durability (euro 7), amending regulation (EU) 2018/858 of the European parliament and of the council and repealing regulations (EC) no 715/2007 and (EC) no 595/2009 of the European parliament and of the council, commission regulation (EU) no 582/2011, commission regulation (EU) 2017/1151, commission regulation (EU) 2017/2400 and commission implementing regulation (EU) 2022/1362: Euro 7, 2024, URL: https://eur-lex.europa.eu/legal-content/EN/TXT/PDF/?uri=CELEX:32024R1257.

- [3] J. Schmitt, M. Rehm, A. Karger, A. Jossen, Capacity and degradation mode estimation for lithium-ion batteries based on partial charging curves at different current rates, J. Energy Storage 59 (2023) 106517, http://dx.doi.org/10.1016/j.est.2022.106517, URL: https://www.sciencedirect.com/science/article/pii/S2352152X22025063.

- [4] T. Hofmann, J. Hamar, B. Mager, S. Erhard, J.P. Schmidt, Transfer learning from synthetic data for open-circuit voltage curve reconstruction and state of health estimation of lithium-ion batteries from partial charging segments, Energy AI 17 (2024) 100382, http://dx.doi.org/10.1016/j.egyai.2024.100382, URL: https://www.sciencedirect.com/science/article/pii/S266654682400048X.

- [5] P. Iurilli, C. Brivio, R.E. Carrillo, V. Wood, Physics-based SoH estimation for Li-Ion cells, Batteries 8 (11) (2022) 204, http://dx.doi.org/10.3390/batteries8110204.

- [6] T. Hofmann, J. Hamar, M. Rogge, C. Zoerr, S. Erhard, J. Philipp Schmidt, Physics-informed neural networks for state of health estimation in lithium-ion batteries, J. Electrochem. Soc. 170 (9) (2023) 090524, http://dx.doi.org/10.1149/1945-7111/acf0ef.

- [7] W. Li, N. Sengupta, P. Dechent, D. Howey, A. Annaswamy, D.U. Sauer, One-shot battery degradation trajectory prediction with deep learning, J. Power Sources 506 (2021) 230024, http://dx.doi.org/10.1016/j.jpowsour.2021.230024.

- [8] A. Farmann, W. Waag, A. Marongiu, D.U. Sauer, Critical review of on-board capacity estimation techniques for lithium-ion batteries in electric and hybrid electric vehicles, J. Power Sources 281 (2015) 114–130, http://dx.doi.org/10.1016/j.jpowsour.2015.01.129.

- [9] M. Ecker, J.B. Gerschler, J. Vogel, S. Käbitz, F. Hust, P. Dechent, D.U. Sauer, Development of a lifetime prediction model for lithium-ion batteries based on extended accelerated aging test data, J. Power Sources 215 (2012) 248–257, http://dx.doi.org/10.1016/j.jpowsour.2012.05.012.

- [10] J. Vetter, P. Novák, M.R. Wagner, C. Veit, K.-C. Möller, J.O. Besenhard, M. Winter, M. Wohlfahrt-Mehrens, C. Vogler, A. Hammouche, Ageing mechanisms in lithium-ion batteries, J. Power Sources 147 (1–2) (2005) 269–281, http://dx.doi.org/10.1016/j.jpowsour.2005.01.006, URL: https://www.sciencedirect.com/science/article/pii/S0378775305000832.

- [11] J.M. Reniers, G. Mulder, D.A. Howey, Review and performance comparison of mechanical-chemical degradation models for lithium-ion batteries, J. Electrochem. Soc. 166 (14) (2019) A3189–A3200, http://dx.doi.org/10.1149/2.0281914jes, URL: https://iopscience.iop.org/article/10.1149/2.0281914jes.

- [12] J.S. Edge, S. O’Kane, R. Prosser, N.D. Kirkaldy, A.N. Patel, A. Hales, A. Ghosh, W. Ai, J. Chen, J. Yang, S. Li, M.-C. Pang, L. Bravo Diaz, A. Tomaszewska, M.W. Marzook, K.N. Radhakrishnan, H. Wang, Y. Patel, B. Wu, G.J. Offer, Lithium ion battery degradation: what you need to know, Phys. Chem. Chem. Phys. : PCCP 23 (14) (2021) 8200–8221, http://dx.doi.org/10.1039/d1cp00359c.

- [13] C. von Lüders, J. Keil, M. Webersberger, A. Jossen, Modeling of lithium plating and lithium stripping in lithium-ion batteries, J. Power Sources 414 (2019) 41–47, http://dx.doi.org/10.1016/j.jpowsour.2018.12.084, URL: https://www.sciencedirect.com/science/article/pii/S0378775318314484.

- [14] J. Keil, A. Jossen, Electrochemical modeling of linear and nonlinear aging of lithium-ion cells, J. Electrochem. Soc. 167 (11) (2020) 110535, http://dx.doi.org/10.1149/1945-7111/aba44f, URL: https://iopscience.iop.org/article/10.1149/1945-7111/aba44f.

- [15] C.R. Birkl, M.R. Roberts, E. McTurk, P.G. Bruce, D.A. Howey, Degradation diagnostics for lithium ion cells, J. Power Sources 341 (2017) 373–386, http://dx.doi.org/10.1016/j.jpowsour.2016.12.011, URL: https://www.sciencedirect.com/science/article/pii/S0378775316316998.

- [16] M. Dubarry, C. Truchot, B.Y. Liaw, Synthesize battery degradation modes via a diagnostic and prognostic model, J. Power Sources 219 (2012) 204–216, http://dx.doi.org/10.1016/j.jpowsour.2012.07.016, URL: https://www.sciencedirect.com/science/article/pii/S0378775312011330.

- [17] P. Gasper, N. Sunderlin, N. Dunlap, P. Walker, D.P. Finegan, K. Smith, F. Thakkar, Lithium loss, resistance growth, electrode expansion, gas evolution, and Li plating: Analyzing performance and failure of commercial large-format NMC-Gr lithium-ion pouch cells, J. Power Sources 604 (2024) 234494, http://dx.doi.org/10.1016/j.jpowsour.2024.234494, URL: https://www.sciencedirect.com/science/article/pii/S0378775324004452.

- [18] A. Karger, J. Schmitt, C. Kirst, J.P. Singer, L. Wildfeuer, A. Jossen, Mechanistic calendar aging model for lithium-ion batteries, J. Power Sources 578 (2023) 233208, http://dx.doi.org/10.1016/j.jpowsour.2023.233208, URL: https://www.sciencedirect.com/science/article/pii/S0378775323005839.

- [19] S.J. An, J. Li, C. Daniel, D. Mohanty, S. Nagpure, D.L. Wood, The state of understanding of the lithium-ion-battery graphite solid electrolyte interphase (SEI) and its relationship to formation cycling, Carbon 105 (2016) 52–76, http://dx.doi.org/10.1016/j.carbon.2016.04.008.

- [20] P.M. Attia, A. Bills, F. Brosa Planella, P. Dechent, G. dos Reis, M. Dubarry, P. Gasper, R. Gilchrist, S. Greenbank, D. Howey, O. Liu, E. Khoo, Y. Preger, A. Soni, S. Sripad, A.G. Stefanopoulou, V. Sulzer, Review—‘‘Knees’’ in lithium-ion battery aging trajectories, J. Electrochem. Soc. 169 (6) (2022) 060517, http://dx.doi.org/10.1149/1945-7111/ac6d13.

- [21] S.K. Heiskanen, J. Kim, B.L. Lucht, Generation and evolution of the solid electrolyte interphase of lithium-ion batteries, Joule 3 (10) (2019) 2322–2333, http://dx.doi.org/10.1016/j.joule.2019.08.018.

- [22] B. Heidrich, M. Stamm, O. Fromm, J. Kauling, M. Börner, M. Winter, P. Niehoff, Determining the origin of lithium inventory loss in NMC622||graphite lithium ion cells using an LiPF<sub>6</sub>-based electrolyte, J. Electrochem. Soc. 170 (1) (2023) 010530, http://dx.doi.org/10.1149/1945-7111/acb401.

- [23] J.P. Pender, G. Jha, D.H. Youn, J.M. Ziegler, I. Andoni, E.J. Choi, A. Heller, B.S. Dunn, P.S. Weiss, R.M. Penner, C.B. Mullins, Electrode degradation in lithium-ion batteries, ACS Nano 14 (2) (2020) 1243–1295, http://dx.doi.org/10.1021/acsnano.9b04365.

- [24] C. Poches, A.A. Razzaq, H. Studer, R. Ogilvie, B. Lama, T.R. Paudel, X. Li, K. Pupek, W. Xing, Fluorinated high-voltage electrolytes to stabilize nickel-rich lithium batteries, ACS Appl. Mater. Interfaces 15 (37) (2023) 43648–43655, http://dx.doi.org/10.1021/acsami.3c06586.

- [25] A. Manthiram, B. Song, W. Li, A perspective on nickel-rich layered oxide cathodes for lithium-ion batteries, Energy Storage Mater. 6 (2017) 125–139, http://dx.doi.org/10.1016/j.ensm.2016.10.007.

- [26] R. Jung, M. Metzger, F. Maglia, C. Stinner, H.A. Gasteiger, Oxygen release and its effect on the cycling stability of LiNi<sub>x</sub>Mn<sub>y</sub>Co<sub>z</sub>O<sub>2</sub> (NMC) cathode materials for Li-Ion batteries, J. Electrochem. Soc. 164 (7) (2017) A1361–A1377, http://dx.doi.org/10.1149/2.0021707jes.

- [27] T. Li, X.-Z. Yuan, L. Zhang, D. Song, K. Shi, C. Bock, Degradation mechanisms and mitigation strategies of nickel-rich NMC-based lithium-ion batteries, Electrochem. Energy Rev. 3 (1) (2020) 43–80, http://dx.doi.org/10.1007/s41918-019-00053-3.

- [28] F. Schipper, E.M. Erickson, C. Erk, J.-Y. Shin, F.F. Chesneau, D. Aurbach, Review—Recent advances and remaining challenges for lithium ion battery cathodes, J. Electrochem. Soc. 164 (1) (2017) A6220–A6228, http://dx.doi.org/10.1149/2.0351701jes.

- [29] Y. Mao, X. Wang, S. Xia, K. Zhang, C. Wei, S. Bak, Z. Shadike, X. Liu, Y. Yang, R. Xu, P. Pianetta, S. Ermon, E. Stavitski, K. Zhao, Z. Xu, F. Lin, X.-Q. Yang, E. Hu, Y. Liu, High–Voltage charging–Induced strain, heterogeneity, and micro–cracks in secondary particles of a Nickel–Rich layered cathode material, Adv. Funct. Mater. 29 (18) (2019) http://dx.doi.org/10.1002/adfm.201900247.

- [30] J. Li, X. Wang, X. Kong, H. Yang, J. Zeng, J. Zhao, Insight into the kinetic degradation of stored Nickel-Rich layered cathode materials for lithium-ion batteries, ACS Sustain. Chem. Eng. 9 (31) (2021) 10547–10556, http://dx.doi.org/10.1021/acssuschemeng.1c02486.

- [31] J. Landesfeind, H.A. Gasteiger, Temperature and concentration dependence of the ionic transport properties of lithium-ion battery electrolytes, J. Electrochem. Soc. 166 (14) (2019) A3079–A3097, http://dx.doi.org/10.1149/2.0571912jes.

- [32] L. Hartmann, L. Reuter, L. Wallisch, A. Beiersdorfer, A. Adam, D. Goldbach, T. Teufl, P. Lamp, H.A. Gasteiger, J. Wandt, Depletion of electrolyte salt upon calendaric aging of lithium-ion batteries and its effect on cell performance, J. Electrochem. Soc. 171 (6) (2024) 060506, http://dx.doi.org/10.1149/1945-7111/ad4821.

- [33] T. Roth, L. Streck, N. Mujanovic, M. Winter, P. Niehoff, A. Jossen, Transient self-discharge after formation in lithium-ion cells: Impact of state-of-charge and anode overhang, J. Electrochem. Soc. 170 (8) (2023) 080524, http://dx.doi.org/10.1149/1945-7111/acf164.

- [34] J. Guo, Y. Li, J. Meng, K. Pedersen, L. Gurevich, D.-I. Stroe, Understanding the mechanism of capacity increase during early cycling of commercial NMC/graphite lithium-ion batteries, J. Energy Chem. 74 (2022) 34–44, http://dx.doi.org/10.1016/j.jechem.2022.07.005.

- [35] A. Aufschläger, S. Kücher, L. Kraft, F. Spingler, P. Niehoff, A. Jossen, High precision measurement of reversible swelling and electrochemical performance of flexibly compressed 5 Ah NMC622/graphite lithium-ion pouch cells, J. Energy Storage 59 (2023) 106483, http://dx.doi.org/10.1016/j.est.2022.106483.

- [36] S. Friedrich, S. Stojecevic, P. Rapp, S. Helmer, M. Bock, A. Durdel, H.A. Gasteiger, A. Jossen, Effect of mechanical pressure on lifetime, expansion, and porosity of silicon-dominant anodes in laboratory lithium-ion cells, J. Electrochem. Soc. 171 (5) (2024) 050540, http://dx.doi.org/10.1149/1945-7111/ad36e6.

- [37] S. Zhang, M.S. Ding, K. Xu, J. Allen, T.R. Jow, Understanding solid electrolyte interface film formation on graphite electrodes, Electrochem. Solid-State Lett. 4 (12) (2001) A206, http://dx.doi.org/10.1149/1.1414946.

- [38] S. Oswald, D. Pritzl, M. Wetjen, H.A. Gasteiger, Novel method for monitoring the electrochemical capacitance by in situ impedance spectroscopy as indicator for particle cracking of nickel-rich NCMs: Part I. Theory and validation, J. Electrochem. Soc. 167 (10) (2020) 100511, http://dx.doi.org/10.1149/1945-7111/ab9187.

- [39] S. Friedrich, S. Helmer, L. Reuter, J.L.S. Dickmanns, A. Durdel, A. Jossen, Effect of mechanical pressure on rate capability, lifetime, and expansion in multilayer pouch cells with silicon-dominant anodes, J. Electrochem. Soc. 171 (9) (2024) 090503, http://dx.doi.org/10.1149/1945-7111/ad71f6.

- [40] S.F. Schuster, M.J. Brand, C. Campestrini, M. Gleissenberger, A. Jossen, Correlation between capacity and impedance of lithium-ion cells during calendar and cycle life, J. Power Sources 305 (2016) 191–199, http://dx.doi.org/10.1016/j.jpowsour.2015.11.096.

- [41] J. Schmitt, A. Maheshwari, M. Heck, S. Lux, M. Vetter, Impedance change and capacity fade of lithium nickel manganese cobalt oxide-based batteries during calendar aging, J. Power Sources 353 (2017) 183–194, http://dx.doi.org/10.1016/j.jpowsour.2017.03.090.

- [42] G. Caposciutti, G. Bandini, M. Marracci, A. Buffi, B. Tellini, Li-ion batteries state of health analysis via electro-chemical impedance spectroscopy, in: 2021 IEEE International Workshop on Metrology for Automotive (MetroAutomotive), IEEE, 2021, pp. 36–41, http://dx.doi.org/10.1109/MetroAutomotive50197.2021.9502724.

- [43] M. Ecker, N. Nieto, S. Käbitz, J. Schmalstieg, H. Blanke, A. Warnecke, D.U. Sauer, Calendar and cycle life study of Li(NiMnCo)O2-based 18650 lithium-ion batteries, J. Power Sources 248 (2014) 839–851, http://dx.doi.org/10.1016/j.jpowsour.2013.09.143.

- [44] K. Takeno, Quick testing of batteries in lithium-ion battery packs with impedance-measuring technology, J. Power Sources 128 (1) (2004) 67–75, http://dx.doi.org/10.1016/j.jpowsour.2003.09.045.

- [45] Y. Zhang, Q. Tang, Y. Zhang, J. Wang, U. Stimming, A.A. Lee, Identifying degradation patterns of lithium ion batteries from impedance spectroscopy using machine learning, Nat. Commun. 11 (1) (2020) 1706, http://dx.doi.org/10.1038/s41467-020-15235-7.

- [46] P. Gasper, A. Schiek, K. Smith, Y. Shimonishi, S. Yoshida, Predicting battery capacity from impedance at varying temperature and state of charge using machine learning, Cell Rep. Phys. Sci. 3 (12) (2022) 101184, http://dx.doi.org/10.1016/j.xcrp.2022.101184, URL: https://www.sciencedirect.com/science/article/pii/S2666386422005021.

- [47] H. Ruan, J. Chen, W. Ai, B. Wu, Generalised diagnostic framework for rapid battery degradation quantification with deep learning, Energy AI 9 (2022) 100158, http://dx.doi.org/10.1016/j.egyai.2022.100158.

- [48] G. dos Reis, C. Strange, M. Yadav, S. Li, Lithium-ion battery data and where to find it, Energy AI 5 (2021) 100081, http://dx.doi.org/10.1016/j.egyai.2021.100081.

- [49] Q. Mayemba, R. Mingant, Li, G. Ducret, P. Venet, Aging datasets of commercial lithium-ion batteries: A review, J. Energy Storage 83 (2024) 110560, http://dx.doi.org/10.1016/j.est.2024.110560.

- [50] M. Hassini, E. Redondo-Iglesias, P. Venet, Lithium–Ion battery data: From production to prediction, Batteries 9 (7) (2023) 385, http://dx.doi.org/10.3390/batteries9070385.

- [51] N.H. Paulson, J. Kubal, L. Ward, S. Saxena, W. Lu, S.J. Babinec, Feature engineering for machine learning enabled early prediction of battery lifetime, J. Power Sources 527 (2022) 231127, http://dx.doi.org/10.1016/j.jpowsour.2022.231127.

- [52] M. Schindler, J. Sturm, S. Ludwig, A. Durdel, A. Jossen, Comprehensive analysis of the aging behavior of Nickel-Rich, silicon-graphite lithium-ion cells subject to varying temperature and charging profiles, J. Electrochem. Soc. 168 (6) (2021) 060522, http://dx.doi.org/10.1149/1945-7111/ac03f6, URL: https://iopscience.iop.org/article/10.1149/1945-7111/ac03f6.

- [53] L. Wildfeuer, A. Karger, D. Aygül, N. Wassiliadis, A. Jossen, M. Lienkamp, Experimental degradation study of a commercial lithium-ion battery, J. Power Sources 560 (2023) 232498, http://dx.doi.org/10.1016/j.jpowsour.2022.232498. 

- [54] M. Naumann, F.B. Spingler, A. Jossen, Analysis and modeling of cycle aging of a commercial LiFePO4/graphite cell, J. Power Sources 451 (2020) 227666, http://dx.doi.org/10.1016/j.jpowsour.2019.227666, URL: https://www.sciencedirect.com/science/article/pii/S0378775319316593.

- [55] F.B. Spingler, M. Naumann, A. Jossen, Capacity recovery effect in commercial LiFePO4 / graphite cells, J. Electrochem. Soc. 167 (4) (2020) 040526, http://dx.doi.org/10.1149/1945-7111/ab7900, URL: https://iopscience.iop.org/article/10.1149/1945-7111/ab7900.

- [56] W. Waag, S. Käbitz, D.U. Sauer, Experimental investigation of the lithium-ion battery impedance characteristic at various conditions and aging states and its influence on the application, Appl. Energy 102 (2013) 885–897, http://dx.doi.org/10.1016/j.apenergy.2012.09.030.

- [57] S. Ludwig, I. Zilberman, A. Oberbauer, M. Rogge, M. Fischer, M. Rehm, A. Jossen, Adaptive method for sensorless temperature estimation over the lifetime of lithium-ion batteries, J. Power Sources 521 (2022) 230864, http://dx.doi.org/10.1016/j.jpowsour.2021.230864.

- [58] A. Barai, K. Uddin, W.D. Widanage, A. McGordon, P. Jennings, A study of the influence of measurement timescale on internal resistance characterisation methodologies for lithium-ion cells, Sci. Rep. 8 (1) (2018) 21.

- [59] P. Iurilli, C. Brivio, V. Wood, On the use of electrochemical impedance spectroscopy to characterize and model the aging phenomena of lithium-ion batteries: a critical review, J. Power Sources 505 (2021) 229860, http://dx.doi.org/10.1016/j.jpowsour.2021.229860.

- [60] C. Leys, C. Ley, O. Klein, P. Bernard, L. Licata, Detecting outliers: Do not use standard deviation around the mean, use absolute deviation around the median, J. Exp. Soc. Psychol. 49 (4) (2013) 764–766, http://dx.doi.org/10.1016/j.jesp.2013.03.013.

- [61] K. Pearson, VII. Note on regression and inheritance in the case of two parents, Proc. R. Soc. Lond. 58 (347–352) (1895) 240–242, http://dx.doi.org/10.1098/rspl.1895.0041.

- [62] R. Leonhart, Lehrbuch Statistik: Einstieg und Vertiefung, 5. überarbeitete Auflage ed., Hogrefe, Bern, 2022, http://dx.doi.org/10.1024/86258-000.

- [63] K. Rumpf, M. Naumann, A. Jossen, Experimental investigation of parametric cell-to-cell variation and correlation based on 1100 commercial lithium-ion cells, J. Energy Storage 14 (2017) 224–243, http://dx.doi.org/10.1016/j.est.2017.09.010, URL: https://www.sciencedirect.com/science/article/pii/S2352152X17302633.

- [64] R. Xiong, J. Tian, H. Mu, C. Wang, A systematic model-based degradation behavior recognition and health monitoring method for lithium-ion batteries, Appl. Energy 207 (2017) 372–383, http://dx.doi.org/10.1016/j.apenergy.2017.05.124, URL: https://www.sciencedirect.com/science/article/pii/S0306261917306645.

- [65] K. Kim, M. Kim, H. Churr, G. Lee, S. Han, G-K curve-based knee point prediction method for li-ion batteries, in: 2021 21st International Conference on Control, Automation and Systems, ICCAS, IEEE, 2021, pp. 1190–1193, http://dx.doi.org/10.23919/ICCAS52745.2021.9650014.

- [66] F. An, L. Chen, J. Huang, J. Zhang, P. Li, Rate dependence of cell-to-cell variations of lithium-ion cells, Sci. Rep. 6 (1) (2016) 35051, http://dx.doi.org/10.1038/srep35051, URL: https://www.nature.com/articles/srep35051.

- [67] P. Dechent, E. Barbers, A. Epp, D. Jöst, W. Li, D.U. Sauer, S. Lehner, Correlation of health indicators on lithium–Ion batteries, Energy Technol. 11 (7) (2023) http://dx.doi.org/10.1002/ente.202201398.

- [68] M. Rogge, A. Jossen, Path–dependent ageing of lithium–ion batteries and implications on the ageing assessment of accelerated ageing tests, Batter. Supercaps 7 (1) (2024) e202300575, http://dx.doi.org/10.1002/batt.202300575, URL: https://chemistry-europe.onlinelibrary.wiley.com/doi/10.1002/batt.202300575.

- [69] J.P. Schmidt, Verfahren zur charakterisierung und modellierung von lithium-ionen zellen: Zugl.: Karlsruher institut für technologie, KIT, diss., 2013, Schriften des Instituts für Werkstoffe der Elektrotechnik, Karlsruher Institut für Technologie, vol. 25, KIT Scientific Publishing, Karlsruhe, 2013.

- [70] T. Hackmann, S. Esser, M.A. Danzer, Operando determination of lithium-ion cell temperature based on electrochemical impedance features, J. Power Sources 615 (2024) 235036, http://dx.doi.org/10.1016/j.jpowsour.2024.235036.

- [71] F.M. Kindermann, A. Noel, S.V. Erhard, A. Jossen, Long-term equalization effects in li-ion batteries due to local state of charge inhomogeneities and their impact on impedance measurements, Electrochim. Acta 185 (2015) 107–116, http://dx.doi.org/10.1016/j.electacta.2015.10.108.

- [72] F.R. Hampel, The influence curve and its role in robust estimation, J. Amer. Statist. Assoc. 69 (346) (1974) 383–393, http://dx.doi.org/10.1080/01621459.1974.10482962.

- [73] The MathWorks, Inc. N.S., Isoutlier: R2024b, 2025, URL: https://de.mathworks.com/help/matlab/ref/isoutlier.html.

- [74] N.S. Raju, R. Bilgic, J.E. Edwards, P.F. Fleer, Methodology review: Estimation of population validity and cross-validity, and the use of equal weights in prediction, 1997.

## Conversion notes

- Source: M. Fischer, M.J. Brand, A. Karger, M. Rubio Gomez, M. Rehm, J. Natterer, A. Jossen, Journal of Power Sources 656 (2025) 237921, https://doi.org/10.1016/j.jpowsour.2025.237921 (published version of record).
- License: open access under CC BY 4.0 (https://creativecommons.org/licenses/by/4.0/). Reuse requires attribution to the original article.
- Data availability as stated in the article: data will be made available on request. No raw data or code is included in this package.
