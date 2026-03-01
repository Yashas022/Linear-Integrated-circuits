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



   
  
















