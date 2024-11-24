# ICC2 ( IC Compiler II)

<details>
  <Summary> Introduction </Summary>
  <br>

  * IC Compiler II is specifically architected to address aggressive performance, power, area (PPA), and time-to-market pressures of leading edge designs.
  
* Key technologies include a pervasively parallel optimization framework, multi-objective global placement, routing driven placement optimization, full flow Arc based concurrent clock and data optimization, total power optimization, multi-pattern and FinFET aware flow and machine learning (ML) driven optimization for fast and predictive design closure.
  
* Advanced Fusion technologies offer signoff IR drop driven optimization, PrimeTime® delay calculation within IC Compiler II, exhaustive path based analysis (PBA) and signoff ECO within place and route for unmatched QoR and design convergence. 

![image](https://github.com/user-attachments/assets/bf363650-49b3-48b4-b64a-5d7bcebbab02)

* The `IC Compiler II` tool is designed for efficient design planning, placement, routing, and analysis of very large designs.
  
* IC Compiler II is a complete netlist-to-GDSII implementation system that includes early design exploration and prototyping, detailed design planning, block implementation, chip assembly and sign-off driven design closure.
  
* The foundation, architecture and implementation is based on novel, patented technologies and the software has been written using modern object-oriented languages and tools.
  
* IC Compiler II benefits from the combination of a new hierarchical infrastructure enabling massive parallelism; a highly compact multi-corner and multi-mode (MCMM) architecture; next-generation design-planning; new global, analytical, and scalable optimization techniques; and global optimization approaches to clock synthesis.
  
* `Design planning` is an integral part of the `RTL to GDSII design process`. During design planning, you assess the feasibility of different implementation strategies early in the design flow.
  For large designs, `design planning` helps you to “divide and conquer” the implementation process by partitioning the design into smaller, more manageable pieces for more efficient processing.
  
* IC Compiler is for place and route and it is used after synthesis which can be done with Synopsys DC compiler or Power compiler. IC Compiler goes through the following steps and its outputs go to tapeout.

![image](https://github.com/user-attachments/assets/b19633b4-bae0-4c58-8d8d-339916a8168f)

* Basic place and route design flow using the IC Compiler II 

![image](https://github.com/user-attachments/assets/64599960-502e-48fd-be37-fe66ec9664bb)


* IC Compiler three initialization Files

![image](https://github.com/user-attachments/assets/4404c6c2-cc11-45e2-a237-a3829ebeb2c3)

* Summary

![image](https://github.com/user-attachments/assets/9645bc4f-9273-4a1c-a45d-6f29d5ade61f)


* The `target_library` is the library that IC Compiler uses to pick cells for optimization and re-mapping. It is typically set to only the standard cells library.
  
* The `link_library` contains every library that contains cells that are referenced by the netlist.

1. Milkyway Reference Libraries 
Information is stored in so-called “views”, for example: 
   * CEL: The full layout view 
   * FRAM: The abstract view used for P&R 
   * LM: Logic Model with Timing and Power info (optional*) 。(Optional) here means that the logical libraries do not have to be stored within the Milkyway library structure, but can be located 
     anywhere else. IC Compiler only reads logical libraries (.db) specified through the link_library variable. 
 
2. Technology File (.tf file) 
   * Tech File is unique to each technology
   * Contains metal layer technology parameters:
     *  Number and name designations for each layer/via
     *  Dielectric constant for technology
     *  Physical and electrical characteristics of each layer/via
     *  Design rules for each layer/Via (Minimum wire widths and wire-to-wire spacing, etc.)
     *  Units and precision for electrical units
     *  Colors and patterns of layers for display 

* Example of a Technology File: 

```
Technology  { 
  dielectric  = 3.7 
  unitTimeName  = "ns" 
  timePrecision  = 1000 
  unitLengthName  = "micron" 
  lengthPrecision  = 1000 
  gridResolution  = 5 
  unitVoltageName  = "v" 
  } 
... 
Layer  "m1" { 
  layerNumber  = 16 
  maskName   = "metal1" 
  pitch   = 0.56 
  defaultWidth  = 0.23 
  minWidth   = 0.23 
  minSpacing  = 0.23 

```

* ICC Design Planning Flow

![image](https://github.com/user-attachments/assets/d1d9948a-95cf-4571-b572-8eeb80d3d517)

#### Hierarchical Design Planning Flow
 
* The hierarchical design planning flow provides an efficient approach for managing large designs.
  
* By dividing the design into multiple blocks, different design teams can work on different blocks in parallel, from RTL through physical implementation.
  
* Working with smaller blocks and using multiply instantiated blocks can reduce overall runtime.

![image](https://github.com/user-attachments/assets/10159c8a-8ef3-4214-b3f7-cda11de315dd)

####  Design Planning at Multiple Levels of Physical Hierarchy

* Large, complex SoC designs require hierarchical layout methodologies capable of managing multiple levels of physical hierarchy at the same time. Many traditional design  tools -- including physical planning, place and route, and other tools -- are limited to two  levels of physical hierarchy: top and block.
  
* The IC Compiler II tool provides comprehensive support for designs with multiple levels of physical hierarchy, resulting in shorter time to  results, better QoR, and higher productivity for physical design teams.

* Use the `set_hierarchy_options` command to enable or disable specific blocks and design levels of hierarchy for planning. IC Compiler II provides support in several areas to accommodate designs with multiple 
levels of physical hierarchy:

#### Data Model

The data model in the IC Compiler II tool has built-in support for multiple levels of physical  hierarchy. Native physical hierarchy support provides significant advantages for multi-level physical hierarchy planning and implementation. When performing block shaping,  placement, routing, timing, and other steps, the tool can quickly access the specific data  relative to physical hierarchy needed to perform the function.

#### Block Shaping

In a complex design with multiple levels of physical hierarchy, the block shaper needs to  know the target area for each sub-chip, the aspect ratio constraints required by hard macro  children, and any interconnect that exists at the sibling-to-sibling, parent-to-child, and  child-to parent interfaces. For multi-voltage designs, the block shaper needs the target locations for voltage areas. These requirements add additional constraints for the shaper to  manage. For multi-level physical hierarchy planning, block shaping constraints on lower  level sub-chips must be propagated to the top level; these constraints take the form of block  shaping constraints on parent sub-chips. To improve performance, the shaper does not need the full netlist content that exists within each sub-chip or block.The IC Compiler II data model provides block shaping with the specific data required to  accomplish these goals. For multi-voltage designs, the tool reads UPF and saves the power  intent at the sub-chip level. The tool retrieves data from the data model to calculate targets  based on natural design utilization or retrieves user-defined attributes that specify design 
targets.

#### Cell and Macro Placement
 
After block shaping, the cell and macro placement function sees a global view of the  interconnect paths and data flow at the physical hierarchy boundaries and connectivity to macro cells. With this information, the tool places macros for each sub-chip at each level of  hierarchy. Because the tool understands the relative location requirements of interconnect  paths at the boundaries at all levels, sufficient resources at the adjacent sub-chip edges are  reserved to accommodate interconnect paths. The placer anticipates the needs of  hierarchical pin placement and places macros where interconnect paths do not require  significant buffering to drive signals across macros.
The placer models the external environment at the boundaries of both child and parent  sub-chips by considering sub-chip shapes, locations, and the global macro placements. Using this information, the placer creates cell placement jobs for each sub-chip at each level  of hierarchy. By delegating sub-chip placement across multiple processes, the tool minimizes turnaround time while maximizing the use of compute resources.

![image](https://github.com/user-attachments/assets/5602713d-92d4-4830-a16a-4591ba8e04f2)


#### Power Planning

For power planning, the IC Compiler II tool provides an innovative pattern-based methodology. Patterns describing construction rules -- widths, layers, and pitches required to form rings and meshes -- are applied to different areas of the floorplan such as voltage areas, groups of macros, and so on. Strategies associate single patterns or multiple patterns with areas. Given these strategy definitions, the IC Compiler II tool characterizes the power plan and automatically generates definitions of strategies for sub-chips at all levels. A complete power plan is generated in a distributed manner. Because the characterized strategies are written in terms of objects at each sub-chip level, power plans can be easily re-created to accommodate floorplan changes at any level.

![image](https://github.com/user-attachments/assets/ad9e78bd-ab4d-4f69-978f-19bedd83752b)

 
#### Pin Placement
 
With block shapes formed, macros placed, and power routed, pin placement retrieves interface data from all levels and invokes the global router to determine the optimal location to place hierarchical pins. The global router recognizes physical boundaries at all levels to ensure efficient use of resources at hierarchical pin interfaces. Pins are aligned across multiple levels when possible. Like all IC Compiler II operations, the global router comprehends multiply instantiated blocks (MIBs) and creates routes compliant with each MIB instantiation. To place pins for MIBs, the pin placement algorithm determines the best 
pin placement that works for all instances, ensuring that the pin placement on each instance is identical. Additionally, pin placement creates feedthroughs for all sub-chips, including MIBs, throughout the hierarchy. The global router creates feedthroughs across MIBs, determines feedthrough reuse, and connects unused feedthroughs to power or ground as required.

![image](https://github.com/user-attachments/assets/4a74f025-8781-45c4-9f1a-05686d41bb55)


#### Timing Budgeting

The IC Compiler II tool estimates the timing at hierarchical interfaces and creates timing budgets for sub-chips. The timing budgeter in IC Compiler II creates timing constraints for all child interface pins within the full chip, the parent and child interfaces for mid-level sub-chips and the primary pins at lowest level sub-chips. The entire design can proceed with placement and optimization concurrently and in a distributed manner.
To examine critical timing paths in the layout or perform other design planning tasks, you can interactively view, analyze, and manually edit any level of the design in a full-chip context. You can choose to view top-level only or multiple levels of hierarchy. When viewing multiple levels, interactive routing is performed as if the design is flat. At completion, routes are pushed into children and hierarchical pins are automatically added.

![image](https://github.com/user-attachments/assets/a5b31adf-453d-4f0b-bdc0-30d53908200b)

</details>

<details>
  <summary>RVMYTH Core Synthesis</summary>
<br>

* vsd.tcl

```

set target_library [list /home/vijayalaxmi/VSDBabySoC_ICC2/nangate_typical.db ]
set link_library [list  /home/vijayalaxmi/VSDBabySoC_ICC2/nangate_typical.db ] 
set symbol_library ""


read_verilog /home/vijayalaxmi/VSDBabySoC_ICC2/rvmyth.v



analyze -library WORK -format verilog {/home/vijayalaxmi/VSDBabySoC_ICC2/vsdbabysoc.v}
elaborate vsdbabysoc -architecture verilog -library WORK
analyze {}

create_clock -name MYCLK -per 10 [get_ports CLK];
set_clock_latency -source 2 [get_clocks MYCLK];
set_clock_latency 1 [get_clocks MYCLK];
set_clock_uncertainty -setup 0.5 [get_clocks MYCLK];
set_clock_uncertainty -hold 0.1 [get_clocks MYCLK];
set_input_delay -max 5 -clock [get_clocks MYCLK] [get_ports reset];
set_input_delay -max 5 -clock [get_clocks MYCLK] [get_ports CLK];
set_input_delay -min 1 -clock [get_clocks MYCLK] [get_ports reset];
set_input_delay -min 1 -clock [get_clocks MYCLK] [get_ports CLK];
set_input_transition -max 0.4 [get_ports reset];
set_input_transition -max 0.4 [get_ports CLK];
set_input_transition -min 0.1 [get_ports reset];
set_input_transition -min 0.1 [get_ports CLK];

set_load -max 0.4 [get_ports OUT];
set_load -min 0.1 [get_ports OUT];

check_design

compile_ultra

file mkdir report
write -hierarchy -format verilog -output /home/vijayalaxmi/VSDBabySoC_ICC2/report/rvmyth.v
write_sdc -nosplit -version 2.0 /home/vijayalaxmi/VSDBabySoC_ICC2/report/rvmyth.sdc
report_area -hierarchy > /home/vijayalaxmi/VSDBabySoC_ICC2/report/vsdbabysoc.area
report_timing > /home/vijayalaxmi/VSDBabySoC_ICC2/report/vsdbabysoc.timing
report_power -hierarchy > /home/vijayalaxmi/VSDBabySoC_ICC2/report/vsdbabysoc.power

gui_start

```

* Invoke dc_shell
  * csh
  * dc_shell
* source /home/vijayalaxmi/vsd.tcl

![image](https://github.com/user-attachments/assets/e288ec37-a8a1-4db0-885a-34f4300a5bbc)
![image](https://github.com/user-attachments/assets/1054b852-1a3c-4e99-9a85-4e0c32aff7d3)

## VSDBabySoC Area, Power & Timing Reports

#### Area Report

```

****************************************
Report : area
Design : vsdbabysoc
Version: T-2022.03-SP5-6
Date   : Sun Nov 24 12:30:53 2024
****************************************

Information: Updating design information... (UID-85)
Library(s) Used:

    NangateOpenCellLibrary (File: /home/vijayalaxmi/VSDBabySoC_ICC2/nangate_typical.db)

Number of ports:                           19
Number of nets:                          2781
Number of cells:                         2241
Number of combinational cells:           1562
Number of sequential cells:               678
Number of macros/black boxes:               0
Number of buf/inv:                        152
Number of references:                       3

Combinational area:               1941.268037
Buf/Inv area:                       96.823999
Noncombinational area:            3056.871889
Macro/Black Box area:                0.000000
Net Interconnect area:      undefined  (Wire load has zero net area)

Total cell area:                  4998.139926
Total area:                 undefined

Information: This design contains black box (unknown) components. (RPT-8)

Hierarchical area distribution
------------------------------

                                  Global cell area          Local cell area
                                  ------------------  ---------------------------- 
Hierarchical cell                 Absolute   Percent  Combi-     Noncombi-  Black-
                                  Total      Total    national   national   boxes   Design
--------------------------------  ---------  -------  ---------  ---------  ------  ---------
vsdbabysoc                        4998.1399    100.0     0.0000     0.0000  0.0000  vsdbabysoc
core                              4998.1399    100.0  1941.2680  3056.8719  0.0000  rvmyth
--------------------------------  ---------  -------  ---------  ---------  ------  ---------
Total                                                 1941.2680  3056.8719  0.0000

1

```

#### Power Report

```
 
****************************************
Report : power
        -hier
        -analysis_effort low
Design : vsdbabysoc
Version: T-2022.03-SP5-6
Date   : Sun Nov 24 12:30:53 2024
****************************************


Library(s) Used:

    NangateOpenCellLibrary (File: /home/vijayalaxmi/VSDBabySoC_ICC2/nangate_typical.db)


Operating Conditions: typical   Library: NangateOpenCellLibrary
Wire Load Model Mode: top

Design        Wire Load Model            Library
------------------------------------------------
vsdbabysoc             5K_hvratio_1_1    NangateOpenCellLibrary


Global Operating Voltage = 1.1  
Power-specific unit information :
    Voltage Units = 1V
    Capacitance Units = 1.000000ff
    Time Units = 1ns
    Dynamic Power Units = 1uW    (derived from V,C,T units)
    Leakage Power Units = 1nW


--------------------------------------------------------------------------------
                                       Switch   Int      Leak     Total
Hierarchy                              Power    Power    Power    Power    %
--------------------------------------------------------------------------------
vsdbabysoc                              111.666  249.102 1.01e+05  461.798 100.0
  core (rvmyth)                          36.668  249.102 1.01e+05  386.800  83.8
1

```

### Timing Report

```

****************************************
Report : timing
        -path full
        -delay max
        -max_paths 1
Design : vsdbabysoc
Version: T-2022.03-SP5-6
Date   : Sun Nov 24 12:30:53 2024
****************************************

Operating Conditions: typical   Library: NangateOpenCellLibrary
Wire Load Model Mode: top

  Startpoint: dac/OUT (internal pin)
  Endpoint: OUT (output port)
  Path Group: (none)
  Path Type: max

  Des/Clust/Port     Wire Load Model       Library
  ------------------------------------------------
  vsdbabysoc         5K_hvratio_1_1        NangateOpenCellLibrary

  Point                                    Incr       Path
  -----------------------------------------------------------
  dac/OUT (avsddac)                        0.00       0.00 r
  OUT (out)                                0.00       0.00 r
  data arrival time                                   0.00
  -----------------------------------------------------------
  (Path is unconstrained)


1

```

## Once the synthesis flow is run without errors, design_vision gui will be generated, here we can view the VSDBabySoC Schematic

![image](https://github.com/user-attachments/assets/3bdfbbe9-fd65-471f-8431-b5b2c483b3eb)
![image](https://github.com/user-attachments/assets/a9da1f2b-32ad-4914-8a45-ef611b2adf72)

## RVMYTH Core Schematic

![image](https://github.com/user-attachments/assets/46d691b2-a548-44ba-9523-df2b517e6b06)
![image](https://github.com/user-attachments/assets/b9c44005-d2ed-449f-b35d-82b609e2f791)
![image](https://github.com/user-attachments/assets/a2199231-e4ee-464e-92a8-ebe4317d573a)
![image](https://github.com/user-attachments/assets/dcad9c12-440f-49db-9914-f1e5b375b01a)

</details>
