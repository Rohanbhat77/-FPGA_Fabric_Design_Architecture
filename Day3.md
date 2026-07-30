# DAY 3 – Mythcore Processor Implementation and FPGA Analysis

## Objective

The objective of Day 3 was to work with a more complex RTL design instead of a simple counter circuit.  
A Mythcore RISC-V based processor design was taken and implemented on FPGA.  

The work involved:

- RTL simulation
- FPGA synthesis
- Schematic generation
- Package and pin mapping
- Adding ILA (Integrated Logic Analyzer)
- Timing analysis
- Utilization analysis
- Power analysis
- Observing simulation outputs

This experiment helped in understanding how larger digital systems behave on FPGA architectures and how FPGA tools analyze timing, routing, area, and power.

---

# FPGA Design Flow

The complete FPGA implementation flow followed was:

1. RTL Design
2. Functional Simulation
3. Synthesis
4. Netlist Generation
5. Placement
6. Routing
7. Timing Analysis
8. Bitstream Generation
9. Hardware Debugging using ILA

---

# RTL Simulation

The Mythcore processor was first simulated before synthesis to verify proper functionality.

## Observations

- Clock signal toggled correctly
- Reset initialized the processor
- Outputs changed according to processor execution
- Functional behavior matched expected results

---

## RTL Simulation Output

<img width="998" height="366" alt="Image" src="https://github.com/user-attachments/assets/e0707e84-44a4-40f9-b1b4-02f2c4083c1c" />


*RTL simulation waveform of Mythcore processor*

---

# Schematic Generation

After synthesis, Vivado generated the RTL schematic for the processor design.

The schematic displayed:

- LUT structures
- Flip-flops
- Internal routing
- Processor datapath
- Logic interconnections

Since Mythcore is significantly more complex than a simple counter, the generated schematic was large and densely interconnected.

---

## RTL Schematic Output

<img width="966" height="557" alt="Image" src="https://github.com/user-attachments/assets/f5add2be-ddb2-4cc3-a411-c182019ae7aa" />

*RTL schematic generated for Mythcore processor*

---

# Package View

The package view displayed FPGA resource placement and I/O pin allocation.

This helped in understanding:

- Physical FPGA layout
- Resource mapping
- Pin assignments
- FPGA routing regions

---

## Package View Output

<img width="590" height="362" alt="image" src="https://github.com/user-attachments/assets/9c3130a1-c75c-4115-9e90-2751fbf1f5e7" />


*FPGA package view showing FPGA resource utilization*

---

# Integrated Logic Analyzer (ILA)

## Objective

ILA was added to debug and monitor internal FPGA signals in real time.

Instead of only viewing external outputs, ILA allows internal processor signals to be captured directly using Vivado Hardware Manager.

---

# ILA Instantiation

```verilog
ila_0 your_instance_name (
    .clk(clk),

    .probe0(reset),
    .probe1(out)
);
```

---

# ILA Connections

The following signals were connected:

| Signal | Purpose |
|--------|----------|
| clk | Clock input |
| reset | Reset signal |
| out | Output probe |

---

# Constraint File

The XDC constraint file was created to define:

- Clock pin mapping
- Reset pin mapping
- Timing constraints
- Debug hub configuration
- Clock frequency

---

## Constraints Used

```tcl
set_property PACKAGE_PIN V6 [get_ports clk]
set_property IOSTANDARD LVCMOS33 [get_ports clk]

set_property IOSTANDARD LVCMOS33 [get_ports reset]
set_property PACKAGE_PIN P2 [get_ports reset]

create_clock -period 10.000 -name clk -waveform {0.000 5.000} [get_ports clk]

set_property C_CLK_INPUT_FREQ_HZ 300000000 [get_debug_cores dbg_hub]
set_property C_ENABLE_CLK_DIVIDER false [get_debug_cores dbg_hub]
set_property C_USER_SCAN_CHAIN 1 [get_debug_cores dbg_hub]

connect_debug_port dbg_hub/clk [get_nets clk_IBUF_BUFG]
```

---

# Utilization Analysis

The utilization report displayed FPGA resource consumption.

## Resources Used

- LUTs
- LUTRAM
- Flip-Flops
- BRAM
- IO Blocks

Compared to the counter design, Mythcore consumed significantly more FPGA resources due to processor complexity.

---

## Utilization Report

<img width="928" height="497" alt="image" src="https://github.com/user-attachments/assets/daf07cce-cb3d-4ce4-92d7-2d915a7a7ad5" />


*FPGA utilization report for Mythcore processor.*

---

# Timing Analysis

Timing analysis was performed after placement and routing.

Timing analysis ensures:

- Proper setup timing
- Proper hold timing
- Correct clock synchronization

<img width="960" height="191" alt="image" src="https://github.com/user-attachments/assets/2efbaee9-a2f4-4811-8aa4-38d3dcc5e9c1" />


*Timing analysis summary*

---

# Power Analysis

Power analysis was performed after implementation.

The report included:

- Dynamic power
- Static power
- Clock power
- Logic power
- Signal power

---

## Observations

- Clock network consumed significant dynamic power
- Logic switching activity contributed to power usage
- Static FPGA power remained nearly constant

---

## Power Analysis Output

<img width="936" height="351" alt="image" src="https://github.com/user-attachments/assets/3c0ac8c8-cf95-4156-8f62-9c6d105a1314" />


*Power analysis report of Mythcore FPGA implementation.*

---

# Important Observations

## Increased Design Complexity

Compared to the counter design:

- Routing complexity increased heavily
- Resource utilization became much larger
- Timing paths became more critical

---

## FPGA Resource Usage

The Mythcore processor used:

- Large number of LUTs
- Multiple flip-flops
- Additional routing resources
- More clock resources

---

## Importance of Constraints

Without proper timing constraints:

- Timing violations can occur
- Placement becomes inefficient
- Routing delays increase
- FPGA timing closure may fail

Constraints help FPGA tools optimize the design properly.

---

# Conclusion

In Day 3, a Mythcore RISC-V processor was successfully implemented and analyzed on FPGA.

The work included:

- RTL simulation
- Synthesis
- Schematic analysis
- Package mapping
- ILA debugging
- Timing analysis
- Utilization analysis
- Power analysis

This experiment provided deeper understanding of how complex processor-based RTL designs are implemented, routed, timed, and debugged inside FPGA architectures.

---
