# Day 5 - RISCV Core on Custom SOFA Fabric

The RVMYTH RISC-V core was integrated with the custom SOFA FPGA fabric and executed through the complete OpenFPGA and VTR flow. The implementation generated various timing, utilization, routing, and simulation reports which were analyzed to verify the correctness of the design and FPGA mapping process.

---

# SOFA RVMYTH Utilization Report

The utilization report shows the FPGA resource usage of the RVMYTH core after synthesis and mapping onto the SOFA FPGA architecture.

The design consumes LUTs, latches, CLBs, routing resources, and logic elements. This report helps in understanding the hardware cost of implementing the processor core on the FPGA fabric.

## Circuit Statistics

- Total Blocks: 5526
- Inputs: 2
- Latches: 1807
- Outputs: 8
- 0-LUTs: 4
- 4-LUTs: 3675

## Net Statistics

- Total Nets: 5488

## Timing Graph

<img width="522" height="482" alt="image" src="https://github.com/user-attachments/assets/0101cdaf-4d41-4357-a7d1-4e7921036bbb" />


*Detailed FPGA primitive block usage and logic element statistics for the RVMYTH implementation.*

---

# Constraints File

An SDC (Synopsys Design Constraints) file was created to define the clock timing constraints for the design.

## Constraint File Used

```tcl
create_clock -period 200 clk
set_input_delay -clock clk -max 0 [get_ports {*}]
set_output_delay -clock clk -max 0 [get_ports {*}]
```

The constraint file defines:

- Clock period
- Input delay constraints
- Output delay constraints

These constraints are used by the timing analysis engine during placement and routing.

---

# Timing Analysis

Timing analysis was performed after placement and routing to verify whether the design satisfies setup and hold timing constraints.

The setup timing report shows that the data arrival time is within the required timing limits and timing slack is positive.

<img width="627" height="515" alt="image" src="https://github.com/user-attachments/assets/c1b23c53-a172-4dec-bd36-c215b8f037a1" />


*Setup timing analysis report showing positive timing slack for the RVMYTH core.*

---

# Hold Timing Analysis

Hold timing analysis verifies that the data remains stable for the required duration after the clock edge.

<img width="667" height="573" alt="image" src="https://github.com/user-attachments/assets/cdc6d9f6-7f98-44b7-b9a9-1feef8483135" />


*Hold timing analysis report showing successful hold timing closure.*

---

# Post Implementation Simulation

Post implementation simulation was performed after synthesis, placement, and routing of the RVMYTH core.

The generated waveform confirms the correct execution of the processor logic after FPGA implementation. The simulation validates that the synthesized and routed netlist behaves correctly under the given clock and reset conditions.

The waveform also demonstrates proper output transitions and stable processor execution after implementation.

<img width="1000" height="367" alt="image" src="https://github.com/user-attachments/assets/9c959203-ce29-4b9d-97e1-1a5b3e19bb8e" />



*Post implementation simulation waveform of the RVMYTH core on SOFA FPGA fabric.*

---

# Observations

- The RVMYTH processor was successfully mapped onto the custom SOFA FPGA fabric.
- FPGA resource utilization increased significantly compared to smaller counter-based designs.
- Timing constraints were successfully met with positive setup and hold slack values.
- The OpenFPGA and VTR flow successfully generated all required reports and simulation outputs.
- Post implementation simulation verified the correctness of the synthesized FPGA netlist.

---

# Conclusion

The RVMYTH RISC-V core was successfully implemented on the custom SOFA FPGA architecture using the OpenFPGA and VTR framework. The generated utilization reports, timing analysis, and simulation waveforms confirm that the processor operates correctly on the FPGA fabric while satisfying all timing constraints.

This experiment demonstrated the complete FPGA implementation flow starting from RTL design to post implementation verification using an open-source FPGA toolchain.
