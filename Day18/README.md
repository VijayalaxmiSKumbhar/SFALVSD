# VSDBabySoC ICC2 flow


## Physical Design Flow

Collaterals can be configured using the following files located at the path 
/home/vijayalaxmi/Desktop/pdflow:

* compile_pg_example.tcl

* init_design.mcmm_example.auto_expanded.tcl
  
* init_design.read_parasitic_tech_example.tcl

* init_design.tech_setup.tcl

* pns_example.tcl

* top.tcl

* write_block_data.tcl

##  `ICC2 Screenshots`

## `top.tcl` is excecuted using the following command in `icc2_shell`, .

* `source /home/vijayalaxmi/Desktop/pdflow/top.tcl`

![image](https://github.com/user-attachments/assets/aefc2be0-57f3-4597-b51b-4f05162ce414)
![image](https://github.com/user-attachments/assets/1abe63d2-4da5-41f9-ae0a-9d68057b2d33)
![image](https://github.com/user-attachments/assets/1c331586-9fae-4f5b-b8ef-e814fe58ddd5)
![image](https://github.com/user-attachments/assets/998d50de-fe70-4a1d-9090-e39c02bf885f)

## Type the command `start_gui` in `icc2_shell`, final layout can be observed:

![image](https://github.com/user-attachments/assets/531920c8-59c8-463c-89e5-3dbc590e168f)
![image](https://github.com/user-attachments/assets/76f945bc-2561-45c3-adf5-39bda767671e)
![image](https://github.com/user-attachments/assets/cad892f5-390c-476f-a788-55e75c1f410f)
![image](https://github.com/user-attachments/assets/88fa239f-110d-4367-b55f-94ca0463c1b8)


## Filler cells used

![image](https://github.com/user-attachments/assets/a58451f0-04d4-4419-8306-fc4e5b191013)
![image](https://github.com/user-attachments/assets/32790537-7bf5-4f7d-861d-0d10e0e5c7e7)


## Placement of VSDBabySoC

#### pre_placement check_design report 
`(/home/vijayalaxmi/Desktop/pdflow/rpts_icc2/place_pins/check_design.pre_pin_placement) :`

```
****************************************
 Report : check_design 
 Options: { dp_pre_pin_placement }
 Design : vsdbabysoc
 Version: T-2022.03-SP5
 Date   : Sat Jan 11 07:44:07 2025
****************************************

Running atomic-check 'dp_pre_pin_placement'

  *** EMS Message summary ***
  ----------------------------------------------------------------------------------------------------
  Total 0 EMS messages : 0 errors, 0 warnings, 0 info.
  ----------------------------------------------------------------------------------------------------

  *** Non-EMS message summary ***
  ----------------------------------------------------------------------------------------------------
  Rule         Type   Count      Message
  ----------------------------------------------------------------------------------------------------
  DPPA-268     Warn   2          Didn't find any enabled planning block for %s.
  DPPA-475     Warn   1          Detected dimension mismatch between the boundary and bbox, for b...
  ----------------------------------------------------------------------------------------------------
  Total 3 non-EMS messages : 0 errors, 3 warnings, 0 info.
  ----------------------------------------------------------------------------------------------------
Information: Non-EMS messages are saved into file 'check_design2025Jan11074407.log'.
1

```

#### pin_placement report 
`(/home/vijayalaxmi/Desktop/pdflow/rpts_icc2/place_pins/report_port_placement.rpt) :`

```

****************************************
Report : report_pin_placement
Design : vsdbabysoc
Version: T-2022.03-SP5
Date   : Sat Jan 11 07:44:07 2025
****************************************
block vsdbabysoc pin OUT layer met5 side 4 offset 626.64
block vsdbabysoc pin reset layer met4 side 3 offset 320.68
block vsdbabysoc pin VCO_IN layer met4 side 3 offset 942.6
block vsdbabysoc pin ENb_CP layer met5 side 2 offset 933.2
block vsdbabysoc pin ENb_VCO layer met5 side 2 offset 324.6
block vsdbabysoc pin REF layer met4 side 1 offset 932.36
block vsdbabysoc pin VREFH layer met4 side 1 offset 310.44

```

#### report_placement report

```

****************************************
Report : report_placement
Design : vsdbabysoc
Version: T-2022.03-SP5
Date   : Sat Jan 11 07:44:18 2025
****************************************
  ==================
  Note: Including violations of fixed cells or between fixed pairs of cells. 
        To ignore violations of / between fixed cells, enable -ignore_fixed. 
  ==================

  Wire length report (all)
  ==================
  wire length in design vsdbabysoc/init_dp: 80744.242 microns.
  wire length in design vsdbabysoc/init_dp (see through blk pins): 80744.242 microns.

  Physical hierarchy violations report
  ====================================
  Violations in design vsdbabysoc/init_dp:
     0 cells have placement violation.

  Voltage area violations report
  ====================================
  Voltage area placement violations in design vsdbabysoc/init_dp:
     0 cells placed outside the voltage area which they belong to.

  Hard macro to hard macro overlap report
  =======================================
  HM to HM overlaps in design vsdbabysoc/init_dp: 0
  ---------------------------------------
  Total hard macro to hard macro overlaps: 0

Information: Default error view vsdbabysoc_dpplace.err is created in GUI error browser. (DPP-054)
1

```

#### Timing report showing slack met with 0.97 value 
`(/home/vijayalaxmi/Desktop/pdflow/rpts_icc2/timing_estimation/vsdbabysoc.post_estimated_timing.rpt :`

```

****************************************
Report : timing
        -path_type full
        -delay_type max
        -max_paths 1
        -report_by design
Design : vsdbabysoc
Version: T-2022.03-SP5
Date   : Sat Jan 11 07:44:23 2025
****************************************

  Startpoint: core/CPU_is_addi_a3_reg (rising edge-triggered flip-flop clocked by clk)
  Endpoint: core/CPU_Xreg_value_a4_reg[26][30] (rising edge-triggered flip-flop clocked by clk)
  Mode: func1
  Corner: estimated_corner
  Scenario: func1::estimated_corner
  Path Group: clk
  Path Type: max

  Point                                            Incr      Path       Delta Incr     Analysis
  ----------------------------------------------------------------------------------------------------
  clock clk (rise edge)                            0.00      0.00
  clock network delay (ideal)                      0.00      0.00

  core/CPU_is_addi_a3_reg/CLK (sky130_fd_sc_hd__dfxtp_1)
                                                   0.00      0.00 r      0.00
  core/CPU_is_addi_a3_reg/Q (sky130_fd_sc_hd__dfxtp_1)
                                                   0.30      0.30 f      0.00        Size: None
  core/U474/Y (sky130_fd_sc_hd__nor2_1)            0.31      0.61 r      0.16
  core/U476/Y (sky130_fd_sc_hd__nand2_1)           0.06 e    0.67 f     -0.07        Size: sky130_fd_sc_hd__nand2_4
  core/U51/Y (sky130_fd_sc_hd__nand2_2)            0.50      1.17 r      0.02
  core/U478/X (sky130_fd_sc_hd__a22o_1)            0.34      1.51 r      0.09
  core/U479/X (sky130_fd_sc_hd__xor2_1)            0.20 e    1.71 f      0.09        Size: sky130_fd_sc_hd__xor2_4
  core/U569/Y (sky130_fd_sc_hd__a21oi_1)           0.25      1.96 r     -0.04
  core/U571/Y (sky130_fd_sc_hd__o21ai_1)           0.13      2.09 f     -0.00
  core/U574/Y (sky130_fd_sc_hd__a21oi_1)           0.24      2.33 r      0.00
  core/U576/Y (sky130_fd_sc_hd__o21ai_1)           0.14      2.47 f     -0.00
  core/U581/Y (sky130_fd_sc_hd__a21oi_1)           0.22      2.69 r     -0.00
  core/U583/Y (sky130_fd_sc_hd__o21ai_1)           0.24      2.93 f      0.00
  core/U587/Y (sky130_fd_sc_hd__a21oi_1)           0.28      3.21 r     -0.00
  core/U589/Y (sky130_fd_sc_hd__o21ai_1)           0.13      3.34 f     -0.00
  core/U344/Y (sky130_fd_sc_hd__a21oi_1)           0.22      3.56 r     -0.00
  core/U213/Y (sky130_fd_sc_hd__o21ai_1)           0.14      3.70 f     -0.00
  core/U343/Y (sky130_fd_sc_hd__a21oi_1)           0.23      3.93 r     -0.00
  core/U210/Y (sky130_fd_sc_hd__o21ai_1)           0.15      4.08 f      0.03
  core/U342/Y (sky130_fd_sc_hd__a21oi_1)           0.24      4.32 r      0.01
  core/U209/Y (sky130_fd_sc_hd__o21ai_1)           0.14      4.45 f      0.00
  core/U341/Y (sky130_fd_sc_hd__a21oi_1)           0.24      4.69 r     -0.00
  core/U215/Y (sky130_fd_sc_hd__o21ai_1)           0.13      4.83 f      0.00
  core/U96/X (sky130_fd_sc_hd__a21o_1)             0.18      5.01 f     -0.00
  core/U942/COUT (sky130_fd_sc_hd__fa_1)           0.41      5.42 f      0.00        Size: None
  core/U94/X (sky130_fd_sc_hd__a21o_1)             0.19      5.61 f     -0.00
  core/U905/COUT (sky130_fd_sc_hd__fa_1)           0.38      5.99 f     -0.00        Size: None
  core/U887/COUT (sky130_fd_sc_hd__fa_1)           0.39      6.37 f     -0.02        Size: None
  core/U1370/COUT (sky130_fd_sc_hd__fa_1)          0.26 e    6.63 f     -0.14        Size: sky130_fd_sc_hd__fah_1
  core/U36/COUT (sky130_fd_sc_hd__fa_2)            0.30 e    6.93 f     -0.07        Size: sky130_fd_sc_hd__fah_1
  core/U87/Y (sky130_fd_sc_hd__clkinv_1)           0.06      6.99 r      0.00
  core/U613/Y (sky130_fd_sc_hd__o21ai_1)           0.06      7.05 f     -0.01
  core/U352/COUT (sky130_fd_sc_hd__fa_1)           0.26 e    7.31 f     -0.13        Size: sky130_fd_sc_hd__fah_1
  core/U348/COUT (sky130_fd_sc_hd__fa_1)           0.27 e    7.58 f     -0.13        Size: sky130_fd_sc_hd__fah_1
  core/U35/COUT (sky130_fd_sc_hd__fa_1)            0.26 e    7.84 f     -0.13        Size: sky130_fd_sc_hd__fah_1
  core/U33/COUT (sky130_fd_sc_hd__fa_1)            0.30 e    8.14 f     -0.12        Size: sky130_fd_sc_hd__fah_1
  core/U81/X (sky130_fd_sc_hd__a21o_1)             0.19      8.33 f      0.00
  core/U347/COUT (sky130_fd_sc_hd__fa_1)           0.39      8.72 f     -0.00        Size: None
  core/U351/SUM (sky130_fd_sc_hd__fa_1)            0.57      9.29 r     -0.00        Size: None
  core/U3/Y (sky130_fd_sc_hd__nand2_1)             0.38      9.67 f      0.00
  core/U691/Y (sky130_fd_sc_hd__o22ai_1)           0.29      9.96 r     -0.03
  core/CPU_Xreg_value_a4_reg[26][30]/D (sky130_fd_sc_hd__dfxtp_1)
                                                   0.00 e    9.96 r      0.00
  data arrival time                                          9.96       -0.49        Delta arrival

  clock clk (rise edge)                           11.00     11.00
  clock network delay (ideal)                      0.00     11.00
  core/CPU_Xreg_value_a4_reg[26][30]/CLK (sky130_fd_sc_hd__dfxtp_1)
                                                   0.00     11.00 r      0.00
  library setup time                              -0.07     10.93
  data required time                                        10.93
  ----------------------------------------------------------------------------------------------------
  data required time                                        10.93
  data arrival time                                         -9.96
  ----------------------------------------------------------------------------------------------------
  slack (MET)                                                0.97


1


```

#### post-placement qor report 
`(/home/vijayalaxmi/Desktop/pdflow/rpts_icc2/timing_estimation/vsdbabysoc.post_estimated_timing.qor) :`

```

****************************************
Report : qor
Design : vsdbabysoc
Version: T-2022.03-SP5
Date   : Sat Jan 11 07:44:23 2025
****************************************


Scenario           'func1::estimated_corner'
Timing Path Group  'clk'
----------------------------------------
Levels of Logic:                     39
Critical Path Length:              9.96
Critical Path Slack:               0.97
Critical Path Clk Period:         11.00
Total Negative Slack:              0.00
No. of Violating Paths:               0
----------------------------------------


Cell Count
----------------------------------------
Hierarchical Cell Count:              1
Hierarchical Port Count:             14
Leaf Cell Count:                   2743
Buf/Inv Cell Count:                 578
Buf Cell Count:                       2
Inv Cell Count:                     576
CT Buf/Inv Cell Count:                0
Combinational Cell Count:          2067
   Single-bit Isolation Cell Count:                        0
   Multi-bit Isolation Cell Count:                         0
   Isolation Cell Banking Ratio:                           0.00%
   Single-bit Level Shifter Cell Count:                    0
   Multi-bit Level Shifter Cell Count:                     0
   Level Shifter Cell Banking Ratio:                       0.00%
   Single-bit ELS Cell Count:                              0
   Multi-bit ELS Cell Count:                               0
   ELS Cell Banking Ratio:                                 0.00%
Sequential Cell Count:              676
   Integrated Clock-Gating Cell Count:                     0
   Sequential Macro Cell Count:                            0
   Single-bit Sequential Cell Count:                       676
   Multi-bit Sequential Cell Count:                        0
   Sequential Cell Banking Ratio:                          0.00%
   BitsPerflop:                                            1.00
Macro Count:                          2
----------------------------------------


Area
----------------------------------------
Combinational Area:            11407.19
Noncombinational Area:         13532.98
Buf/Inv Area:                   2169.58
Total Buffer Area:                 7.51
Total Inverter Area:            2162.07
Macro/Black Box Area:         671652.37
Net Area:                             0
Net XLength:                   50337.65
Net YLength:                   49383.02
----------------------------------------
Cell Area (netlist):                         696592.54
Cell Area (netlist and physical only):       696592.55
Net Length:                    99720.67


Design Rules
----------------------------------------
Total Number of Nets:              2993
Nets with Violations:                43
Max Trans Violations:                26
Max Cap Violations:                  43
----------------------------------------

1

```

