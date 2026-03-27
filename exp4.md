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
