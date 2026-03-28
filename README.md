# Experiment 4

# Differential Amplifier Analysis

## Aim

To design and simulate three MOSFET differential amplifier configurations using LTspice, carry out DC, transient, and AC analyses, and compare their performance in terms of gain, bandwidth, and power consumption.

---

## Introduction

A differential amplifier is an essential building block in analog electronics that amplifies the difference between two input signals while rejecting signals common to both inputs. This makes it highly effective in minimizing noise.

MOSFET-based differential amplifiers are commonly used in integrated circuits such as operational amplifiers and comparators because of their high gain, good noise immunity, and efficient operation.

In this experiment, three different MOSFET differential amplifier configurations are designed and simulated using LTspice. Their characteristics are studied through DC, transient, and AC analyses to compare performance.

---

## Theory

A differential amplifier produces an output based on the difference between two input voltages:

v_id = v_in1 - v_in2

It typically consists of two matched MOSFETs sharing a common source node connected to a constant current source, with loads connected at the drains.

For small input differences, both transistors remain in saturation and share current equally, resulting in linear amplification.

The gain is given by:

A_v = g_m × R_out

where:
- g_m = transconductance
- R_out = output resistance

Transconductance:

g_m = (2 × I_D) / V_ov

For larger input differences:

v_id > √2 × V_ov

one transistor turns OFF, causing non-linear operation.

Load types influence performance:
- Resistive load → moderate gain  
- Active load → higher gain  
- Current mirror load → maximum gain  

---

# Circuit 1: Differential Amplifier with Resistive Load
circuit diagram:
<img width="1029" height="781" alt="image" src="https://github.com/user-attachments/assets/086d748f-befc-4b50-8182-a455590d91bb" />

## Working Principle

This configuration uses two NMOS transistors with resistors connected at their drains. A constant tail current is shared between them.

Depending on the input difference:
- If v_in1 > v_in2 → M1 carries more current  
- If v_in2 > v_in1 → M2 carries more current  

The variation in current creates voltage drops across the resistors, producing the output.

---

## Design Summary

Given:
- VDD = +0.9V, VSS = -0.9V  
- Power ≤ 1.8mW  
- I_SS = 1mA (selected)  

Current distribution:
I_D1 = I_D2 = 0.5mA  

Load resistance:
R_D = 0.9 / 0.5mA = 1.8kΩ  

Bias values:
- V_G = 0V  
- V_S = -0.7V  
- V_GS = 0.7V  
- V_OV = 0.34V  
- V_DS = 0.7V → saturation condition satisfied  

Width:
W ≈ 17.6µm → adjusted to ≈ 28.5µm in simulation  

---

## Key Results

ICMR:
-0.34V ≤ V_ICM ≤ 0.36V  

OCMR:
-0.36V ≤ V_OCM ≤ 0.9V  

Linear range:
|V_id| ≤ 0.68V  

---

## Transient Analysis

Case 1 (100mV):
- Linear behavior  
- Clean sinusoidal output  

Case 2 (600mV):
- Distortion present  
- One transistor turns OFF  

---

## Gain

Simulated:
A_v ≈ 6.04 (15.62 dB)  

Theoretical:
A_v ≈ 4.5 (≈13 dB)  

Difference caused by:
- Channel length modulation  
- Non-ideal device effects  
- Parasitic components  

---

## DC Analysis
DC Analysis:
<img width="1785" height="810" alt="image" src="https://github.com/user-attachments/assets/9b6d9a2f-2082-47a9-9059-5d918d20918c" />

- Midband gain ≈ 9.87 dB  
- Bandwidth ≈ 4.8 MHz  
- UGB ≈ 29 MHz  
The DC operating point confirms that the output voltage and source voltage is near the designed bias value, ensuring proper saturation operation.

---

### 1.2.f Input Common Mode Range (ICMR)

The input common-mode range is defined as the range of input voltage for which all transistors remain in saturation.

### Minimum Input Common Mode Voltage

For proper operation, the tail current source must remain active and the NMOS transistors must stay in saturation.

Condition:

$$
V_{GS} \ge V_T
$$

Using:

$$
V_{GS} = V_{ICM} - V_S
$$

So,

$$
V_{ICM(min)} = V_S + V_T
$$

Substituting values:

$$
V_S = -0.7V, \quad V_T = 0.36V
$$

$$
V_{ICM(min)} = -0.7 + 0.36
$$

$$
V_{ICM(min)} = -0.34V
$$

### Maximum Input Common Mode Voltage

For maximum input voltage, the NMOS transistors must remain in saturation.

Condition:

$$
V_{DS} \ge V_{OV}
$$

Using:

$$
V_D = 0V, \quad V_S = -0.7V
$$

$$
V_{DS} = V_D - V_S = 0 - (-0.7) = 0.7V
$$

Now,

$$
V_{ICM(max)} = V_D + V_T
$$

Substituting:

$$
V_{ICM(max)} = 0 + 0.36
$$

$$
V_{ICM(max)} = 0.36V
$$

### Final Input Common Mode Range

$$
-0.34V \le V_{ICM} \le 0.36V
$$

##

### 1.2.g Output Common Mode Range

The output common-mode voltage range is determined by ensuring that the NMOS transistors remain in saturation and the circuit operates properly.

### Maximum Output Voltage

The maximum output voltage occurs when the drain voltage is at its highest possible value, which is limited by the supply voltage:

$$
V_{OCM(max)} \le V_{DD}
$$

However, to maintain current flow through the load resistor:

$$
V_{OCM(max)} = V_{DD}
$$

$$
V_{OCM(max)} = 0.9V
$$

### Minimum Output Voltage

For proper operation, the NMOS transistors must remain in saturation:

$$
V_{DS} \ge V_{OV}
$$

Using:

$$
V_{DS} = V_D - V_S
$$

At the edge of saturation:

$$
V_D - V_S = V_{OV}
$$

So,

$$
V_D = V_S + V_{OV}
$$

Since:

$$
V_D = V_{OCM(min)}
$$

$$
V_{OCM(min)} = V_S + V_{OV}
$$

### Substituting Values

$$
V_S = -0.7V, \quad V_{OV} = 0.34V
$$

$$
V_{OCM(min)} = -0.7 + 0.34
$$

$$
V_{OCM(min)} = -0.36V
$$

### Final Output Common Mode Range

$$
-0.36V \le V_{OCM} \le 0.9V
$$

##
---
## 1.3 Transient Analysis and Linearity Observation

The linear behavior of the differential amplifier is verified using transient analysis.

### Condition for Linearity

$$
|V_{id}| < \sqrt{2} V_{OV}
$$

$$
\sqrt{2} V_{OV} = 1.414 \times 0.34 = 0.48V
$$

### Case 1: Linear Region

Input applied:

$$
V_{id} = 100mV < 0.48V
$$

<img width="1916" height="849" alt="image" src="https://github.com/user-attachments/assets/5aee6e4f-5178-4b4b-bce0-e774338e362f" />
Observation:

- Output waveform is sinusoidal
- No distortion observed
- Both transistors operate in saturation
- Amplifier behaves linearly

### Case 2: Non-Linear Region

Input applied:

$$
V_{id} = 600mV > 0.48V
$$

<img width="1919" height="847" alt="image" src="https://github.com/user-attachments/assets/cac11637-fa5a-434c-8b67-cbd5b71ddf0a" />


Observation:

- Output waveform shows distortion
- Clipping observed
- One transistor enters cutoff region
- Linear amplification is lost

##

The behavior of the differential amplifier is analyzed for two cases based on the input differential voltage.

### Comparison Table

| Parameter | Case 1: Linear Region | Case 2: Non-Linear Region |
|----------|----------------------|--------------------------|
| Condition | $V_{id} < \sqrt{2}V_{OV}$ | $V_{id} > \sqrt{2}V_{OV}$ |
| Input ($V_{id}$) | 100 mV | 600 mV |
| Output waveform | Sinusoidal | Distorted / Clipped |
| Gain | Constant | Reduced / Non-linear |
| Transistor operation | Both in saturation | One enters cutoff |
| Current distribution | Equal sharing | Current shifts to one transistor |

## 1.4 AC Analysis


In AC analysis, the frequency response of the differential amplifier is evaluated to understand how gain varies with frequency.

The midband gain is identified from the flat portion of the Bode plot where the gain remains nearly constant.  
The bandwidth is determined as the frequency range between the lower cutoff frequency ($f_L$) and upper cutoff frequency ($f_H$), measured at the −3 dB points from the midband gain.

##

### Midband Gain:

From the AC simulation:

$$
A_v = 9.871 \text{ dB}
$$

The −3 dB level is:

$$
A_v - 3 = 9.871 - 3
$$

$$
A_v - 3 = 6.871 \text{ dB}
$$

##

### Cutoff Frequencies

Lower cutoff frequency:

$$
f_L = 0
$$

Upper cutoff frequency:

$$
f_H = 4.819 \text{ MHz}
$$

##

### Bandwidth

Bandwidth is calculated as:

$$
BW = f_H - f_L
$$

$$
BW = 4.819 - 0
$$

$$
BW = 4.819 \text{ MHz}
$$

---

## 1.5 Unity Gain Bandwidth (UGB)

Since the gain does not cross 0 dB within the plotted range, the unity gain bandwidth cannot be directly extracted.

Therefore, it is approximated using:

$$
UGB = A_v \times BW
$$

Using linear gain:

$$
A_v = 6.04
$$

$$
UGB = 6.04 \times 4.819 \text{ MHz}
$$

$$
UGB \approx 29.1 \text{ MHz}
$$

---

### Note

The theoretical analysis is based on first-order approximations assuming ideal MOSFET operation in saturation. It ignores higher-order effects such as channel length modulation, mobility reduction, and parasitic capacitances.

In contrast, simulation incorporates these non-ideal effects, which leads to differences between calculated and observed results.

---

## Comparison of Results

| Parameter | Theoretical | Simulated |
|------------|-------------|-----------|
| Voltage Gain ($A_v$) | 4.5 V/V | 6.04 V/V |
| Gain (dB) | 14.46 dB | 15.62 dB |

The variation between theoretical and simulated gain is mainly due to simplified assumptions in calculations and the inclusion of real device effects like channel length modulation, mobility degradation, and parasitic elements in simulation.

---

## Inference

The MOS differential amplifier with resistive load was successfully implemented and analyzed while meeting all specified design requirements:

Power consumption ≤ 1.8mW  
VDD = 0.9V  
VSS = -0.9V  
Output common-mode voltage = 0V  

The tail current was selected as 1mA to fully utilize the power budget. Under balanced conditions, the current divides equally between the two transistors:

$$
I_{D1} = I_{D2} = 0.5mA
$$

The operating point was chosen such that both NMOS transistors remain in saturation, ensuring proper amplification. The source node voltage was adjusted to:

$$
V_S \approx -0.7V
$$

by fine-tuning the transistor width during simulation.

Theoretical and simulated values show good agreement:

- Theoretical gain ≈ 5.29 V/V (14.46 dB)  
- Simulated gain ≈ 6.04 V/V (15.62 dB)  
- Bandwidth ≈ 4.819 MHz  
- Unity gain bandwidth ≈ 29.1 MHz  

The small difference between theoretical and simulated results is due to second-order effects such as channel length modulation, reduced mobility, and parasitic capacitances present in real MOSFET models. Additionally, theoretical calculations assume ideal behavior and ignore finite output resistance.

From the AC response, the amplifier shows a constant gain in the mid-frequency region followed by a decline at higher frequencies due to parasitic capacitances, which introduce a dominant pole and limit the bandwidth.

The amplifier performs linear amplification for small differential inputs. However, when the input exceeds the allowable range, non-linear effects appear, leading to distortion.

Overall, the designed differential amplifier meets the required specifications and demonstrates proper biasing, expected gain, and acceptable frequency response.

## Inference

The circuit meets the design requirements and operates correctly as a differential amplifier. It provides moderate gain and stable performance for small input signals.

---

# Circuit 2: Differential Amplifier with PMOS Active Load
circuit diagram:
<img width="1257" height="876" alt="image" src="https://github.com/user-attachments/assets/a685a418-769b-4fac-9af5-3fdcac4996c9" />
## Working Principle

In this configuration, resistors are replaced by a PMOS current mirror load, and an NMOS transistor acts as a current source.

- M5 → provides tail current  
- M3, M4 → form active load  

This increases output resistance and ideally improves gain.

---
## 2.2 Design Calculations

### GIVEN PARAMETERS

- Technology: TSMC 180nm  
- Supply voltage, $V_{DD} = +0.9V$  
- Negative supply, $V_{SS} = -0.9V$  
- Power limit, $P \leq 1.8mW$  
- Channel length, $L_n = 480nm$  
- Input common-mode voltage, $V_{in,CM} = 0V$  
- Output common-mode voltage, $V_{O,CM} = 0V$  
- Tail node voltage, $V_p = -0.7V$  
- Load capacitance, $C_L = 10pF$  
- Threshold voltage, $V_T \approx 0.36V$  

---

### 2.2.a Power Constraint

The total power consumed by the circuit is expressed as:

$$
P = (V_{DD} - V_{SS}) \cdot I_{SS}
$$

Total supply voltage:

$$
V_{DD} - V_{SS} = 0.9 - (-0.9) = 1.8V
$$

Given power limit:

$$
P \leq 1.8 \times 10^{-3}
$$

$$
1.8 \cdot I_{SS} \leq 1.8 \times 10^{-3}
$$

$$
I_{SS} \leq 1mA
$$

To utilize the maximum allowable power and enhance transconductance, we select:

$$
I_{SS} = 1mA
$$

Power consumed:

$$
P = 1.8 \times 1mA = 1.8mW
$$

Thus, the design operates within the specified power limit.

Here, transistor M5 acts as the tail current source supplying $I_{SS}$.

---

### 2.2.b Drain Current Calculation

When both inputs are equal:

$$
V_{in1} = V_{in2}
$$

the circuit is perfectly balanced, and the tail current divides equally:

$$
I_{D1} = I_{D2} = \frac{I_{SS}}{2}
$$

Substituting:

$$
I_{D1} = I_{D2} = \frac{1mA}{2} = 0.5mA
$$

Each transistor therefore conducts equal current under zero differential input.

---

### 2.2.c Bias Point Calculation

#### NMOS Differential Pair (M1 and M2)

Given:

$$
V_{in,CM} = 0V
$$

So,

$$
V_{G1} = V_{G2} = 0V
$$

#### Source Voltage

From design:

$$
V_S = V_p = -0.7V
$$

#### Gate-Source Voltage

$$
V_{GS} = V_G - V_S
$$

$$
V_{GS} = 0 - (-0.7) = 0.7V
$$

#### Overdrive Voltage

$$
V_{OV} = V_{GS} - V_T
$$

$$
V_{OV} = 0.7 - 0.36 = 0.34V
$$

#### Drain Voltage

$$
V_D = 0V
$$

#### Drain-Source Voltage

$$
V_{DS} = V_D - V_S
$$

$$
V_{DS} = 0 - (-0.7) = 0.7V
$$

#### Saturation Check

$$
V_{DS} > V_{OV}
$$

$$
0.7 > 0.34
$$

Hence, both M1 and M2 operate in saturation.

---

### NMOS Current Source (M5)

For M5:

- Source:

$$
V_S = V_{SS} = -0.9V
$$

- Drain:

$$
V_D = V_p = -0.7V
$$

#### Drain-Source Voltage

$$
V_{DS} = V_D - V_S = -0.7 - (-0.9) = 0.2V
$$

#### Saturation Requirement

$$
V_{DS} \geq V_{OV}
$$

Thus:

$$
0.2V \geq V_{OV}
$$

#### Selecting Overdrive Voltage

To maintain saturation:

$$
V_{OV} \approx 0.2V
$$

#### Gate-Source Voltage

$$
V_{GS} = V_T + V_{OV}
$$

$$
V_{GS} = 0.36 + 0.2 = 0.56V
$$

#### Gate Voltage

$$
V_G = V_S + V_{GS}
$$

$$
V_G = -0.9 + 0.56 = -0.34V
$$

#### Verification

$$
0.2 \geq 0.2
$$

Thus, M5 operates at the edge of saturation and delivers the required current.

---

### PMOS Active Load (M3 and M4)

For PMOS devices:

- Source:

$$
V_S = V_{DD} = 0.9V
$$

- Drain:

$$
V_D = 0V
$$

#### Source-Drain Voltage

$$
V_{SD} = V_S - V_D = 0.9 - 0 = 0.9V
$$

#### Saturation Condition

$$
V_{SD} > V_{OV}
$$

Since $0.9V$ is sufficiently large, both M3 and M4 remain in saturation.

---

### Final Bias Summary

All transistors (M1–M5) operate in saturation, ensuring correct differential amplifier functionality.

---

### 2.2.d Width Calculation

The MOSFET current equation in saturation:

$$
I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{OV})^2
$$

Rearranging:

$$
W = \frac{2 I_D L}{\mu_n C_{ox} (V_{OV})^2}
$$

---

### NMOS Differential Pair (M1 and M2)

Substituting:

$$
I_D = 0.5mA,\quad V_{OV} = 0.34V,\quad L = 480nm
$$

$$
\mu_n C_{ox} = 2.365 \times 10^{-4}
$$

$$
W = \frac{2 \times 0.5 \times 10^{-3} \times 480 \times 10^{-9}}{2.365 \times 10^{-4} \times (0.34)^2}
$$

$$
W \approx 17.56 \mu m
$$

Final:

$$
W_{M1} = W_{M2} \approx 17.6 \mu m
$$

---

### NMOS Current Source (M5)

Given:

$$
I_D = 1mA,\quad V_{OV} = 0.2V
$$

$$
W = \frac{2 \times 1 \times 10^{-3} \times 480 \times 10^{-9}}{2.365 \times 10^{-4} \times (0.2)^2}
$$

$$
W \approx 101.5 \mu m
$$

---

### Width Optimization

To meet exact biasing conditions such as:

$$
V_p \approx -0.7V,\quad I_{SS} \approx 1mA
$$

the widths were fine-tuned in simulation.

Updated values:

$$
W_{M1} = W_{M2}: 17.56\mu m \rightarrow 29.852\mu m
$$

$$
W_{M5}: 101.5\mu m \rightarrow 195.85\mu m
$$

This adjustment compensates for non-ideal device behavior and ensures accurate operating conditions.
## Design Summary

Tail current:
I_SS = 1mA  

Current split:
I_D1 = I_D2 = 0.5mA  

Bias conditions:
- V_S ≈ -0.7V  
- V_GS ≈ 0.7V  
- V_OV ≈ 0.34V  

For M5:
- V_DS = 0.2V  
- Operates near saturation boundary  

Widths adjusted:
- M1, M2 ≈ 29.85µm  
- M5 ≈ 195.85µm  

---

## Key Results

ICMR:
-0.34V ≤ V_ICM ≤ 0.39V  

OCMR:
-0.36V ≤ V_out ≤ 0.65V  

Linear range:
|V_id| ≤ 0.5V  

---

## Transient Analysis

Case 1 (100mV):
- Linear response  
- No distortion  

Case 2 (600mV):
- Output clipping  
- One transistor OFF  

---

## Gain

Simulated:
A_v ≈ 1.81 (5.15 dB)  

Theoretical:
A_v ≈ 41.7 (32.4 dB)  

---

## Reason for Large Deviation

- Non-ideal current source behavior  
- Finite output resistance of active load  
- Channel length modulation  
- Mobility degradation  
- Parasitic capacitances  

---

## AC Analysis

- Gain ≈ 5.2 dB  
- Bandwidth ≈ 2.2 GHz  
- UGB ≈ 8.7 GHz  

---
## DC Analysis

<img width="1682" height="726" alt="image" src="https://github.com/user-attachments/assets/4daa2a65-e68a-4541-a6a8-6a7a7f309c50" />

The DC simulation verifies that the node voltages closely match the intended bias values. This confirms that the transistors are correctly biased and operating in the saturation region as required for proper differential amplification.

---

### 2.2.e Input Common Mode Range (ICMR)

The input common-mode range specifies the allowable range of input voltage over which all transistors in the circuit remain in saturation.

### Minimum Input Common Mode Voltage

To ensure correct operation:
- NMOS transistors (M1, M2) must remain ON  
- Tail current source (M5) must stay in saturation  

Condition:

$$
V_{GS1} \ge V_T
$$

Since:

$$
V_{GS1} = V_{ICM} - V_S
$$

we get:

$$
V_{ICM(min)} = V_S + V_T
$$

Substituting:

$$
V_S = -0.7V,\quad V_T = 0.36V
$$

$$
V_{ICM(min)} = -0.7 + 0.36 = -0.34V
$$

---

### Maximum Input Common Mode Voltage

For the upper limit, PMOS load transistors must remain in saturation.

Condition:

$$
V_{SD} \ge V_{OVp}
$$

Using:

$$
V_{SD} = V_{DD} - V_D
$$

At the boundary:

$$
V_{SD} = V_{SG} - |V_{TP}|
$$

Also:

$$
V_{SG} = V_{DD} - V_{ICM}
$$

Rearranging:

$$
V_{ICM(max)} = V_D + |V_{TP}|
$$

Substituting:

$$
V_D \approx 0V,\quad |V_{TP}| \approx 0.39V
$$

$$
V_{ICM(max)} = 0.39V
$$

---

### Final ICMR

$$
-0.34V \le V_{ICM} \le 0.39V
$$

---

### 2.2.f Output Common Mode Range (OCMR)

The output common-mode range defines the allowable output voltage range while keeping all transistors in saturation.

### Minimum Output Voltage

To maintain saturation of NMOS devices:

$$
V_{DS1} \ge V_{OV}
$$

Using:

$$
V_{DS1} = V_{out} - V_S
$$

Thus:

$$
V_{out(min)} \ge V_S + V_{OV}
$$

Substituting:

$$
V_S = -0.7V,\quad V_{OV} = 0.34V
$$

$$
V_{out(min)} = -0.7 + 0.34 = -0.36V
$$

---

### Maximum Output Voltage

For PMOS transistors to remain in saturation:

$$
V_{SD} \ge V_{OVp}
$$

Using:

$$
V_{SD} = V_{DD} - V_{out}
$$

Thus:

$$
V_{out(max)} \le V_{DD} - V_{OVp}
$$

Substituting:

$$
V_{DD} = 0.9V,\quad V_{OVp} \approx 0.25V
$$

$$
V_{out(max)} = 0.65V
$$

---

### Final OCMR

$$
-0.36V \le V_{out} \le 0.65V
$$

---

### 2.2.g Differential Input Voltage Range (Linear Region)

The amplifier operates linearly only when both transistors conduct simultaneously and remain in saturation.

The differential input is:

$$
v_{id} = v_{in1} - v_{in2}
$$

### Linear Operation Condition

For linear behavior:
- Both M1 and M2 must be ON  
- Tail current must be shared  

### Maximum Differential Input

At the edge of linearity:

$$
v_{id(max)} = 2V_{OV}
$$

Substituting:

$$
V_{OV} = 0.25V
$$

$$
v_{id(max)} = 0.5V
$$

---

### Final Differential Range

$$
-0.5V \le v_{id} \le 0.5V
$$

---

## 2.3 Transient Analysis and Linearity Observation

Transient analysis is used to study how the amplifier responds to time-varying input signals and to verify its linear operation.

### Condition for Linearity

$$
|V_{id}| < \sqrt{2} V_{OV}
$$

Using:

$$
V_{OV} = 0.24V
$$

$$
\sqrt{2} V_{OV} = 1.414 \times 0.24 = 0.34V
$$

---

### Case 1: Linear Operation
<img width="1919" height="850" alt="image" src="https://github.com/user-attachments/assets/0657f47e-8f42-4ce2-bf88-85c504ffd9e9" />
Applied input:

$$
V_{id} = 80mV < 0.34V
$$

Observation:

- Output waveform is smooth and sinusoidal  
- No visible distortion  
- Both transistors conduct simultaneously  
- Amplifier operates in linear region

- ### Case 2: Non-Linear Region

Input applied:

$$
V_{id} = 600mV > 0.34V
$$
<img width="1919" height="846" alt="image" src="https://github.com/user-attachments/assets/1a4b077a-fbd1-45e9-8b94-e7bc1491c278" />

Observation:

- Output waveform is smooth and sinusoidal  
- No visible distortion  
- Both transistors conduct simultaneously  
- Amplifier operates in linear region


  ## Theoretical vs. Simulated Amplifier Gain

<img width="1919" height="424" alt="image" src="https://github.com/user-attachments/assets/f6187168-15b2-4d75-88dc-3049c125ae68" />

The output waveform is inverted and amplified relative to the differential input.

---

### Simulated Gain Analysis:

<img width="1919" height="424" alt="image" src="https://github.com/user-attachments/assets/f6187168-15b2-4d75-88dc-3049c125ae68" />


**Input Parameters:**

- Signal Type: Sinusoidal  
- Frequency: 1 kHz  
- Differential Amplitude: 50 mV  
- DC Offset: 0 V

**Measured Peak-to-Peak Voltages:**

$$
V_{in(pp)} = 50mV - (-50mV) = 100mV
$$

$$
V_{out(pp)} = 106mV - (-75mV) = 181mV
$$

**Voltage Gain:**

$$
A_v = \frac{V_{out(pp)}}{V_{in(pp)}} = \frac{181mV}{100mV} \approx 1.81
$$

**Gain in Decibels:**

$$
A_v(dB) = 20 \log_{10}(1.81) \approx 5.15 \, dB
$$

---

### Theoretical Gain Calculation

**Assuming Channel Length Modulation:**

$$
\lambda = 0.1 \, V^{-1}
$$

**MOSFET Output Resistance:**

$$
r_o = \frac{1}{\lambda I_D} = \frac{1}{0.1 \cdot 0.5mA} = 20 k\Omega
$$

**Effective Output Resistance (NMOS || PMOS):**

$$
r_{o,eff} = r_{o_n} \parallel r_{o_p} = 20k \parallel 20k = 10 k\Omega
$$

**Transconductance:**

$$
g_m = \frac{2 I_D}{V_{OV}} = \frac{2 \cdot 0.5mA}{0.24V} \approx 4.17 mS
$$

**Differential Gain:**

$$
A_d = g_m \cdot R_{out} = 4.17 mS \cdot 10 k\Omega \approx 41.7
$$

**Gain in dB:**

$$
A_d(dB) = 20 \log_{10}(41.7) \approx 32.4 dB
$$

---

### Causes of Gain Discrepancy

Theoretical gain is higher than simulated gain due to multiple non-idealities and modeling assumptions:

1. **Channel Length Modulation**  
   Real MOSFETs have bias-dependent $\lambda$, affecting $r_o$ and lowering gain.

2. **Finite Output Resistance of Active Load**  
   PMOS loads provide limited $R_{out}$; variations reduce the actual gain.

3. **Mobility Reduction and Short-Channel Effects**  
   Carrier mobility decreases at high fields, lowering effective $g_m$.

4. **Variations in Overdrive Voltage ($V_{OV}$)**  
   Small shifts in operating point reduce transconductance in simulation.

5. **Non-Ideal Tail Current Source (M5)**  
   Finite output resistance and current mismatch slightly degrade gain.

6. **Parasitic Capacitances**  
   Internal MOSFET capacitances attenuate signals, particularly at higher frequencies.

7. **Measurement Approximation**  
   Simulated gain is derived from waveform peaks, which may introduce small errors.

   ## AC Frequency Response Analysis

<img width="1919" height="424" alt="image" src="https://github.com/user-attachments/assets/f47f5271-1043-488f-bd8b-5eed0e001ff9" />

The AC analysis evaluates the frequency response of the differential amplifier.  
The **midband gain** is taken from the flat portion of the Bode plot, while the **bandwidth** is defined as the range between the lower ($f_L$) and upper ($f_H$) cutoff frequencies at the −3 dB points.

---

### Midband Gain

From simulation results:

$$
A_v = 5.2 \, \text{dB}
$$

-3 dB point:

$$
A_v - 3 = 5.2 - 3 = 2.2 \, \text{dB}
$$

---

### Cutoff Frequencies

**Lower cutoff:**

$$
f_L = 0
$$

**Upper cutoff:**

$$
f_H = 2.2 \, \text{GHz}
$$

---

### Bandwidth

The bandwidth is:

$$
BW = f_H - f_L = 2.2 - 0 = 2.2 \, \text{GHz}
$$

---

## Unity Gain Bandwidth (UGB)

The 0 dB frequency is approximately:

$$
f_{0dB} \approx 4.8 \, \text{GHz}
$$

Using linear gain:

$$
A_v = 1.81
$$

$$
UGB = A_v \cdot f_H = 1.81 \cdot 4.8 \, \text{GHz} \approx 8.69 \, \text{GHz}
$$

---

### Note

Theoretical first-order analysis assumes ideal MOSFET behavior in saturation and ignores:

- Channel length modulation  
- Mobility reduction  
- Non-ideal current sources  
- Parasitic capacitances  

Simulation includes these effects, causing deviations between theory and simulation.

---

## Comparison of Theoretical and Simulated Gain

| Parameter | Theoretical | Simulated |
|-----------|------------|-----------|
| Voltage Gain ($A_v$) | 41.7 V/V | 1.81 V/V |
| Gain (dB) | 32.4 dB | 5.15 dB |

**Observation:** The lower simulated gain is mainly due to non-ideal MOSFET effects and finite output resistance of the active load and current source.

---

## Summary and Inference

The designed MOS differential amplifier with PMOS active load and NMOS current source meets design constraints:

- Power ≤ 1.8 mW  
- $V_{DD} = 0.9$ V  
- $V_{SS} = -0.9$ V  
- $V_{OCM} = 0$ V  

**Tail Current:**

$$
I_{tail} \approx 1 \, \text{mA}, \quad I_{D1} = I_{D2} \approx 0.5 \, \text{mA}
$$

All transistors (M1–M5) are biased in **saturation**, with tail node voltage:

$$
V_S \approx -0.7 \, \text{V}
$$

The amplifier exhibits a flat midband response, and bandwidth is primarily limited by parasitic capacitances and non-ideal transistor effects.
## Inference

Even though the theoretical gain is high, real device limitations significantly reduce it. However, the circuit achieves a much higher bandwidth compared to the resistive load case.

---

# Overall Conclusion

- Resistive load amplifier:
  - Moderate gain  
  - Predictable performance  

- Active load amplifier:
  - High theoretical gain  
  - Practical gain reduced due to non-idealities  
  - Improved bandwidth  

Differential amplifiers behave linearly only for small input signals. For larger inputs, non-linear effects occur due to current steering.

This experiment highlights the importance of considering practical device effects in analog circuit design.
