# Differential Amplifier Analysis

## Aim
To design and simulate three MOSFET differential amplifier configurations using LTspice by performing DC, Transient, and AC analyses, and to compare their performance based on gain, bandwidth, and power efficiency.

## Theory
A differential amplifier amplifies the difference between two input signals while rejecting any signal that is common to both inputs. This property is known as common-mode rejection and is an important feature in analog circuit design.
The differential input voltage is given by:
$$
v_{id} = v_{in1} - v_{in2}
$$
 The differential gain of the amplifier is given by:

$$
A_v = g_m R_{out}
$$
$$
g_m = \frac{2 I_D}{V_{ov}}
$$

where $I_D$ is the drain current and $V_{ov}$ is the overdrive voltage.

For larger differential inputs:
$$
v_{id} > \sqrt{2} V_{ov}
$$
## Circuit 1: Differential Amplifier 
## Given parameters  
| Parameter                 | Value       |
| ------------------------- | ----------- |
| Technology                | TSMC 180 nm |
| ( V_{DD} )                | +0.9 V      |
| ( V_{SS} )                | −0.9 V      |
| Power Limit               | ≤ 1.8 mW    |
| ( L_n )                   | 480 nm      |
| ( V_{in,CM} )             | 0 V         |
| ( V_{out,CM} )            | 0 V         |
| Tail Voltage ( V_p )      | −0.7 V      |
| Load Capacitance ( C_L )  | 10 pF       |
| Threshold Voltage ( V_T ) | ≈ 0.36 V    |
circuit diagram:

<img width="851" height="730" alt="image" src="https://github.com/user-attachments/assets/99184e31-48c6-48c8-b16c-e395946b2adb" />


###  Power Constraint
$$
P = (V_{DD} - V_{SS}) \cdot I_{SS}
$$

$$
V_{DD} - V_{SS} = 0.9 - (-0.9) = 1.8V
$$

Since the maximum allowed power is 1.8mW,

$$
P \leq 1.8 \times 10^{-3}
$$

$$
(V_{DD} - V_{SS}) \cdot I_{SS} \leq 1.8 \times 10^{-3}
$$

$$
1.8 \cdot I_{SS} \leq 1.8 \times 10^{-3}
$$

$$
I_{SS} \leq 1mA
$$

we choose:

$$
I_{SS} = 1mA
$$
###  Drain Current Calculation
$$
I_{D1} = I_{D2} = \frac{I_{SS}}{2}
$$
$$
I_{D1} = I_{D2} = \frac{1mA}{2}
$$

$$
I_{D1} = I_{D2} = 0.5mA
$$
Rd calculation 
$$
V_{OCM} = 0V
$$

So,

$$
V_{out1} = V_{out2} = 0V
$$

The output voltage is given by:

$$
V_{out} = V_{DD} - I_D R_D
$$
$$
I_D R_D = 0.9
$$

$$
R_D = \frac{0.9}{0.5 \times 10^{-3}}
$$

$$
R_D = 1.8k\Omega
$$
Overdrive voltage 

$$
V_{OV} = V_{GS} - V_T
$$

$$
V_{OV} = 0.7 - 0.36
$$

$$
V_{OV} = 0.34V
$$
$$
W = \frac{2 \times 0.5 \times 10^{-3} \times 480 \times 10^{-9}}{2.365 \times 10^{-4} \times (0.34)^2}
$$

$$
W \approx 17.48 \mu m
$$
Final width obtained to Id of the MOSFET :

$$
W \approx 30.475 \mu m
$$
## DC Analysis

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/19503614-100e-4873-9d3c-e03f64532f28" />


###  Input Common Mode Range (ICMR)
  Mainimum Input Common Mode Voltage
$$
V_{ICM(min)} = V_S + V_T
$$
$$
V_{ICM(min)} = -0.7 + 0.36 = -0.34V
$$
Maximum Input Common Mode Voltage

$$
V_{ICM(max)} = V_D + V_T = 0+0.36
$$
$$
V_{ICM(max)} = 0.36V
$$
### Maximum Output Voltage

The maximum output voltage occuring  is limited by the supply voltage:
$$
V_{OCM(max)} = V_{DD}
$$

$$
V_{OCM(max)} = 0.9V
$$

 Minimum Output Voltage
 $$
V_{DS} = V_D - V_S = V(ov)
$$




$$
V_D = V_S + V_{OV}
$$

As $$
V_D = V_{OCM(min)}
$$

$$
V_{OCM(min)} = V_S + V_{OV}
$$

$$
V_S = -0.7V, \quad V_{OV} = 0.34V
$$

$$
V_{OCM(min)} = -0.7 + 0.34 =-.36V
$$
 ## Vid calculation in linear region 
$$
|V_{id}| \le 2V_{OV}
$$ 
$$
|V_{id}| \le 2 \times 0.34  =   0.68V
$$
##  Transient Analysis and Linearity Observation
### In  Linear Region

$$
V_{id} = 100mV < 0.48V
$$
<img width="1916" height="417" alt="Screenshot 2026-03-27 223036" src="https://github.com/user-attachments/assets/ed9491c6-c0bc-491a-aa3a-5329c92bb2e8" />

Shows sinusoidal out wave form with constant gain 
### Case 2: Non-Linear Region

Input applied:

$$
V_{id} = 600mV > 0.48V
$$
<img width="1260" height="282" alt="image" src="https://github.com/user-attachments/assets/50bd48ff-280a-4de5-84ce-0c2c34574219" />
Distored output wave form with reduced gain
### Theoretical Gain

$$
r_o = \frac{1}{\lambda I_D}
$$
$$
r_o = \frac{1}{0.1 \times 0.5 \times 10^{-3}}
$$

$$
r_o = 20k\Omega
$$
$$
r_{o,eff} = 20k \parallel 20k
$$

$$
r_{o,eff} = 10k\Omega
$$
$$
A_d = g_m R_{out}
$$
$$
A_d \approx 4.5
$$

## Circuit 2: Differential Amplifier with PMOS  and an NMOS current source
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/857dc34d-9c65-4b99-ae94-526794a162a6" />
#Power Constraint
$$
P = (V_{DD} - V_{SS}) \cdot I_{SS}
$$
$$
P \leq 1.8 \times 10^{-3}
$$

$$
1.8 \cdot I_{SS} \leq 1.8 \times 10^{-3}
$$

$$
I_{SS} \leq 1mA
$$
$$
I_{D1} = I_{D2} = \frac{I_{SS}}{2}
$$


$$
I_{D1} = I_{D2} = \frac{1mA}{2}
$$

$$
I_{D1} = I_{D2} = 0.5mA
$$

Thus, each transistor carries equal current under zero differential input.
#overdrive voltage 
$$
V_{OV} = V_{GS} - V_T
$$

$$
V_{OV} = 0.7 - 0.36
$$

$$
V_{OV} = 0.34V
$$
$$
V_{DS} = V_D - V_S
$$
$$
V_{DS} = 0.7V
$$

$$
V_{DS} > V_{OV}
$$

$$
0.7 > 0.34
$$
so M1 and M2 is in saturation 
For PMOS:


$$
V_{DD} = 0.9V
$$

$$
V_D = 0V
$$
# Width Calculation
$$
I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{OV})^2
$$
$$
W = \frac{2 \times 0.5 \times 10^{-3} \times 480 \times 10^{-9}}{2.365 \times 10^{-4} \times (0.34)^2}
$$

$$
W = \frac{480 \times 10^{-12}}{2.365 \times 10^{-4} \times 0.1156}
$$

$$
W = \frac{480 \times 10^{-12}}{2.733 \times 10^{-5}}
$$

$$
W \approx 17.6 \mu m
$$
$$
W = \frac{2 \times 1 \times 10^{-3} \times 480 \times 10^{-9}}{2.365 \times 10^{-4} \times (0.2)^2}
$$

$$
W = \frac{960 \times 10^{-12}}{2.365 \times 10^{-4} \times 0.04}
$$

$$
W = \frac{960 \times 10^{-12}}{9.46 \times 10^{-6}}
$$

$$
W \approx 101.5 \mu m
$$
After altering the width was set to desired requirements 
final width is given by 
$$
W  : 17.56\mu m \rightarrow 27.569\mu m
$$

$$
W_{M5} : 101.5\mu m \rightarrow 103.45\mu m
$$
### Input Common Mode Voltage
$$
V_{ICM(min)} = V_S + V_T
$$
$$
V_{ICM(min)} = -0.7 + 0.36
$$

$$
V_{ICM(min)} = -0.34V
$$
$$
V_{ICM(max)} = V_D + |V_{TP}|
$$
$$
V_{ICM(max)} = 0.39V
$$
 Final Input Common Mode Range

$$
-0.34V \le V_{ICM} \le 0.39V
$$

# DC analysis :
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/0e46576c-84ed-4d4c-910b-4948aebeda13" />
## Output Common Mode Range (OCMR)
$$
V_{out(min)} - V_S \ge V_{OV}
$$

$$
V_{out(min)} \ge V_S + V_{OV}
$$
$$
V_{out(min)} = -0.7 + 0.34
$$

$$
V_{out(min)} = -0.36V
$$
### Maximum Output Common Mode Voltage
$$
V_{DD} - V_{out(max)} \ge V_{OVp}
$$

$$
V_{out(max)} \le V_{DD} - V_{OVp}
$$
$$
V_{out(max)} = 0.9 - 0.25 =0.65
$$
# Vout range 
$$
-0.36V \le V_{out} \le 0.65V
$$
# Differential Input Voltage Range (Linear Region)

$$
v_{id(max)} = 2V_{OV}
$$
$$
-0.5V \le v_{id} \le 0.5V
$$
condition for linearity 
$$
V_{id} = 0.1V < 0.34V
$$
<img width="1480" height="293" alt="image" src="https://github.com/user-attachments/assets/db89c1d9-5537-4a88-ab44-254985a438b9" />
condition for non- linearity 
$$
V_{id} = 500mV > 0.34V
$$
<img width="1433" height="284" alt="image" src="https://github.com/user-attachments/assets/66d9c1f7-8d56-4cab-86dd-769ade3fa9c4" />
## Theoretical  Gain

A_v = √[(μ_n × (W/L)_n) / (μ_p × (W/L)_p)]

Substiting 
μ_n = 273.809 × 10^-4
μ_p = 115.689 × 10^-4

(W/L)_n = 38.2 / 480×10^-9
(W/L)_p = 30.625 / 480×10^-9


A_v = √[(273.809 × 38.2) / (115.689 × 30.625)]
A_v = √(10462.9 / 3542.9)
A_v = √(2.95)
A_v ≈ 1.718 V/V

Gain in dB
A_v(dB) = 20 log(A_v)
A_v(dB) = 20 log(1.718)
A_v(dB) ≈ 4.70 dB
# Simulated gain
A_v = \frac{V_{out(p-p)}}{V_{in(p-p)}}



A_v = \frac{385 \times 10^{-3}}{10 \times 10^{-3}}

A_v = 38.5
$$
A_v(dB) = 20\log_{10}(38.5) =31.75db
$$
# AC analysis 
<img width="1132" height="223" alt="image" src="https://github.com/user-attachments/assets/86e3ba72-db42-4d1b-a193-998d5365cd77" />
Bandwidth = f{h} - f{l}
          = 2.5 Ghz- 0 
          = 2.5 GHz

## CMOS Differential Amplifier with PMOS Bias I.e bias controlled 
circuit diagram 
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/670c93f6-6788-495d-b644-14e15e046e41" />
Power Constraint

Total power:
$$
P = (V_{DD} - V_{SS}) \cdot I_{SS}
$$

$$
V_{DD} - V_{SS} = 1.8V
$$

$$
1.8 \cdot I_{SS} \leq 1.8 \times 10^{-3}
\Rightarrow I_{SS} \leq 1mA
$$
$$
I_{D1} = I_{D2} = \frac{I_{SS}}{2} = 0.5mA
$$
## NMOS Differential Pair (M1, M2)

| Parameter | Value |
|----------|------|
| \(V_G\) | 0 V |
| \(V_S\) | -0.7 V |
| \(V_D\) | 0 V |

$$
V_{GS} = 0.7V
$$

$$
V_{OV} = 0.34V
$$

$$
V_{DS} = 0.7V
$$

**Condition:**
$$
V_{DS} > V_{OV}
$$
PMOS Active Load (M3, M4)

| Parameter | Value |
|----------|------|
| \(V_S\) | 0.9 V |
| \(V_D\) | 0 V |

$$
V_{SD} = 0.9V
$$

### Saturation Requirement:
$$
V_{SD} \ge V_{SG} - |V_T|
$$

$$
V_G \ge -0.39V
$$

**Chosen bias:**
$$
V_{b2} = -0.36V
$$

$$
V_{SG} = 1.26V
$$

$$
V_{OV(p)} = 0.87V
$$

**Check:**
$$
0.9 > 0.87
$$
This verifies mosfet is in saturation region 

## PMOS Width Calculation (Wₚ)

### Given Parameters

- Drain Current:  
  \( I_D = 0.5 \, mA = 0.5 \times 10^{-3} \, A \)

- Channel Length:  
  \( L = 480 \, nm = 480 \times 10^{-9} \, m \)

- Process Parameter:  
  \( \mu_p C_{ox} = 9.98 \times 10^{-5} \)

- Overdrive Voltage:  
  \( V_{OV(p)} = 0.87 \, V \)

---

### Formula Used

\[
W_p = \frac{2 I_D L}{\mu_p C_{ox} \cdot V_{OV(p)}^2}
\]

---

### Substitution

\[
W_p = \frac{2 \times (0.5 \times 10^{-3}) \times (480 \times 10^{-9})}{9.98 \times 10^{-5} \times (0.87)^2}
\]

---

### Simplification

\[
W_p = \frac{480 \times 10^{-12}}{9.98 \times 10^{-5} \times 0.7569}
\]

\[
W_p = \frac{480 \times 10^{-12}}{7.55 \times 10^{-5}}
\]

---

### Final Result

\[
W_p \approx 6.35 \, \mu m
\]

---

### Conclusion

\[
W_3 = W_4 \approx 6.35 \, \mu m
\]
Adjusted width after altering 
\[
W_{M3} = W_{M4} : 6.35 \, \mu m \rightarrow 13.876 \, \mu m
\]
## DC Analysis 
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/29d0a8f0-07f2-4fa0-a6c0-6ce1376ec720" />
# Input Common Mode Range (ICMR)
\[
V_{ICM(min)} = V_S + V_T = -0.7 + 0.36 = -0.34 \, V
\]
At the edge of saturation:

\[
V_D - V_S = V_{OV}
\]

 Using MOS Relations

\[
V_{OV} = V_{GS} - V_T
\]

\[
V_{GS} = V_{ICM} - V_S
\]
\[
0.7 = (V_{ICM} + 0.7) - 0.36
\]

\[
0.7 = V_{ICM} + 0.34
\]
\[
V_{ICM(max)} = 0.36 \, V
\]

## Input Common Mode Range

\[
-0.34 \, V \leq V_{ICM} \leq 0.36 \, V
\]
# Differential Input Voltage Range

\[
v_{id} = v_{in1} - v_{in2}
\]
## Maximum Differential Input Voltage

<p align="center">

\[
v_{id(max)} = 2V_{OV}
\]

\[
= 2 \times 0.34 = 0.68 \, V
\]

</p>

---

## Differential Input Range

<p align="center">

\[
-0.68 \, V \leq v_{id} \leq 0.68 \, V
\]

</p>

## Transient Analysis 
# linear region 
<p align="center">

\[
v_{id} = 10\, mV < 0.48 \, V
\]

</p>
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/f44cfe82-cec4-4cba-bcb0-d2ca067bb120" />

# Non-Linear Region
\[
v_{id} = 500\, mV > 0.48 \, V
\]
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/3ead58cf-3fff-4c3d-9ad6-430011414820" />
# Simulateed Gain 

<p align="center">

\[
V_{in(p-p)} = 5\,mV - (-5\,mV) = 10\,mV
\]

\[
V_{out(p-p)} = 161\,mV - (-240\,mV) = 401\,mV
\]

\[
A_v = \frac{V_{out(p-p)}}{V_{in(p-p)}} = \frac{401 \times 10^{-3}}{10 \times 10^{-3}} = 40.1
\]

\[
A_v(dB) = 20\log_{10}(40.1) \approx 32.06 \, dB
\]

</p>

# Theoritical gain 
<p align="center">

\[
r_{o,eff} = r_{on} \parallel r_{op} = 18.5k \parallel 18.5k \approx 9.25 \, k\Omega
\]

\[
g_m = \frac{2I_D}{V_{OV}} = \frac{2 \times 0.54 \times 10^{-3}}{0.34} \approx 3.18 \, mS
\]

\[
A_v = g_m \cdot R_{out} = 3.18 \times 10^{-3} \times 9.25 \times 10^{3} \approx 29.4
\]

\[
A_v(dB) = 20\log_{10}(29.4) \approx 29.36 \, dB
\]

</p>

# AC analysis 
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/d7bad21d-d7ef-4827-8a6b-237d100bd5db" />

Midband gain:


<p align="center">

\[
A_v = 33 \, dB
\]

\[
A_v(-3dB) = 33 - 3 = 30 \, dB
\]
# Cuttoff Frequencies 
\[
f_L = 0 \, Hz
\]

\[
f_H = 442.90 \, MHz
\]
# Band width calculation 
\[
BW = f_H - f_L = 442.90 - 0 = 442.90 \, MHz
\]

</p>
