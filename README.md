# FPGA Fabric Design and Architecture 

This repository contains the documentation, implementation flow, analysis reports, simulations, and FPGA architecture exploration completed during the FPGA Fabric Design and Architecture Workshop.

The project focuses on understanding the complete FPGA implementation flow, from RTL design to FPGA architecture generation, placement, routing, timing analysis, utilization analysis, power analysis, and post-implementation verification using open-source FPGA CAD tools.

## Tools and Platforms Used
- VTR (Verilog-to-Routing)
- VPR (Versatile Place and Route)
- OpenFPGA
- Vivado
- SOFA FPGA Fabric
- RISC-V Processor Core (RVMYTH)

---

# Workshop Overview

The workshop focused on understanding how digital RTL designs are transformed into FPGA hardware implementations using open-source FPGA CAD frameworks.

The flow covered:

- RTL Design
- Functional Simulation
- FPGA Synthesis
- Technology Mapping
- Placement
- Routing
- Timing Analysis
- FPGA Resource Utilization
- Power Analysis
- FPGA Fabric Generation
- Post Implementation Simulation

The workshop also introduced custom FPGA architectures using SOFA FPGA fabric and OpenFPGA framework.

---

# Tools Used

| Tool | Purpose |
|------|----------|
| Vivado | RTL Simulation and FPGA Analysis |
| VTR | FPGA CAD Flow |
| VPR | Placement and Routing |
| OpenFPGA | FPGA Fabric Generation |
| Verilog | RTL Design |
| SDC | Timing Constraints |

---

# Repository Structure

| Day | Description |
|-----|-------------|
| [Day 1](./Day1.md) | Introduction to FPGA Flow, Vivado Simulation and Basic Counter Design |
| [Day 2](./Day2.md) | VTR Flow, EArch Architecture, Timing Constraints, Routing and FPGA Reports |
| [Day 3](./Day3.md) | Mythcore Processor Implementation, ILA Debugging and FPGA Analysis |
| [Day 4](./Day4.md) | Post Synthesis Simulation, Primitive Models and Timing Verification |
| [Day 5](./Day5.md) | RISC-V Core on Custom SOFA FPGA Fabric using OpenFPGA |

---

# Topics Covered

## FPGA Basics

- FPGA Architecture
- LUTs and Flip-Flops
- Routing Resources
- FPGA Logic Blocks
- Clock Networks

---

## RTL Design and Simulation

- Verilog HDL
- Testbench Creation
- RTL Functional Simulation
- Waveform Analysis

---

## FPGA CAD Flow

- RTL Synthesis
- Technology Mapping
- Placement
- Routing
- Bitstream Generation

---

## Timing Analysis

- Setup Timing
- Hold Timing
- Critical Path Analysis
- Timing Constraints using SDC

---

## FPGA Architecture Exploration

- EArch FPGA Architecture
- SOFA FPGA Fabric
- FPGA Resource Utilization
- Routing Congestion Analysis

---

## OpenFPGA Flow

- FPGA Fabric Generation
- FPGA Architecture Mapping
- Netlist Generation
- Post Implementation Simulation

---

# Important Concepts Explored

- FPGA Fabric Architecture
- Routing Architecture
- Timing Closure
- Placement and Routing
- Resource Utilization
- Power Estimation
- Processor Implementation on FPGA
- FPGA Netlist Generation
- Open-source FPGA Toolchain

---

# FPGA Architectures Explored

## EArch Architecture

The EArch FPGA architecture was used to understand:

- FPGA routing resources
- Timing analysis
- FPGA placement
- FPGA netlist generation

---

## SOFA FPGA Fabric

The SOFA FPGA fabric was used for implementing the RVMYTH RISC-V processor core using OpenFPGA framework.

Features explored:

- FPGA fabric generation
- Timing closure
- FPGA routing
- Resource utilization
- Post implementation simulation

---

# Outputs Generated

The following reports and outputs were generated during the workshop:

- RTL Simulation Waveforms
- Timing Reports
- Hold Reports
- Setup Reports
- FPGA Utilization Reports
- Placement Reports
- Routing Reports
- Post Implementation Simulation
- FPGA Netlists
- FPGA Architecture Reports
- Power Analysis Reports

---

# Learning Outcomes

Through this workshop, the following concepts were understood practically:

- FPGA implementation flow
- FPGA architecture exploration
- RTL to GDS-style FPGA flow
- Open-source FPGA CAD frameworks
- Timing analysis and timing closure
- FPGA routing and placement
- FPGA resource analysis
- Processor implementation on FPGA fabric

---

# References

## VLSI System Design
https://www.vlsisystemdesign.com/ip/

## RISC-V Based Microprocessor
https://github.com/shivanishah269/risc-v-core

## 4-stage RISC-V Core
https://github.com/ShonTaware/RISC-V_Core_4_Stage

## SOFA FPGA Framework
https://github.com/lnis-uofu/SOFA

## OpenFPGA Documentation
https://openfpga.readthedocs.io/en/master/

## VPR Documentation
https://docs.verilogtorouting.org/en/latest/vpr/

## VTR Documentation
https://docs.verilogtorouting.org/en/latest/

---

# Acknowledgement

- Kunal Ghosh – VSD Corp Pvt Ltd
- VSD Workshop Team

This repository documents the complete hands-on FPGA architecture and FPGA CAD flow exploration performed during the workshop.

---
