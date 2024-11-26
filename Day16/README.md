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
  <summary>Lab: vsdbabysoc</summary>
<br>

#### Downloading Physical Design Collaterals:

* git clone https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd to download all the technology files (.techlef) for the Skywater 130nm PDK, along with all the .lef files for the standard cells.
* git clone https://github.com/bharath19-gs/synopsys_ICC2flow_130nm to download the technology files (.tf) for the Skywater 130nm PDK, as well as the RC Tech file (parasitics) in .itf format.
* git clone https://github.com/kunalg123/icc2_workshop_collaterals to obtain all the scripts necessary for setting up and executing the physical design flow in the ICC2 Compiler tool.


The ITF file is essential for parasitic extraction tools to create the RC parasitics necessary for analyzing timing, signal integrity, power, and reliability.

Moreover, the ITF file can also be utilized to produce TLU+ files, which are vital technology files in physical design.

To convert an .itf file to .tluplus format, follow these steps:

```

* cd `/home/vijayalaxmi/VSDBabySoC/synopsys_ICC2flow_130nm/synopsys_skywater_flow_nominal/itf_files`
* In Terminal,
    grdgenxo -itf2TLUPlus -i skywater130.nominal.itf -o skywater130.nominal.tluplus # to generate TLUplus RC Tech file from .itf file format using StarRC tool.

```

![image](https://github.com/user-attachments/assets/c4174a8f-7492-47d3-bf0c-ceddeadef6ee)

* synthesis.tcl

```

set target_library /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db
set link_library {* /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/avsdpll.db /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/avsddac.db}
set search_path {/home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/include /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/module}
read_file {sandpiper_gen.vh  sandpiper.vh  sp_default.vh  sp_verilog.vh clk_gate.v rvmyth.v rvmyth_gen.v vsdbabysoc.v} -autoread -top vsdbabysoc
link
read_sdc /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/sdc/vsdbabysoc_synthesis.sdc
compile_ultra
report_qor > /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/reports/qor_post_synth.rpt
report_area > /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/reports/area_post_synth.rpt
report_power > /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/reports/power_post_synth.rpt
write_file -format verilog -hierarchy -output /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/vsdbabysoc_net.v
write -f ddc -out /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/vsdbabysoc.ddc

start_gui

```

* Invoke dc_shell
  * csh
  * dc_shell
* source /home/vijayalaxmi/Desktop/VLSI/synthesis.tcl

![image](https://github.com/user-attachments/assets/e3c6222a-0b85-4aa6-8eb7-790a107cacc0)
![image](https://github.com/user-attachments/assets/eca343e5-0d46-4929-a6c7-f9220caf9e5c)


## VSDBabySoC Reports

#### QoR Report

```

Information: Updating design information... (UID-85)
 
****************************************
Report : qor
Design : vsdbabysoc
Version: T-2022.03-SP5-6
Date   : Tue Nov 26 12:47:22 2024
****************************************


  Timing Path Group 'clk'
  -----------------------------------
  Levels of Logic:              41.00
  Critical Path Length:         10.87
  Critical Path Slack:           0.00
  Critical Path Clk Period:     11.00
  Total Negative Slack:          0.00
  No. of Violating Paths:        0.00
  Worst Hold Violation:          0.00
  Total Hold Violation:          0.00
  No. of Hold Violations:        0.00
  -----------------------------------


  Cell Count
  -----------------------------------
  Hierarchical Cell Count:          1
  Hierarchical Port Count:         12
  Leaf Cell Count:               2539
  Buf/Inv Cell Count:             518
  Buf Cell Count:                   4
  Inv Cell Count:                 514
  CT Buf/Inv Cell Count:            0
  Combinational Cell Count:      1863
  Sequential Cell Count:          676
  Macro Count:                      0
  -----------------------------------


  Area
  -----------------------------------
  Combinational Area:    11173.215786
  Noncombinational Area: 13532.978775
  Buf/Inv Area:           1950.620739
  Total Buffer Area:            18.77
  Total Inverter Area:        1931.85
  Macro/Black Box Area:      0.000000
  Net Area:                  0.000000
  -----------------------------------
  Cell Area:             24706.194561
  Design Area:           24706.194561


  Design Rules
  -----------------------------------
  Total Number of Nets:          2579
  Nets With Violations:             0
  Max Trans Violations:             0
  Max Cap Violations:               0
  -----------------------------------


  Hostname: sfalvsd

  Compile CPU Statistics
  -----------------------------------------
  Resource Sharing:                    0.03
  Logic Optimization:                  2.02
  Mapping Optimization:                4.27
  -----------------------------------------
  Overall Compile Time:               19.77
  Overall Compile Wall Clock Time:    20.11

  --------------------------------------------------------------------

  Design  WNS: 0.00  TNS: 0.00  Number of Violating Paths: 0


  Design (Hold)  WNS: 0.00  TNS: 0.00  Number of Violating Paths: 0

  --------------------------------------------------------------------


1

```

#### Power Report

```
 
 
****************************************
Report : power
        -analysis_effort low
Design : vsdbabysoc
Version: T-2022.03-SP5-6
Date   : Tue Nov 26 12:47:22 2024
****************************************


Library(s) Used:

    sky130_fd_sc_hd__tt_025C_1v80 (File: /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db)
    avsddac (File: /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/avsddac.db)
    avsdpll (File: /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/avsdpll.db)


Operating Conditions: tt_025C_1v80   Library: sky130_fd_sc_hd__tt_025C_1v80
Wire Load Model Mode: top

Design        Wire Load Model            Library
------------------------------------------------
vsdbabysoc             Small             sky130_fd_sc_hd__tt_025C_1v80


Global Operating Voltage = 1.8  
Power-specific unit information :
    Voltage Units = 1V
    Capacitance Units = 1.000000pf
    Time Units = 1ns
    Dynamic Power Units = 1mW    (derived from V,C,T units)
    Leakage Power Units = 1nW


Attributes
----------
i - Including register clock pin internal power


  Cell Internal Power  =   2.6041 mW   (83%)
  Net Switching Power  = 536.1713 uW   (17%)
                         ---------
Total Dynamic Power    =   3.1402 mW  (100%)

Cell Leakage Power     =   8.0471 nW


                 Internal         Switching           Leakage            Total
Power Group      Power            Power               Power              Power   (   %    )  Attrs
--------------------------------------------------------------------------------------------------
io_pad             0.0000            0.0000            0.0000            0.0000  (   0.00%)
memory             0.0000            0.0000            0.0000            0.0000  (   0.00%)
black_box          0.0000            0.3975            0.0000            0.3975  (  12.66%)
clock_network      2.5022            0.0000            0.0000            2.5022  (  79.68%)  i
register       4.2197e-02        1.8358e-02            5.4668        6.0562e-02  (   1.93%)
sequential         0.0000            0.0000            0.0000            0.0000  (   0.00%)
combinational  5.9688e-02            0.1203            2.5803            0.1800  (   5.73%)
--------------------------------------------------------------------------------------------------
Total              2.6041 mW         0.5362 mW         8.0471 nW         3.1402 mW
1

```

### Area Report

```

 
****************************************
Report : area
Design : vsdbabysoc
Version: T-2022.03-SP5-6
Date   : Tue Nov 26 12:47:22 2024
****************************************

Library(s) Used:

    sky130_fd_sc_hd__tt_025C_1v80 (File: /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db)
    avsddac (File: /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/avsddac.db)
    avsdpll (File: /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/avsdpll.db)

Number of ports:                           19
Number of nets:                          2591
Number of cells:                         2540
Number of combinational cells:           1861
Number of sequential cells:               676
Number of macros/black boxes:               2
Number of buf/inv:                        518
Number of references:                       4

Combinational area:              11173.215786
Buf/Inv area:                     1950.620739
Noncombinational area:           13532.978775
Macro/Black Box area:                0.000000
Net Interconnect area:      undefined  (Wire load has zero net area)

Total cell area:                 24706.194561
Total area:                 undefined
1

```

## Once the synthesis flow is run without errors, design_vision gui will be generated, here we can view 

## VSDBabySoC Schematic

![image](https://github.com/user-attachments/assets/7f1bb72a-461d-4fcd-8c44-7f7ccee9ebcc)
![image](https://github.com/user-attachments/assets/54e344b9-9e1d-48a3-8217-da371274e1e6)


## RVMYTH Core Schematic

![image](https://github.com/user-attachments/assets/58c50b13-122e-4c5c-b105-a844d0714596)
![image](https://github.com/user-attachments/assets/41ee5ce4-79f2-4244-b738-64d723770361)
![image](https://github.com/user-attachments/assets/6fef96eb-f831-4582-875f-2e5ee3de924b)
![image](https://github.com/user-attachments/assets/6e1b42d2-4ced-4ee4-bd51-3401ffc8341c)


## Physical Design Flow

Collaterals can be configured using the following files located at the path 
/home/vijayalaxmi/Desktop/PD_flow/scripts:

compile_pg_example.tcl
init_design.mcmm_example.auto_expanded.tcl
init_design.read_parasitic_tech_example.tcl
init_design.tech_setup.tcl
pns_example.tcl
top.tcl
write_block_data.tcl



</details>
