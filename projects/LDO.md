---
title: LDO
layout: page
---

## Circuit Diagram

![image](https://user-images.githubusercontent.com/33692444/146647902-49792e00-c648-48a4-96e0-d91e3af06755.png)

## Description

* The main aim of this circuit is to maintain a constant programmable voltage within range (so devices using this are not damaged) throughout without any fluctuations from startup , power down and load/line regulation. 
* Noise Contribution of the circuit to other components using this is minimal. 
* The ciruit is ensured to be stable throughtout PVT using compensation, feedback and OTA. 
* Minimal power consumption is ensured by low functional and leakage currents. 
* No ideal components were used in the design and everything mimicked real world. 

## Specifications

The whole circuit was designed to meet the following specifications throughout PVT ranging from 
temperature of -40 to 125 degree, including all corners FF, SS , SF, FS , TT for all components .

* Phase margin >= 50 degree
* PSRR <= -30db
* DC loopgain >= 50db
* Vreg trans range 828m to 871m (2.5% variation)
* Power down current < 6u
* Functional current < 100u
* Max Vreg < 940m (including transient peaks

Simulations were carried out in Cadence Virtuoso using 135n FinFets and 54n FinFets technology files for all the devices

## Components used

### Pass Device
Sized the pass device with greater length and multipliers such that it can withstand large 
current and the Vgs and Vds are maintained so that the OTA functions properly and output 
voltage is maintained respectively.

### Compensation
Used the proper compensation technique such that it does not disturb introduce noise at 
the Vgs of the pass device and at the same time does not occupy too much area while giving 
good phase margin.

### Programmable output
The resistances decide the quiescent current and the feedback factor to the OTA and the 
output voltage. It was designed such that output voltage has 4 levels, 825m-900m in steps of 
25m, so that the LDO can have a wide range of application.

### Operational amplifier
Designed an OTA using the gm/id method to give sufficient gain but minimizing output 
resistance such that the compensation constraints can be relaxed. The OTA designed was
A 5-transistor differential circuit with the mosfets being in either subthreshold or saturation 
region throughout PVT.

## Working

* A vref is set by a source and the comparator finds the difference bertween the feedback voltage and the vref and then amplifies it. 
* The amplified voltage is given as gate voltage to the pass device which regulates the current flowing through it.
* The current then proportionaly decreases/increases the feedback voltage.
* Based on the feedback voltage the difference is again calculated till the difference is minimized.
* The feedback loop keeps running till the output voltage is maintained. 
* A separate compensation block is integrated to ensure the output does not oscillate and system have sufficient phase margin throughout PVT.


