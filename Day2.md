# DAY 2 - Exploring OpenFPGA, VPR and VTR Flow

## Introduction

Day 2 focused on understanding the open-source FPGA CAD flow using:
- OpenFPGA
- VPR (Versatile Place and Route)
- VTR (Verilog-To-Routing)

The complete flow from Verilog RTL to FPGA routing and timing analysis was explored. Timing constraints, post-synthesis simulation, power analysis and generated reports were also studied.

---

# Introduction to OpenFPGA

OpenFPGA is an open-source FPGA framework used for:
- FPGA architecture exploration
- Bitstream generation
- FPGA fabric generation
- CAD automation
- Verification and testing

The framework supports:
- Verilog-to-Bitstream flow
- Custom FPGA architecture exploration
- Automated FPGA fabric generation

---

# Introduction to VPR

VPR (Versatile Place and Route) is an open-source CAD tool used for:
- Packing
- Placement
- Routing
- Timing Analysis

The VPR flow consists of:

1. Packing  
2. Placement  
3. Routing  
4. Timing Analysis  

---

# VPR Flow Command

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
<blif-file-path> \
--route_chan_width 100 \
--disp on
```

---

# VPR Architecture Flow

The VPR flow performs:

## Packing
Combines logic primitives into FPGA logic blocks.

## Placement
Places logic blocks inside FPGA grid.

## Routing
Creates interconnections between FPGA logic blocks.

## Timing Analysis
Analyzes setup and hold timing paths.

---

# VPR GUI Visualization

VPR GUI was used to visualize:
- FPGA grid
- Routing resources
- Logic placement
- Nets and critical paths

## VPR Visualization

<img width="893" height="857" alt="Image" src="https://github.com/user-attachments/assets/ab3b9fe2-0c89-4475-90ef-bbfdf13d2b5d" />


*VPR placement and routing visualization.*

---

# EArch FPGA Architecture Analysis using VPR

The `EArch.xml` FPGA architecture file was analyzed using the VPR flow. The architecture visualization, routing resources, nets, logical connections and timing reports were generated and studied.

The VPR flow was executed using the following command:

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
$VTR_ROOT/vtr_flow/benchmarks/blif/tseng.blif \
--route_chan_width 100 \
--disp on
```

---

# FPGA Architecture Visualization

The FPGA architecture generated using `EArch.xml` contains:
- Logic blocks
- Routing channels
- Switch blocks
- Interconnect resources
- FPGA grid structure


# Nets Analysis

The nets report contains:
- Source and destination nodes
- Interconnect paths
- Net routing information
- Routing resource usage

## Nets Report
<img width="921" height="892" alt="Image" src="https://github.com/user-attachments/assets/e8b8e826-8b6f-4b76-b2a8-c9270c9e6478" />


*Net connections generated after routing.*

---

# Logical Connections

Logical connections show:
- Signal interconnections
- Routing connectivity
- Logic block communication

## Logical Connections Report

<img width="923" height="881" alt="Image" src="https://github.com/user-attachments/assets/0e59ae9c-c3ee-40bb-8f52-b8004350d7db" />


*Logical interconnections generated during routing.*

---

# Critical Path Analysis

Critical path analysis determines:
- Longest timing path
- Maximum propagation delay
- Maximum operating frequency

The critical path directly impacts FPGA performance.

## Critical Path Report

<img width="918" height="887" alt="image" src="https://github.com/user-attachments/assets/6ed0484b-885a-42be-8db9-9cbfb0fcdc8a" />



*Critical timing path generated during timing analysis.*

---

# Routing Utilization

Routing utilization shows:
- Channel occupancy
- Routing efficiency
- Congestion distribution
- Resource utilization

## Routing Utilization Report

<img width="922" height="897" alt="image" src="https://github.com/user-attachments/assets/bea85348-8ca2-4f74-9374-a913b7a0f0d1" />



*Routing utilization generated after placement and routing.*

---

# Timing Analysis using Constraints

Timing constraints were added using an SDC file.

The constraints file defines:
- Clock period
- Input delays
- Output delays

---

# SDC Constraint File

## Constraint File

```tcl
create_clock -period 10 -name pclk
set_input_delay -clock pclk -max 0 [get_ports {*}]
set_output_delay -clock pclk -max 0 [get_ports {*}]
```

---

# Running VPR with Constraints

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
$VTR_ROOT/vtr_flow/benchmarks/blif/tseng.blif \
--route_chan_width 100 \
--sdc_file tseng.sdc \
--disp on
```

---

# Setup Timing Analysis

Setup timing checks whether data reaches destination registers before the active clock edge.

After adding constraints:
- Setup slack improved
- Timing closure was achieved
- Violations were reduced

## Setup Timing Report

<img width="1095" height="576" alt="image" src="https://github.com/user-attachments/assets/10461c20-42e0-45f3-8af9-a93a86fed5ac" />



*Setup timing report after applying timing constraints.*

---

# Hold Timing Analysis

Hold timing ensures data remains stable after the active clock edge.

## Hold Timing Report

<img width="1143" height="207" alt="image" src="https://github.com/user-attachments/assets/eada22f6-a830-4551-a808-447386e085f9" />



*Hold timing report generated using VPR timing analysis.*

---

# Introduction to VTR

VTR (Verilog-To-Routing) is a complete open-source FPGA CAD flow.

The VTR flow performs:
- RTL Elaboration
- Synthesis
- Technology Mapping
- Packing
- Placement
- Routing
- Timing Analysis

Tools involved:
- ODIN II
- ABC
- VPR

---

# VTR Flow Command

```bash
$VTR_ROOT/vtr_flow/scripts/run_vtr_flow.py \
counter.v \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
-temp_dir . \
-route_chan_width 100
```

---

# Counter Design for VTR Flow

The following counter design was used for VTR implementation.

## Counter Verilog Code

```verilog
/*Important: Once you run ./a.out, it will keep running infinitely, because it is in an always block. You need to hit Ctrl + Z to stop it, else, the vcd will become a large file and will never end.
*/

module up_counter (
out      ,
enable   ,
clk      ,
reset
);

output [3:0] out;

input enable, clk, reset;

reg [3:0] out;

always @(posedge clk)

if (reset) begin
    out = 4'b0 ;
end

else if (enable) begin
    out = out + 1;
end

endmodule
```

---

# VTR Flow Stages

The VTR flow performed the following stages:

1. Elaboration and Synthesis using ODIN II  
2. Logic Optimization using ABC  
3. Packing using VPR  
4. Placement using VPR  
5. Routing using VPR  
6. Timing Analysis  

---

# Generated VTR Outputs

The VTR flow generated:
- `.net`
- `.place`
- `.route`
- `.blif`
- Timing reports
- Routing reports
- Placement reports

---

# Nets and Logical Connections

The generated reports included:
- Nets
- Routing utilization
- Critical paths
- Logical interconnections

## Nets Report and Logical Connections

<img width="1175" height="767" alt="image" src="https://github.com/user-attachments/assets/74c0a27e-02c7-4e69-b047-7c103f4a8e16" />
<img width="927" height="747" alt="image" src="https://github.com/user-attachments/assets/49d200ce-7161-4c9d-baf1-798188ad8ac9" />



*Logical routing connections generated by VPR.*

---

# Critical Path Analysis

Critical path analysis was performed after routing.

The critical path determines:
- Maximum operating frequency
- Worst-case delay path

## Critical Path Report

<img width="905" height="771" alt="image" src="https://github.com/user-attachments/assets/d3697f88-c1b2-49ec-b061-1ab5535a93f0" />




*Critical timing path generated during routing.*

---

# Timing Analysis using Constraints

Timing constraints were added using `.sdc` file.

The constraints define:
- Clock period
- Input delays
- Output delays

---
# Setup Timing Report

## Setup Timing

<img width="792" height="465" alt="image" src="https://github.com/user-attachments/assets/25af78ef-3dc8-45fe-9969-eafac7d6471a" />




*Setup timing report before applying constraints.*

---

# Hold Timing Report

## Hold Timing

<img width="808" height="537" alt="image" src="https://github.com/user-attachments/assets/9a021249-6915-407a-add7-2fbdc64c51b3" />




*Hold timing report generated by VPR before constraints.*

---

# SDC Constraint File

## Constraint File

```tcl
create_clock -period 10 up_counter_clk
set_input_delay -clock up_counter_clk -max 0 [get_ports {*}]
set_output_delay -clock up_counter_clk -max 0 [get_ports {*}]
```

---

# Running VPR with Constraints

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
counter.pre-vpr.blif \
--route_chan_width 100 \
--sdc_file counter.sdc
```

---

# Setup Timing Report

After adding timing constraints:
- Setup slack improved
- Timing requirements were met

## Setup Timing

<img width="900" height="603" alt="image" src="https://github.com/user-attachments/assets/dc211b5b-de59-4e02-9fa4-b095d0fd4d6b" />




*Setup timing report after applying constraints.*

---

# Post Synthesis Simulation

Post synthesis simulation was performed using:
- Generated post synthesis netlist
- SDF timing file
- Vivado simulator

The generated files:
- `up_counter_post_synthesis.v`
- `up_counter_post_synthesis.sdf`

---

# Generating Post Synthesis Netlist

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
counter.pre-vpr.blif \
--gen_post_synthesis_netlist on
```

---

# Testbench for Post Synthesis Simulation

## Counter Testbench

```verilog
`timescale 1ns/1ps

module upcounter_testbench();

reg clk, reset, enable;
wire [3:0] out;

up_counter dut(
    .\up_counter^enable (enable),
    .\up_counter^clk (clk),
    .\up_counter^reset (reset),
    .\up_counter^out~0 (out[0]),
    .\up_counter^out~1 (out[1]),
    .\up_counter^out~2 (out[2]),
    .\up_counter^out~3 (out[3])
);

initial $sdf_annotate("up_counter_post_synthesis.sdf", dut);

initial begin

clk=0;
enable=0;
reset=1;

#20;

reset=0;
enable=1;

end

always
#5 clk=~clk;

endmodule
```

---

# Power Analysis using VTR

Power estimation was performed using VTR power analysis flow.

The flow estimated:
- Dynamic power
- Routing power
- Clock power
- Leakage power

---

# Power Analysis Command

```bash
$VTR_ROOT/vtr_flow/scripts/run_vtr_flow.py \
counter.v \
$VTR_ROOT/vtr_flow/arch/timing/k6_frac_N10_mem32K_40nm.xml \
-power \
-temp_dir . \
-route_chan_width 100
```

---

## stdout.log report

<img width="852" height="362" alt="image" src="https://github.com/user-attachments/assets/65b1a3df-7fd4-4477-a4f9-fe30fb10650b" />



*stdout.log report generated using VTR.*

# Power Report

## Power Analysis

<img width="756" height="392" alt="image" src="https://github.com/user-attachments/assets/054cfc28-22ad-4b43-b188-7b81b89fc4ac" />



*Power estimation report generated using VTR.*

---

# VTR Generated Reports

Generated reports included:
- Timing reports
- Routing reports
- Power reports
- Placement reports
- Post synthesis netlists

---

# Important Commands Used

## Running VTR Flow

```bash
$VTR_ROOT/vtr_flow/scripts/run_vtr_flow.py \
counter.v \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
-temp_dir . \
-route_chan_width 100
```

---

## Running VPR GUI

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
counter.pre-vpr.blif \
--route_chan_width 100 \
--disp on
```

---

## Running VPR with Constraints

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
counter.pre-vpr.blif \
--route_chan_width 100 \
--sdc_file counter.sdc
```

---

## Generating Post Synthesis Netlist

```bash
$VTR_ROOT/vpr/vpr \
$VTR_ROOT/vtr_flow/arch/timing/EArch.xml \
counter.pre-vpr.blif \
--gen_post_synthesis_netlist on
```
