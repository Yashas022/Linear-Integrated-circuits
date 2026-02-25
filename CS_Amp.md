Experiment 1: Common Source (CS) Amplifier Report and Analysis
# Experiment-1

## Aim
To perform DC analysis, Transient analysis, and AC analysis of a Common Source (CS) amplifier circuit using LTSpice and extract the various associated parameters.

## Components Required
- **MOSFET** (nmos4 in TSMC 180nm)
- **Voltage Supply** (1.5V)
- **power**=0.5mw and Cl=1pF
- **Connecting Wires**

## Theory
MOSFET is one of the most essential components in electronics due to:
- Compact design
- Low power consumption
- Simple geometry
- Compatibility with VLSI technology

### MOSFET Configurations
- **Common Source (CS)** (most widely used)
- **Common Drain**
- **Common Gate**

### Common Source Amplifier
- Operates in **saturation region** where:
  - V_gs > V_th
  - V_gd < V_th
  - V_ds geq V_ov
- 180-degree phase shift between input and output
- High input impedance (ideally infinite)
- Output taken from drain end to maintain common ground reference

---

### DC Analysis
- Ensures MOSFET operates in saturation
- Determines the **DC operating point** to prevent signal distortion
- Helps in bias resistor calculation
- Maintains a correct operating point despite parameter fluctuations
  <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/996492f0-a945-4961-b8c1-a08f8b756125" />


### Transient Analysis
- Analyzes response to time-varying signals
- Determines **signal distortion** and **DC shift** between input and output
- Detects **phase distortion**
- Essential for **high-speed applications**
 <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/2c690602-e9e6-43b1-b1c1-cb41e5d1f180" />




### AC Analysis
- **Small signal analysis**
- Determines **gain** of the amplifier circuit: \( A_v = -g_m R_d \)
- Analyzes **frequency response** of the amplifier

  <img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/3f320829-99d9-4241-acce-be85ca35b854" />
  
<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/23681526-c9c6-4d87-b71e-e7dac21e31eb" />

---

## Procedure
1. **Create a new folder** and save the LTSpice file in this directory.
2. **Set MOSFET parameters:**
   - NMOS: Name as `CMOSN`, Length = **180nm**, Width = **3um**
   - PMOS: Name as `CMOSP`, Length = **180nm**, Width = **3um**
3. **DC Analysis:**
   - Apply **Vdd = 1.5V**, **Vgs = 0.9V**
   - Run `.op` command in LTSpice to extract **DC operating point**
4. **Transient Analysis:**
   - Apply **sinusoidal input**: **Vgs = 0.9V**, Amplitude = **50mV**, Frequency = **1kHz**
   - Run `.tran 3m` to observe **time-domain response**
5. **AC Analysis:**
   - Specify frequency sweep from **0.1Hz to 1THz** with **20 points per decade**
   - Run `.ac dec 20 0.1 100G` to analyze **gain & frequency response**

---
### Inference 
1) Current is directly Propotional to the Width of the Mosfet and the current varies with the change in width.

2) Mosfet saturation ensures the mosfet works as an amplifier and produces the desired negative gain as per the equation Av=-gm*Rd.

3) Q point stability is attained in saturation region thus helping in attaining linear amplification .

4) The Mosfet gain is increased in mid band frequency range (small signal analysis).

5) The Transient analysis reveleas the response of the circuit to time domain ssignal and determines how quickly the circuit responds to variation.
This is essential in high speed applications.

6) AC Analysis helps in designing circuits with desired gain and helps in impedance matching.
Also helps in understanding the frequency response and small signal behaviour of the circuit.
