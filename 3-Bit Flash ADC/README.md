# 3-Bit Flash ADC — CMOS Design (ECL-312)

**Author:** Gandemula Ajay Kumar (BT22ECE053)
**Institute:** IIIT Nagpur, Dept. of Electronics and Communication Engineering
**Course:** CMOS Design (ECL-312)
**Instructor:** Dr. Paritosh Peshwe

## Overview

A 3-bit Flash ADC implemented at the transistor level using CMOS logic, designed and simulated in **Microwind** (layout) and **NGSpice** (netlist-level transient simulation). Flash ADCs are the fastest ADC architecture, using fully parallel comparison instead of successive approximation — ideal for high-speed applications like digital oscilloscopes and radar signal processing.

## Architecture

The design has three stages:

1. **Resistive Voltage Divider** — 8× 1kΩ resistors generate 7 evenly spaced reference voltages from `Vref`.
2. **7 Comparators** — each compares the analog input against one reference voltage, implemented as a CMOS differential-pair comparator (see MOSFET structure below).
3. **Priority Encoder** — combines the 7 comparator outputs (thermometer code) into a 3-bit binary output, built from 4-input OR gates derived via K-map reduction:

```
Q2 = D1 + D3 + D5 + D7
Q1 = D2 + D3 + D6 + D7
Q0 = D4 + D5 + D6 + D7
```

## Repository Structure

```
.
├── spice/
│   └── adc_netlist.cir      # NGSpice transistor-level netlist (comparator + ADC)
├── layout/
│   └── adc1.MSK             # Microwind mask/layout file
└── docs/
    ├── CMOS_Project_Report.docx
    └── ADC_Report.pdf       # Full report with schematics, layouts, waveforms
```

## Simulation

Run the netlist in NGSpice:

```bash
ngspice spice/adc_netlist.cir
```

This runs a transient analysis (`.tran 0.1 320`) and plots the comparator output nodes.

**Verified result:** for `Vin = 1.800 V`, the ADC output digital code = `001`.

## Tools Used

- **Microwind** — CMOS transistor-level layout and DC simulation
- **NGSpice** — netlist-level transient simulation

## Conclusion

The 3-bit Flash ADC was successfully designed and verified at both the netlist and layout level, confirming correct operation of the voltage divider, comparator array, and priority encoder stages.
