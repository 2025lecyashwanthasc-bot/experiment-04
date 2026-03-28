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

## AC Analysis

- Midband gain ≈ 9.87 dB  
- Bandwidth ≈ 4.8 MHz  
- UGB ≈ 29 MHz  

---

## Inference

The circuit meets the design requirements and operates correctly as a differential amplifier. It provides moderate gain and stable performance for small input signals.

---

# Circuit 2: Differential Amplifier with PMOS Active Load

## Working Principle

In this configuration, resistors are replaced by a PMOS current mirror load, and an NMOS transistor acts as a current source.

- M5 → provides tail current  
- M3, M4 → form active load  

This increases output resistance and ideally improves gain.

---

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
