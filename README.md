S# Experiment – 1  
## DC, Transient and AC Analysis of Common Source Amplifier using 180nm NMOS in LTspice

---

## AIM :

To design a Common Source (CS) amplifier using NMOSFET in tsmc 180nm tech.lib in LTspice and to perform DC, Transient and AC analysis as per the given specifications.
## Introduction to Common Source Amplifier:

The Common Source (CS) amplifier is a fundamental single-transistor amplifier widely used in analog electronics. It provides voltage amplification with high input impedance and moderate output impedance.

In a CS amplifier:

- The input signal is applied to the gate of the MOSFET.
- The output signal is taken from the drain, producing a phase-inverted amplified output.
- The source terminal is typically connected to ground (common), hence the name Common Source.

This configuration is popular for small-signal amplification in analog circuits due to its simplicity, high gain, and ease of integration in CMOS technology.
---
## Design Specifications :
| Parameter        | Symbol | Value       | Unit | Notes                   |
| ---------------- | ------ | ----------- | ---- | ----------------------- |
| Supply Voltage   | VDD    | 2         | V    | Power supply            |
| Power Constraint | P      | ≤ 1.2       | mW   | Maximum allowable power |
| Load Capacitance | CL     | 10           | pF   | Output load capacitor   |
| Channel Length   | L      | 180         | nm   | MOSFET channel length   |
| Technology Node  | —      | 180 nm TSMC | —    | CMOS process technology |

---

## COMPONENTS USED :

- NMOS transistor (180nm model)  
- Drain resistor (RD)  
- DC power supply  
- AC signal source  
- Load capacitor (1 pF)  
- Ground and connecting wires  
---

## Circuit Description :

The circuit was designed using 180 nm NMOS technology in LTspice.

- Drain Resistor (RD): Connected between VDD and the drain terminal. It controls the output voltage swing and gain.
- Input Signal: Applied to the gate terminal of the NMOS transistor.
- Output Signal: Taken from the drain terminal.
- Source Terminal: Usually connected to ground (common reference).

![Image description](https://github.com/2024ecanithalc-sys/LIClab_experiments/blob/main/circuit%20diagram.jpeg?raw=true)
---
## Theory :

The **Common Source (CS) amplifier** is one of the most fundamental and widely used MOSFET amplifier configurations. It is primarily used for **voltage amplification** in analog circuits.  

### Circuit Configuration
- The **source terminal** is connected to **ground** (common reference).  
- The **input signal** is applied to the **gate terminal**.  
- The **output signal** is taken from the **drain terminal**.  
- A **drain resistor (RD)** is connected between **VDD** and the drain terminal to control the gain and output swing.  

### Operating Principle
1. The input voltage at the gate (**Vgs**) controls the **drain current (Id)**.  
2. Changes in **Id** produce a voltage drop across **RD**, generating the **amplified output voltage** at the drain.  
3. The output is **phase-inverted** relative to the input (180° phase shift).  

### Biasing and Q-Point
- Proper amplification requires the MOSFET to operate in the **saturation region**.  
- The **Q-point** (operating point) is usually set such that **VDS ≈ VDD / 2**, ensuring **maximum symmetrical output swing** without distortion.  

### Characteristics
- High voltage gain.  
- Moderate to high input impedance.  
- Output impedance depends on RD and MOSFET parameters.  
- Phase inversion of 180° between input and output.  

### Applications
- Small-signal voltage amplification.  
- Analog signal processing circuits.  
- Front-end amplifier stages for sensors and ADCs.  
- RF and audio amplifier stages in integrated circuits.
- 
## Procedure :

1. The **180 nm NMOS model file** (`tsmc018.lib`) was included in LTspice using the `.include` directive.  

2. The **Common Source amplifier circuit** was built with the following parameters:  
   - Supply voltage: **VDD = 2 V**  
   - Drain resistor: **RD ≈ 5 kΩ**  
   - NMOS transistor: **L = 180 nm**, **W =1.1 µm**  

3. **DC analysis** was performed using `.op` and `.dc` commands to determine the **Q-point**, targeting **VDS ≈ VDD / 2** for maximum output swing.  

4. The **drain resistor (RD)** and **W/L ratio** of the MOSFET were adjusted to achieve the desired **drain current** while keeping the **power consumption ≤ 1.2 mW**.  

5. **Transient analysis** (`.tran 5m`) was carried out using a sine input `SINE(0.9 10m 1k)` to observe both **linear and non-linear behavior** of the amplifier.  

6. **AC analysis** (`.ac dec 10 0.1 100G`) was performed to obtain the **frequency response**, including the amplifier's **gain** and **bandwidth**.

## DC ANALYSIS AND DESIGN CALCULATIONS :

To design the Common Source amplifier, the Q-point was fixed at  
VDS ≈ VDD / 2 for maximum symmetrical output swing.

The device parameters were extracted from the model file (tsmc018.lib).

### Given Parameters (From tsmc018.lib)
 
- Vth = 0.366 V  
- Tox = 4.1 × 10⁻⁹ m  
- μn (U0) = 273.809 cm²/V·s  
- εr (SiO₂) = 3.9  
- ε0 = 8.854 × 10⁻¹² F/m  
- Power constraint: P ≤ 1.2 mW  

Since the input DC bias at the gate is 0.9 V,

VGS = 0.9 V  

As VGS > Vth (0.9 V > 0.366 V),  
the NMOS operates in saturation region.

### Step 1: Calculate Drain Current Using Power Constraint

Using:

P = V × I  

0.4 × 10⁻³ = 2 × ID  

ID = (0.4 × 10⁻³) /2 

ID ≈ 2.00 × 10⁻⁴ A  

ID ≈ 0.200 mA  

### Step 2: Fix Q-Point

For maximum symmetrical swing:

VDS = VDD / 2  

VDS = 2 / 2  

VDS ≈ 1 V  

### Step 3: Calculate Drain Resistor (RD)

RD = (VDD − VDS) / ID  

RD = (2 − 1) / (2 × 10⁻⁴)  

RD ≈ 5 kΩ  

### Step 4: Calculate Oxide Capacitance (Cox)

First calculate oxide permittivity:

εox = εr × ε0  

εox = 3.9 × (8.854 × 10⁻¹²)  

εox ≈ 3.45 × 10⁻¹¹ F/m  

Now,

Cox = εox / Tox  

Cox = (3.45 × 10⁻¹¹) / (4.1 × 10⁻⁹)  

Cox ≈ 8.42 × 10⁻³ F/m²  

### Step 5: Calculate Process Transconductance Parameter (kn')

Convert mobility to SI units:

μn = 273.80 cm²/V·s  
= 0.02738 m²/V·s  

Now,

kn' = μn × Cox  

kn' = 0.02738 × (8.41 × 10⁻³)  

kn' ≈ 2.306 × 10⁻⁴ A/V²  

### Step 6: Calculate Required Transistor Width (W)

Using MOSFET saturation equation:

ID = (kn'/2) × (W/L) × (VGS − Vth)²  

Given:

VGS = 0.9 V  
Vth = 0.366 V  

(VGS − Vth) = 0.534 V  

L = 180 nm = 180 × 10⁻⁹ m  

Substituting:

2.00 × 10⁻⁴ = (2.30 × 10⁻⁴ / 2) × (W / 180 × 10⁻⁹) × (0.534)²  

Solving,

W ≈ 1.1 µm  

After simulation tuning to obtain accurate Q-point:

Final selected width:

W = 1.5 µm  


### DC Operating Point from LTspice

ID ≈ 0.2 mA  
VDS ≈ 1.0 V  

Thus, the Q-point is successfully fixed near mid-supply.
### DC Simulation Result

![Image description](https://github.com/2024ecanithalc-sys/LIClab_experiments/blob/main/Operating%20point.jpeg?raw=true)

-----

## DC PARAMETER VARIATION STUDY :

### (a) Effect of Varying RD (For Fixed W/L)

The width and length of the transistor were kept constant (W = 1.5 µm, L = 180 nm).  
The drain resistor RD was varied to observe its effect on the Q-point.

Observation:

- Increasing RD increases the voltage drop across RD.
- As RD increases, VDS decreases.
- Drain current slightly reduces for larger RD values.
- Proper RD selection is required to maintain VDS ≈ VDD/2.

Thus, RD ≈ 5 kΩ was selected to obtain VDS ≈ 1V.

### DC Sweep Result

The DC sweep of input voltage was performed from 0 V to 2 V to observe variation in supply current and verify the power constraint.

![Image description](https://github.com/2024ecanithalc-sys/LIClab_experiments/blob/main/DCsweep.jpeg?raw=true)


---

### (b) Effect of Varying W (For Fixed RD)

The drain resistor was kept constant at RD ≈ 5 kΩ.  
The transistor width (W) was varied to analyze its effect on drain current.

Observation:

- Increasing W increases drain current.
- Larger W shifts the Q-point due to higher ID.
- Smaller W reduces ID and moves VDS closer to VDD.

From simulation tuning, W = 1.5 µm provided the required drain current (≈ 0.2 mA) and correct biasing.
### DC Transfer Characteristic (Vout vs Vin)

The DC sweep was performed by varying input voltage from 0 V to 2  V.  
The variation of output voltage with respect to input voltage is shown below.

![DC Transfer Curve](dc_transfer.png)

---

## TRANSIENT ANALYSIS :

Transient simulation was performed using:

.tran 5m

A sine input of SINE(0.9 10m 1k) was applied at the gate terminal.

### Input Waveform (Vin)

![Input Waveform](vin_transient.png)

### Output Waveform (Vout)

![Output Waveform](vout_transient.png)

### Combined Input and Output Waveforms

![Image description](![Image description](https://github.com/2024ecanithalc-sys/LIClab_experiments/blob/main/Transient%20analysis.jpeg?raw=true)


### Observation

- Output waveform is inverted with respect to input (≈ 180° phase shift).
- Peak output voltage ≈ 590 mV
- Peak input variation ≈ 19 mV
- Voltage gain ≈ 3
- The amplifier operates in saturation region.

Thus, transient analysis confirms proper biasing and amplification.

...

### Gain Calculation (From Transient Analysis)

From the transient waveform:

Voltage Gain (Av) = Vout / Vin  

Peak-to-peak values were measured from the graph.

Output voltage:

Vout(max) = 1.032V  
Vout(min) = 0.973 V  

Vout(pp) =   1.032V -0.973 V
Vout(pp) = 0.059 V 

Input voltage:

Vin(max) = 0.91  V  
Vin(min) = 0.8903  V  

Vin(pp) = 0.91  V - 0.8903  V  
Vin(pp) = 0.0197  

Therefore,
Av = Vout(pp) / Vin(pp)  

Av =  0.059 V  / 0.0197V  
Av ≈ 3 

Gain in dB:

Av(dB) = 20 log(Av)  

Av(dB) = 20 log(3)  
Av(dB) ≈ 9054 DB  

### Theoretical Gain Calculation

For a Common Source amplifier:

Av = gm × RD  
gm = 2ID / (VGS − Vth)

Given:

ID = 0.2 mA  
VGS = 0.9 V  
Vth = 0.366 V  
RD = 5 kΩ  

Overdrive voltage:

Vov = VGS − Vth = 0.9 − 0.366 = 0.534 V  

Transconductance:

gm = (2 × 0.2 × 10⁻³) / 0.534  
gm ≈ 0.75 mS  

Therefore,

Av = gm × RD  
Av = (0.75 × 10⁻³) × (5000)  
Av ≈ 3.7 

Gain in dB:

Av(dB) = 20 log(3.7)  
Av(dB) ≈ 11.36 DB 

The simulated gain (3 ) is lower than the theoretical(3.7) value due to channel length modulation, output resistance effects, and other non-ideal device characteristics.

----

## AC ANALYSIS : 

AC analysis was performed using:

.ac dec 10 0.1 100G

The frequency response was obtained to determine gain and bandwidth.

### Observations

- The amplifier shows constant gain in the midband region.
- At higher frequencies, gain decreases due to parasitic capacitances.
- The presence of load capacitor (CL = 10 pF) reduces the bandwidth.

### Extracted Parameters

From AC plot (with CL = 1 pF):

- Midband gain ≈ 3
- Gain in dB ≈ 9.54 dB
- 3 dB bandwidth ≈ 56.4 GHz
- Unity Gain Bandwidth (UGB) ≈ 150.23 MHz
- GBP ≈ 3 × 56.4 GHz
     ≈  MHz (approx)

### AC Response Without Load Capacitor

(https://github.com/2024ecanithalc-sys/LIClab_experiments/blob/main/AC%20analysis.jpeg?raw=true)

### AC Response With Load Capacitor (CL = 10 pF)

![AC With Load](ac_with_cl.png)

![AC Response With Load Capacitor](AC_With_CL_Final.png)

----

### OVERALL COMPARISON TABLE :

| Parameter | Theoretical Value | Practical (Simulation) Value | Reason for Variation |
|------------|------------------|-----------------------------|----------------------|
| Drain Current (ID) | ≈ 0.2 mA | ≈ 0.2 mA | Minor rounding and model accuracy differences |
| VDS (Q-point) | 1 V | ≈ 1 V | Slight deviation due to transistor model non-idealities |
| Drain Resistor (RD) | 5 kΩ | 5 kΩ | Directly calculated from design equation |
| Transistor Width (W) | 1.1 µm (calculated) |1.5 µm (adjusted) | Width tuned in simulation to achieve exact Q-point |
| Voltage Gain (Av) | 3 | 3.7 | Channel length modulation and output resistance effects |
| Gain (dB) | 9.54 dB | 11.36 dB | Practical gain reduced due to non-ideal device behavior |
| 3 dB Bandwidth | — | 56  GHz | Limited by parasitic capacitances |
| Unity Gain Bandwidth (UGB) | — | 150 MHz | Determined by dominant pole and device capacitances |
| Gain Bandwidth Product (GBP) | — | ≈ 187 MHz | Product of midband gain and bandwidth |

----

## INFERENCE :

1. The Common Source (CS) amplifier was successfully designed using 180 nm NMOS technology under the given power constraint of 0.5 mW.

2. The Q-point was fixed at VDS ≈ VDD/2 (≈ 1 V), ensuring maximum symmetrical output swing.

3. The calculated drain current (0.2 mA) closely matched the simulated value (≈ 0.2 mA), validating the DC design.

4. Transient analysis confirmed voltage amplification with 180° phase inversion.

5. The practical gain (≈ 3 or 9.54 dB) was slightly lower than theoretical gain due to channel length modulation and non-ideal device effects.

6. AC analysis showed a midband gain of ≈  3 with 3 dB bandwidth ≈ 56.4  GHz.

7. The Unity Gain Bandwidth (UGB) was ≈ 150 MHz.

8. Adding load capacitance (10 pF) reduced bandwidth while maintaining nearly the same midband gain.

9. Overall, simulation results closely agree with theoretical expectations, validating the design methodology.

