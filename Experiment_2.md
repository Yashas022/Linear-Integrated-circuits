# Experiment-2 CS amplifier with different configurations 
# Experiment 2A – CS Amplifier with Resistor Load

## Aim

To design and simulate a **Common Source (CS) amplifier** using:

- NMOS transistor (M1)
- PMOS active load (M2) instead of RD
- Source degeneration resistor (Rs)

in **TSMC 180nm technology** using **LTSpice**, with:

- Supply Voltage: **1.5V**
- Power constraint ≈ **0.5mW**
- Gate DC bias = **0.9V**

And to analyze:

- DC operating point  
- Saturation region verification  
- Transient response  
- Small-signal voltage gain  
- Bandwidth  
- Theoretical vs Practical comparison

  ##  Circuit Description

The circuit consists of:

- **M1 (NMOS)** → Amplifying transistor  
- **M2 (PMOS)** → Active load replacing RD  
- **Rs = 600Ω** → Source degeneration resistor  
- **VDD = 1.5V**  
- Input Signal: `SINE(0.9 10m 1k)`

### Why PMOS Active Load?

- Higher output resistance
- Higher gain compared to resistor load  
- Suitable for integrated circuit implementation  
- Better voltage swing control


## DC Analysis (Theoretical)
**For Nmos**
Choosen Overdrive Voltage

\[
V_{ov} ≈ 0.25V
\]

\[
V_{GS} = V_{TH} + V_{ov}
\]

\[
V_{GS} = 0.366 + 0.25
\]

\[
V_{GS} = 0.61V
\]

Calculating Vout and Rs

Vout = VDS + VRS
Vout = VDD/2 + 0.2  
Vout = 1.5/2 + 0.2  
Vout = 0.75 + 0.2  
Vout = 0.95V

VRS= IdRs
0.2= 0.3mARs
Rs=600 ohm  

**Gate_voltage**

Vg=Vgs+IdRs
  =0.61+0.2
Vg= 0.81V

**Verification for biasing in saturation region**

 Vds >= Vgs- Vth
 Vds>= 0.25V

 
  Hence it is in saturation region
**For PMOS**
Choosen Overdrive Voltage

\[
V_{ov} ≈ 0.25V
\]

\[
V_{GS} = V_{TH} + V_{ov}
\]

\[
V_{GS} = 0.39 + 0.25
\]

\[
V_{GS} = 0.64V
\]
Gate voltage 

Vsg= Vdd-Vg

Vg=1.5-.64

Vg=0.86V   

###  Width Calculation

Drain current in saturation:

$$
I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{OV})^2
$$

Rearranging:

$$
W = \frac{2 I_D L}{\mu_n C_{ox} (V_{OV})^2}
$$

### For NMOS

Initially, the calculated NMOS width came out to be approximately

$$
W_n = 7.49\mu m
$$

However, after running the simulation, the drain current was slightly lower than the intended 300µA. This happens because practical transistor models include second-order effects that slightly alter the expected current.

To correct this and achieve the desired operating current, I increased the width to:

$$
W_n = 1.108\mu m 
$$

 **To get the desired Id and Vout the width of both PMOS and NMOS are varied**
  
 ## Practical DC analysis 
 <img width="1600" height="1000" alt="image" src="https://github.com/user-attachments/assets/7a6e8258-8c81-4974-b119-8fa85d174db3" />


### Theoretical Gain

Assume channel length modulation:

$$
\lambda = 0.1V^{-1}
$$

Transconductance:

$$
g_m = \frac{2I_D}{V_{OV}}
$$

$$
g_m =2.67 \times 10^{-3} S
$$

Output resistance:

$$
r_o = \frac{1}{\lambda I_D}
$$

$$
r_o = 30k\Omega
$$


Voltage gain with source degeneration:

$$
A_v = \frac{g_m (r_{o1} || r_{o2})}{1 + g_m R_S}
$$

$$
A_v = 30.78
$$

Gain in dB:

$$
A_v(dB) = 20\log_{10}(15.38)
$$

$$
A_v(dB) = 29.76dB
$$
### Transient Analysis

<img width="1600" height="1000" alt="image" src="https://github.com/user-attachments/assets/ac0d9485-3200-4b5b-8493-0f6c851a7edc" />


### AC Analysis 
<img width="1267" height="391" alt="image" src="https://github.com/user-attachments/assets/0513a693-7809-4409-b6b2-53bdaf53c869" />

From the AC analysis, the midband gain of the amplifier is approximately 28 dB.

Midband Gain ≈ 28.4 dB
−3 dB Gain Level ≈ 25.4 dB

From the Bode plot, this occurs at:

f_H ≈ 37.66 MHz

This frequency represents the upper cutoff frequency of the amplifier.

Beyond this point, the gain starts decreasing rapidly due to internal MOSFET parasitic capacitances (Cgs, Cgd) which introduce dominant poles in the circuit.

Hence, the bandwidth of the amplifier is approximately:

Bandwidth ≈ 37.66 MHz

This confirms that the circuit behaves as a low-pass amplifier with a finite high-frequency limit determined by device parasitics.


  ##
  ##
  ### Experiment 2B – CS Amplifier with PMOS Active Load and NMOS Current Source

##  Aim

To design a Common Source (CS) amplifier using an NMOS transistor with NMOS Current Source and PMOS Active Load in 180nm TSMC technology in LTSpice with a supply voltage of 1.5V and power constraint less than or equal to 0.5mW, and to analyze its DC operating point, transient response, voltage gain, and bandwidth

### Source Degeneration Effect Using M3

Because M3 has finite output resistance, it introduces a degeneration effect in the source of M1.

The effective voltage gain becomes:

$$
A_v = \frac{-g_{m1} r_{o2}}{1 + g_{m1} r_{o3}}
$$

The denominator term:

$$
(1 + g_{m1} r_{o3})
$$

reduces the overall gain and acts similarly to classical source degeneration.

##

### Effects of NMOS Current Source Degeneration

- Improves bias stability  
- Reduces sensitivity to device variations  
- Enhances linearity  
- Increases operating point robustness  

However, the voltage gain is reduced due to the additional term in the denominator.

##

## Design Calculations

### GIVEN PARAMETERS

- Technology: TSMC 180nm
- Supply voltage, $V_{DD} = 1.5V$
- Power constraint ≤ 0.5mW
- Channel length, $L_n = 180nm$
- Threshold voltage, $V_T ≈ 0.366V$
- Electron mobility, $\mu_n = 273.81 \times 10^{-4} \ m^2/Vs$
- Load capacitor, $C_L = 10pF$
- Gate oxide thickness, $t_ox = 4.1 \times 10^{-9} \ m$

  
We can obsereve that all the circuit parameters will be same except 
The Vgs of the M2 is given by 

Vgs= Vov+Vtn
Vgs = .25+.366
Vgs= 0.61V 
 After setting the value of the Vgs the width of the NMOS is altered in such way the desired value Vout and Id value are obtained.
The obtained width of the NMOS W(m3) = 24.4um.

## DC Analysis
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/ef543fa7-7d9a-4ff0-8a08-05e58cdc49f6" />


### Transient Analysis

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/258814bb-f5f9-4d4e-9b61-79519456082a" />


### Simulated Gain

The input signal applied was:

- Type: Sine wave  
- Frequency = 1kHz  
- Amplitude = 10mV  
- DC Offset = 0.91V  

Measured peak-to-peak values:

$$
V_{in(p-p)} = 0.9095-0.8913 =0.0182 V
$$

$$
V_{out(p-p)} = 1.0656 - 1.0372V = 0.0284V
$$

Voltage gain is calculated as:

$$
A_v = \frac{V_{out(p-p)}}{V_{in(p-p)}}
$$

$$
A_v = \frac{0.0284}{0.0182}
$$

$$
A_v = 1.5604
$$

Gain in dB:

$$
A_v(dB) = 20 \log_{10}(A_v)
$$

$$
A_v(dB) = 20 \log_{10}(1.5604)
$$

$$
A_v(dB) = 3.8649 \text{ dB}
$$

$$
A_v = \frac{-g_{m1} r_{o2}}{1 + g_{m1} r_{o3}}
$$

This expression is obtained by assuming:

- $\lambda_1 = 0$ (output resistance of M1 neglected)
- All transistors operating in saturation

##

### Transconductance of M1

$$
g_{m1} = \frac{2 I_D}{V_{OV}}
$$

$$
g_{m1} = \frac{2 \times 300 \times 10^{-6}}{0.25}
$$

$$
g_{m1} = 2.4 \times 10^{-3} \ S
$$

##

### Output Resistances

$$
r_o = \frac{1}{\lambda I_D}
$$

For $\lambda = 0.1 \ V^{-1}$:

$$
r_{o2} = r_{o3} = \frac{1}{0.1 \times 300 \times 10^{-6}}
$$

$$
r_{o2} = r_{o3} = 33.33k\Omega
$$

##

### Gain Calculation

$$
A_v = \frac{-(2.4 \times 10^{-3}) \times 33.33 \times 10^3}
{1 + (2.4 \times 10^{-3}) \times 33.33 \times 10^3}
$$

$$
A_v = \frac{-80}{1 + 80}
$$

$$
A_v = \frac{-80}{81}
$$

$$
A_v \approx -0.99
$$

Magnitude:

$$
|A_v| \approx 0.99
$$

Gain in dB:

$$
A_v(dB) = 20 \log_{10}(0.99)
$$

$$
A_v(dB) \approx -0.08 \text{ dB}
$$

Thus, when $g_{m1} r_{o3}$ is large, the denominator significantly reduces the gain, explaining why Experiment B produces lower gain compared to Experiment A.

### 3.6 AC Analysis

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/e087b91e-bc22-4298-b815-366ae97b9c4c" />


In AC analysis, the frequency response of the Common Source amplifier is observed.

The midband gain is obtained from the flat region of the Bode plot.  
The bandwidth is defined as the frequency range between the lower cutoff frequency ($f_L$) and upper cutoff frequency ($f_H$), measured at the −3 dB points.

##

### Midband gain:

From AC simulation:

$$
A_v = 3.530 \text{ dB}
$$

The −3 dB gain is:

$$
A_v - 3 = 3.530 - 3
$$

$$
A_v - 3 = 0.530 \text{ dB}
$$

##

### Cutoff Frequencies

Lower cutoff frequency:

$$
f_L = 0
$$

Upper cutoff frequency:

$$
f_H = 184.562 \text{ MHz}
$$

##

### Bandwidth

Bandwidth is defined as:

$$
BW = f_H - f_L
$$

$$
BW = 184.562 - 0
$$

$$
BW = 184.562 \text{ MHz}
$$

# Experiment 2C - Common Source (CS) Amplifier using PMOS Active Load and Diode-Connected NMOS

## Aim

To design a Common Source (CS) amplifier using an NMOS transistor with PMOS Active Load and Diode-Connected NMOS in 180nm TSMC technology in LTSpice with a supply voltage of 1.8V and power constraint less than or equal to 1mW, and to analyze its DC operating point, transient response, voltage gain, and bandwidth.

### Diode-Connected NMOS (M3)

In this experiment, the source terminal of M1 is connected to a diode-connected NMOS transistor (M3). A diode-connected MOSFET has its gate and drain shorted together.

Its small-signal resistance is:

$$
r_{d3} = \frac{1}{g_{m3} + g_{ds3}}
$$

This configuration provides:

- Self-biasing of the amplifier  
- Improved operating point stability  
- Transistor-based current control  

However, it introduces source degeneration because the source is no longer at AC ground.

##

**Gain is given by**
$$
A_v = \frac{-g_{m1} (r_{o1} || r_{o2})}{1 + g_{m1} r_{d3}}
$$
All parameters are same as 1st circuit the Rs is replaced by Diode connected transistor That is the gate and drain are shorted.

## 3. Design Calculations

### GIVEN PARAMETERS

- Technology: TSMC 180nm
- Supply voltage, $V_{DD} = 1.5V$
- Power constraint ≤ 0.5mW
- Channel length, $L_n = 180nm$
- Threshold voltage, $V_T ≈ 0.366V$
- Electron mobility, $\mu_n = 273.81 \times 10^{-4} \ m^2/Vs$
- Load capacitor, $C_L = 10pF$
- Gate oxide thickness, $t_ox = 4.1 \times 10^{-9} \ m$

As M3 is diode-connected,

$$
V_{S1} = V_{GS3}
$$

$$
V_{S1} = 0.61V
$$

Gate voltage becomes:

$$
V_{IN} = V_{GS1} + V_{S1}
$$

$$
V_{IN} = 0.61 + 0.61
$$

$$
V_{IN} = 1.22V
$$

### Output Voltage Selection

For this configuration:

$$
V_{OUT} = \frac{V_{DD}}{2} + V_{DS3}
$$

$$
V_{OUT} = 0.75 + 0.61
$$

$$
V_{OUT} = 1.36V
$$
 ## DC Analysis 
 <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/19e29823-e10f-43ca-a4ef-79c9f3866342" />

### Transient Analysis
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/a454f8f7-4d56-4ca6-b032-471facbc9cba" />

### Theoretical Gain

For this configuration (PMOS active load with diode-connected NMOS), the voltage gain is given by:

$$
A_v = \frac{-g_{m1} r_{o2}}{1 + \frac{g_{m1}}{g_{m3}}}
$$

### Transconductance:

$$
g_{m1} = \frac{2 I_D}{V_{OV}}
$$

$$
g_{m1} = \frac{2 \times 300 \times 10^{-6}}{0.25}
$$

$$
g_{m1} = 2.4 \times 10^{-3} \ S
$$

Since M3 carries the same current:

$$
g_{m3} = 2.4 \times 10^{-3} \ S
$$

Assuming channel length modulation:

$$
r_{o2} = \frac{1}{\lambda I_D}
$$

$$
r_{o2} = \frac{1}{0.1 \times 300 \times 10^{-6}}
$$

$$
r_{o2} = 33.3k\Omega
$$

Substituting:

$$
A_v = \frac{2.4 \times 10^{-3} \times 33.3 \times 10^{3}}
{1 + \frac{2.4 \times 10^{-3}}{2.4 \times 10^{-3}}}
$$

$$
A_v = \frac{80}{2}
$$

$$
A_v = 40
$$

Gain in dB:

$$
A_v(dB) = 20 \log_{10}(40)
$$

$$
A_v(dB) = 32.04\ dB
$$


