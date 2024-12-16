# RVMYTH CORE

## Synthesis

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

![image](https://github.com/user-attachments/assets/32546bd1-5c28-4a2f-8330-694d324d3570)
![image](https://github.com/user-attachments/assets/cfd522b1-3f28-4f4b-a75f-e4aeaca10eeb)

## Schematic

![image](https://github.com/user-attachments/assets/082e16e8-8e96-4e7a-a396-018b5b0bab4b)
![image](https://github.com/user-attachments/assets/2b0a1d53-9c98-4549-ba44-336e018c1ab2)
![image](https://github.com/user-attachments/assets/22531272-b6fa-41e4-969d-9756fea352d5)
![image](https://github.com/user-attachments/assets/d2d725de-7bc2-4bc5-b9cf-cdcdc1ae61d4)

## Physical Design

#### The top.tcl script file that is run in the icc2_shell that generates the Final Layout. 

```
The steps includes:


###---NDM Library creation---###

###---Read Synthesized Verilog---###

## Technology setup for routing layer direction, offset, site default, and site symmetry.

###---Routing settings---###

####################################
# Check Design: Pre-Floorplanning
####################################

####################################
# Floorplanning
####################################

####################################
## PG Pin connections
#####################################

####################################
### Place IO
######################################

####################################
### Memory Placement
######################################

####################################
# Configure placement
####################################

########################################
## Read parasitic files
########################################

########################################
## Read constraints
########################################

####################################
# Fix all shaped blocks and macros
####################################

####################################
# Create Power
####################################

####################################
# Pin Placement
####################################

####################################
# Timing estimation
####################################

####################################
# Place, CTS, Route
####################################

```
![image](https://github.com/user-attachments/assets/8b1a665a-2b64-4e2a-b818-9380681b1b55)
![image](https://github.com/user-attachments/assets/3e818a5d-b10f-49d3-b365-96ca2d964d1a)

#### Once the `top.tcl` file is run, type `start_gui` in `icc2_shell`:

![image](https://github.com/user-attachments/assets/03103f7f-7a8b-4c41-a34e-c4893253e59d)
![image](https://github.com/user-attachments/assets/b3f824e9-9420-4b7e-bda6-0374d2f3b192)
![image](https://github.com/user-attachments/assets/31410229-fd5c-45eb-882a-912fe9fdc475)
![image](https://github.com/user-attachments/assets/73c6bf29-b302-4978-bafb-c312379df983)
![image](https://github.com/user-attachments/assets/09f744d0-4196-4452-af44-08bc50501be3)
![image](https://github.com/user-attachments/assets/b659394e-e5a6-4f74-8c36-ec424bdc694b)

## Outputs Generated

* Type `set_propagated_clock [all_clocks]` in `icc2_shell`:

![image](https://github.com/user-attachments/assets/f5a22d72-5bb9-4c47-a1bc-04c25d24acf6)

*  Type `report_timing` in `icc2_shell` and slack time is met as shown below:

![image](https://github.com/user-attachments/assets/6801f021-ab16-4eec-9534-0d082e94a253)
![image](https://github.com/user-attachments/assets/963d737c-25de-493f-a0e8-52f17834e40c)
![image](https://github.com/user-attachments/assets/bcb4383e-67d5-47ab-9456-d9d601b04018)

* Type `estimate_timing` in `icc2_shell`: 

![image](https://github.com/user-attachments/assets/54c9f0ff-47ca-410f-9dcf-49f9f12c95f9)
![image](https://github.com/user-attachments/assets/bd9abc38-5e2a-4685-91a4-a281b33ad1ca)


## Violations

* Type the following command in `icc2_shell` once the layout is generated:

`report_constraints -all_violators -nosplit -verbose -significant_digits 4 > violators.rpt`

![image](https://github.com/user-attachments/assets/196e76c3-809f-46e8-b797-24224acfaee6)

```

****************************************
Report : constraint
        -verbose
        -all_violators
Design : vsdbabysoc_1
Version: T-2022.03-SP5
Date   : Mon Dec 16 09:36:35 2024
****************************************

   late_timing
   -----------

No paths.

   early_timing
   -----------

Warning: Scenario func1::estimated_corner is not configured for hold analysis: skipping. (UIC-058)
Error: None of the specified scenarios are active for hold analysis. (UIC-057)
No paths.

   Mode: func1 Corner: estimated_corner
   Scenario: func1::estimated_corner
    Net: CLK
    max_transition       0.1985
  - Transition Time      0.4000
  --------------------------------
    Slack               -0.2015 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Transition     Transition        Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/cto_buf_drc_3129/A   0.1985   0.4000       -0.2015  (VIOLATED) 

    Net: core/n818
    max_transition       0.1985
  - Transition Time      0.2390
  --------------------------------
    Slack               -0.0404 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Transition     Transition        Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U189/ZN       0.1985         0.2390        -0.0404  (VIOLATED) 
     PIN : core/HFSBUF_2534_49/A   0.1985    0.2390        -0.0404  (VIOLATED) 
     PIN : core/U205/A2       0.1985         0.2390        -0.0404  (VIOLATED) 

    Net: core/ZBUF_1524_20
    max_transition       0.1985
  - Transition Time      0.2170
  --------------------------------
    Slack               -0.0184 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Transition     Transition        Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U1114/B1      0.1985         0.2170        -0.0184  (VIOLATED) 
     PIN : core/U1138/B1      0.1985         0.2170        -0.0184  (VIOLATED) 
     PIN : core/U1146/B1      0.1985         0.2170        -0.0184  (VIOLATED) 
     PIN : core/U1158/B1      0.1985         0.2170        -0.0184  (VIOLATED) 
     PIN : core/U1162/B1      0.1985         0.2170        -0.0184  (VIOLATED) 
     PIN : core/U1142/B1      0.1985         0.2170        -0.0184  (VIOLATED) 
     PIN : core/U1130/B1      0.1985         0.2168        -0.0182  (VIOLATED) 
     PIN : core/U1186/B1      0.1985         0.2168        -0.0182  (VIOLATED) 
     PIN : core/U1110/B1      0.1985         0.2167        -0.0182  (VIOLATED) 
     PIN : core/U1178/B1      0.1985         0.2167        -0.0182  (VIOLATED) 
     PIN : core/U1122/B1      0.1985         0.2165        -0.0179  (VIOLATED) 
     PIN : core/U1090/B1      0.1985         0.2163        -0.0178  (VIOLATED) 
     PIN : core/U1094/B1      0.1985         0.2161        -0.0176  (VIOLATED) 
     PIN : core/U1126/B1      0.1985         0.2161        -0.0176  (VIOLATED) 
     PIN : core/U1098/B1      0.1985         0.2161        -0.0176  (VIOLATED) 
     PIN : core/U1150/B1      0.1985         0.2157        -0.0172  (VIOLATED) 
     PIN : core/U1102/B1      0.1985         0.2157        -0.0172  (VIOLATED) 
     PIN : core/U1134/B1      0.1985         0.2153        -0.0168  (VIOLATED) 
     PIN : core/U1118/B1      0.1985         0.2149        -0.0164  (VIOLATED) 
     PIN : core/U1170/B1      0.1985         0.2146        -0.0161  (VIOLATED) 

    Net: core/ZBUF_2495_340
    max_transition       0.1985
  - Transition Time      0.2032
  --------------------------------
    Slack               -0.0047 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Transition     Transition        Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U435/A1       0.1985         0.2032        -0.0047  (VIOLATED) 
     PIN : core/U661/B1       0.1985         0.2030        -0.0045  (VIOLATED) 
     PIN : core/U556/A1       0.1985         0.2030        -0.0045  (VIOLATED) 
     PIN : core/U706/B1       0.1985         0.2030        -0.0045  (VIOLATED) 
     PIN : core/U676/B1       0.1985         0.2029        -0.0044  (VIOLATED) 
     PIN : core/U480/A1       0.1985         0.2028        -0.0043  (VIOLATED) 
     PIN : core/U511/B1       0.1985         0.2028        -0.0043  (VIOLATED) 
     PIN : core/U586/B1       0.1985         0.2026        -0.0041  (VIOLATED) 
     PIN : core/U405/A1       0.1985         0.2026        -0.0040  (VIOLATED) 
     PIN : core/U541/A1       0.1985         0.2025        -0.0040  (VIOLATED) 
     PIN : core/U616/A1       0.1985         0.2022        -0.0037  (VIOLATED) 
     PIN : core/U450/B1       0.1985         0.2022        -0.0037  (VIOLATED) 
     PIN : core/U691/B1       0.1985         0.2022        -0.0037  (VIOLATED) 
     PIN : core/U496/B1       0.1985         0.2021        -0.0035  (VIOLATED) 
     PIN : core/U646/A1       0.1985         0.2019        -0.0034  (VIOLATED) 
     PIN : core/U631/A1       0.1985         0.2017        -0.0032  (VIOLATED) 
     PIN : core/U601/A1       0.1985         0.2015        -0.0029  (VIOLATED) 
     PIN : core/U420/A1       0.1985         0.2014        -0.0028  (VIOLATED) 
     PIN : core/U1046/A1      0.1985         0.2006        -0.0020  (VIOLATED) 
     PIN : core/U390/A1       0.1985         0.2005        -0.0020  (VIOLATED) 
     PIN : core/U722/B1       0.1985         0.2005        -0.0020  (VIOLATED) 
     PIN : core/U465/B1       0.1985         0.2005        -0.0020  (VIOLATED) 
     PIN : core/U571/A1       0.1985         0.2000        -0.0015  (VIOLATED) 

  ---------------------------------------------------------------------------
   Number of max_transition violation(s): 4

   Mode: func1 Corner: estimated_corner
   Scenario: func1::estimated_corner
    Net: core/HFSNET_47
    max_capacitance    121.4600
  - Capacitance        258.0628
  --------------------------------
    Slack              -136.6028 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/HFSBUF_2879_52/Z 121.4600  258.0628       -136.6028 (VIOLATED) 

    Net: core/ZBUF_4172_711
    max_capacitance    181.8850
  - Capacitance        279.6522
  --------------------------------
    Slack              -97.7672 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_4172_inst_2084/Z 181.8850 279.6522   -97.7672  (VIOLATED) 

    Net: core/HFSNET_64
    max_capacitance    121.4600
  - Capacitance        218.1522
  --------------------------------
    Slack              -96.6922 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/HFSBUF_3043_71/Z 121.4600  218.1522       -96.6922  (VIOLATED) 

    Net: core/HFSNET_72
    max_capacitance    121.4600
  - Capacitance        208.7818
  --------------------------------
    Slack              -87.3218 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/HFSBUF_2794_79/Z 121.4600  208.7818       -87.3218  (VIOLATED) 

    Net: core/HFSNET_70
    max_capacitance    121.4600
  - Capacitance        199.0697
  --------------------------------
    Slack              -77.6097 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/HFSBUF_2361_77/Z 121.4600  199.0697       -77.6097  (VIOLATED) 

    Net: core/ZBUF_3856_373
    max_capacitance    181.8850
  - Capacitance        253.5021
  --------------------------------
    Slack              -71.6171 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_3856_inst_1449/Z 181.8850 253.5021   -71.6171  (VIOLATED) 

    Net: core/ZBUF_853_473
    max_capacitance    121.4600
  - Capacitance        187.3765
  --------------------------------
    Slack              -65.9165 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_853_inst_1680/Z 121.4600 187.3765    -65.9165  (VIOLATED) 

    Net: core/HFSNET_61
    max_capacitance    121.4600
  - Capacitance        183.6065
  --------------------------------
    Slack              -62.1465 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/HFSINV_255_66/ZN 121.4600  183.6065       -62.1465  (VIOLATED) 

    Net: core/HFSNET_56
    max_capacitance    121.4600
  - Capacitance        182.6649
  --------------------------------
    Slack              -61.2049 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/HFSINV_1928_61/ZN 121.4600 182.6649       -61.2049  (VIOLATED) 

    Net: core/ZBUF_3659_418
    max_capacitance    121.4600
  - Capacitance        180.5956
  --------------------------------
    Slack              -59.1355 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_3659_inst_1547/Z 121.4600 180.5956   -59.1355  (VIOLATED) 

    Net: core/ZBUF_9442_514
    max_capacitance    121.4600
  - Capacitance        178.8056
  --------------------------------
    Slack              -57.3456 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_9442_inst_1755/Z 121.4600 178.8056   -57.3456  (VIOLATED) 

    Net: core/HFSNET_57
    max_capacitance    181.8850
  - Capacitance        237.0883
  --------------------------------
    Slack              -55.2033 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/HFSBUF_2079_62/Z 181.8850  237.0883       -55.2033  (VIOLATED) 

    Net: core/ZBUF_16801_292
    max_capacitance    121.4600
  - Capacitance        175.7567
  --------------------------------
    Slack              -54.2967 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_16801_inst_1217/Z 121.4600 175.7567  -54.2967  (VIOLATED) 

    Net: core/ZBUF_1866_483
    max_capacitance    181.8850
  - Capacitance        234.3966
  --------------------------------
    Slack              -52.5116 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_1866_inst_1706/Z 181.8850 234.3966   -52.5116  (VIOLATED) 

    Net: core/ZBUF_254_418
    max_capacitance    181.8850
  - Capacitance        221.9342
  --------------------------------
    Slack              -40.0492 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_254_inst_1549/Z 181.8850 221.9342    -40.0492  (VIOLATED) 

    Net: core/ZBUF_23837_345
    max_capacitance    121.4600
  - Capacitance        159.4049
  --------------------------------
    Slack              -37.9449 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_23837_inst_1362/Z 121.4600 159.4049  -37.9449  (VIOLATED) 

    Net: core/n304
    max_capacitance     60.7300
  - Capacitance         97.4469
  --------------------------------
    Slack              -36.7169 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U46/ZN       60.7300        97.4469       -36.7169  (VIOLATED) 

    Net: core/n954
    max_capacitance     60.5774
  - Capacitance         92.6322
  --------------------------------
    Slack              -32.0548 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U235/ZN      60.5774        92.6322       -32.0548  (VIOLATED) 

    Net: core/n908
    max_capacitance     59.3567
  - Capacitance         90.3705
  --------------------------------
    Slack              -31.0138 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U503/ZN      59.3567        90.3705       -31.0138  (VIOLATED) 

    Net: core/ZBUF_1083_964
    max_capacitance    121.4600
  - Capacitance        150.1109
  --------------------------------
    Slack              -28.6509 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_1083_inst_2585/Z 121.4600 150.1109   -28.6509  (VIOLATED) 

    Net: core/ZBUF_1679_964
    max_capacitance    181.8850
  - Capacitance        209.7497
  --------------------------------
    Slack              -27.8648 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_1679_inst_2586/Z 181.8850 209.7497   -27.8648  (VIOLATED) 

    Net: core/n911
    max_capacitance     59.3567
  - Capacitance         86.6734
  --------------------------------
    Slack              -27.3167 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U472/ZN      59.3567        86.6734       -27.3167  (VIOLATED) 

    Net: core/n898
    max_capacitance     60.7300
  - Capacitance         87.2992
  --------------------------------
    Slack              -26.5692 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U1247/Z      60.7300        87.2992       -26.5692  (VIOLATED) 

    Net: core/ZBUF_6644_625
    max_capacitance    181.8850
  - Capacitance        208.0733
  --------------------------------
    Slack              -26.1883 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_6644_inst_1934/Z 181.8850 208.0733   -26.1883  (VIOLATED) 

    Net: core/ZBUF_3868_442
    max_capacitance    121.4600
  - Capacitance        145.6003
  --------------------------------
    Slack              -24.1403 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_3868_inst_1606/Z 121.4600 145.6003   -24.1403  (VIOLATED) 

    Net: core/ZBUF_5951_25
    max_capacitance     60.7300
  - Capacitance         84.7452
  --------------------------------
    Slack              -24.0152 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_5951_inst_461/Z  60.7300  84.7452    -24.0152  (VIOLATED) 

    Net: core/ZBUF_777_452
    max_capacitance     60.7300
  - Capacitance         80.3050
  --------------------------------
    Slack              -19.5750 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_777_inst_1623/Z  60.7300  80.3050    -19.5750  (VIOLATED) 

    Net: core/n520
    max_capacitance     26.7029
  - Capacitance         45.5425
  --------------------------------
    Slack              -18.8396 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U195/ZN      26.7029        45.5425       -18.8396  (VIOLATED) 

    Net: core/ZBUF_6988_570
    max_capacitance    181.8850
  - Capacitance        200.3784
  --------------------------------
    Slack              -18.4934 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_6988_inst_1854/Z 181.8850 200.3784   -18.4934  (VIOLATED) 

    Net: core/n989
    max_capacitance     58.3649
  - Capacitance         76.8474
  --------------------------------
    Slack              -18.4825 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U1504/ZN     58.3649        76.8474       -18.4825  (VIOLATED) 

    Net: core/ZBUF_394_988
    max_capacitance     60.7300
  - Capacitance         79.1022
  --------------------------------
    Slack              -18.3722 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_394_inst_2730/Z  60.7300  79.1022    -18.3722  (VIOLATED) 

    Net: core/n711
    max_capacitance     26.7029
  - Capacitance         44.0580
  --------------------------------
    Slack              -17.3551 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U134/ZN      26.7029        44.0580       -17.3551  (VIOLATED) 

    Net: core/HFSNET_44
    max_capacitance    181.8850
  - Capacitance        198.8915
  --------------------------------
    Slack              -17.0065 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/HFSBUF_2534_49/Z 181.8850  198.8915       -17.0065  (VIOLATED) 

    Net: core/n818
    max_capacitance     16.0217
  - Capacitance         31.8456
  --------------------------------
    Slack              -15.8239 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U189/ZN      16.0217        31.8456       -15.8239  (VIOLATED) 

    Net: core/gre_net_120
    max_capacitance     60.7300
  - Capacitance         74.6768
  --------------------------------
    Slack              -13.9468 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3395/Z  60.7300  74.6768      -13.9468  (VIOLATED) 

    Net: core/ZBUF_566_105
    max_capacitance     60.7300
  - Capacitance         74.4313
  --------------------------------
    Slack              -13.7013 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_566_inst_665/Z  60.7300  74.4313     -13.7013  (VIOLATED) 

    Net: core/gre_net_174
    max_capacitance     60.7300
  - Capacitance         73.9109
  --------------------------------
    Slack              -13.1809 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3449/Z  60.7300  73.9109      -13.1809  (VIOLATED) 

    Net: core/gre_net_167
    max_capacitance     60.7300
  - Capacitance         73.4589
  --------------------------------
    Slack              -12.7289 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3442/Z  60.7300  73.4589      -12.7289  (VIOLATED) 

    Net: core/ZBUF_1524_542
    max_capacitance     60.7300
  - Capacitance         73.3515
  --------------------------------
    Slack              -12.6215 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_1524_inst_1808/Z  60.7300  73.3515   -12.6215  (VIOLATED) 

    Net: core/ZBUF_406_977
    max_capacitance    121.4600
  - Capacitance        134.0693
  --------------------------------
    Slack              -12.6093 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_406_inst_2646/Z 121.4600 134.0693    -12.6093  (VIOLATED) 

    Net: core/n957
    max_capacitance     59.3567
  - Capacitance         71.6000
  --------------------------------
    Slack              -12.2433 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ctmTdsLR_1_3224/ZN  59.3567  71.6000      -12.2433  (VIOLATED) 

    Net: core/ZBUF_69_473
    max_capacitance     60.7300
  - Capacitance         72.4214
  --------------------------------
    Slack              -11.6914 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_69_inst_1679/Z  60.7300  72.4214     -11.6914  (VIOLATED) 

    Net: core/n928
    max_capacitance     59.3567
  - Capacitance         71.0285
  --------------------------------
    Slack              -11.6718 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U1203/ZN     59.3567        71.0285       -11.6718  (VIOLATED) 

    Net: core/ZBUF_35_65
    max_capacitance     60.7300
  - Capacitance         72.3275
  --------------------------------
    Slack              -11.5975 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_35_inst_543/Z  60.7300  72.3275      -11.5975  (VIOLATED) 

    Net: core/ZBUF_1201_942
    max_capacitance    242.3100
  - Capacitance        253.6856
  --------------------------------
    Slack              -11.3756 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_1201_inst_2461/Z 242.3100 253.6856   -11.3756  (VIOLATED) 

    Net: core/gre_net_230
    max_capacitance     60.7300
  - Capacitance         71.9788
  --------------------------------
    Slack              -11.2488 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3554/Z  60.7300  71.9788      -11.2488  (VIOLATED) 

    Net: core/gre_net_122
    max_capacitance     60.7300
  - Capacitance         71.4517
  --------------------------------
    Slack              -10.7217 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3397/Z  60.7300  71.4517      -10.7217  (VIOLATED) 

    Net: core/n782
    max_capacitance     24.6048
  - Capacitance         35.1680
  --------------------------------
    Slack              -10.5632 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U1015/ZN     24.6048        35.1680       -10.5632  (VIOLATED) 

    Net: core/n804
    max_capacitance     26.7029
  - Capacitance         37.1911
  --------------------------------
    Slack              -10.4882 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U145/ZN      26.7029        37.1911       -10.4882  (VIOLATED) 

    Net: core/gre_net_149
    max_capacitance     60.7300
  - Capacitance         70.8989
  --------------------------------
    Slack              -10.1689 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3424/Z  60.7300  70.8989      -10.1689  (VIOLATED) 

    Net: core/n654
    max_capacitance     24.6048
  - Capacitance         34.6515
  --------------------------------
    Slack              -10.0467 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U824/ZN      24.6048        34.6515       -10.0467  (VIOLATED) 

    Net: core/n953
    max_capacitance     26.7029
  - Capacitance         36.7121
  --------------------------------
    Slack              -10.0092 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U55/ZN       26.7029        36.7121       -10.0092  (VIOLATED) 

    Net: core/gre_net_144
    max_capacitance     60.7300
  - Capacitance         70.6684
  --------------------------------
    Slack               -9.9384 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3419/Z  60.7300  70.6684       -9.9384  (VIOLATED) 

    Net: core/ZBUF_2060_542
    max_capacitance    181.8850
  - Capacitance        191.7551
  --------------------------------
    Slack               -9.8701 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_2060_inst_1809/Z 181.8850 191.7551    -9.8701  (VIOLATED) 

    Net: core/gre_net_244
    max_capacitance     60.7300
  - Capacitance         69.7201
  --------------------------------
    Slack               -8.9901 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3568/Z  60.7300  69.7201       -8.9901  (VIOLATED) 

    Net: core/gre_a_BUF_13_0
    max_capacitance     60.7300
  - Capacitance         69.5204
  --------------------------------
    Slack               -8.7904 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_a_BUF_13_inst_3500/Z  60.7300  69.5204  -8.7904 (VIOLATED) 

    Net: core/ZBUF_333_154
    max_capacitance     60.7300
  - Capacitance         69.3369
  --------------------------------
    Slack               -8.6069 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_333_inst_849/Z  60.7300  69.3369      -8.6069  (VIOLATED) 

    Net: core/gre_net_121
    max_capacitance     60.7300
  - Capacitance         69.1851
  --------------------------------
    Slack               -8.4551 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3396/Z  60.7300  69.1851       -8.4551  (VIOLATED) 

    Net: core/HFSNET_24
    max_capacitance    121.4600
  - Capacitance        129.4665
  --------------------------------
    Slack               -8.0065 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/HFSBUF_1952_29/Z 121.4600  129.4665        -8.0065  (VIOLATED) 

    Net: core/ZBUF_577_982
    max_capacitance    242.3100
  - Capacitance        250.2217
  --------------------------------
    Slack               -7.9117 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_577_inst_2692/Z 242.3100 250.2217     -7.9117  (VIOLATED) 

    Net: core/n955
    max_capacitance     59.3567
  - Capacitance         67.2427
  --------------------------------
    Slack               -7.8860 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ctmTdsLR_1_3303/ZN  59.3567  67.2427       -7.8860  (VIOLATED) 

    Net: core/n923
    max_capacitance     60.4248
  - Capacitance         68.0790
  --------------------------------
    Slack               -7.6542 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U1235/ZN     60.4248        68.0790        -7.6542  (VIOLATED) 

    Net: core/n971
    max_capacitance     60.5774
  - Capacitance         68.0125
  --------------------------------
    Slack               -7.4351 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U26/ZN       60.5774        68.0125        -7.4351  (VIOLATED) 

    Net: core/ZBUF_386_968
    max_capacitance     60.7300
  - Capacitance         68.0955
  --------------------------------
    Slack               -7.3655 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_386_inst_2606/Z  60.7300  68.0955     -7.3655  (VIOLATED) 

    Net: core/n939
    max_capacitance     53.4058
  - Capacitance         60.7081
  --------------------------------
    Slack               -7.3023 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U109/ZN      53.4058        60.7081        -7.3023  (VIOLATED) 

    Net: core/HFSNET_35
    max_capacitance    181.8850
  - Capacitance        188.9620
  --------------------------------
    Slack               -7.0770 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/HFSBUF_2250_40/Z 181.8850  188.9620        -7.0770  (VIOLATED) 

    Net: core/ZBUF_51_136
    max_capacitance     60.7300
  - Capacitance         67.6272
  --------------------------------
    Slack               -6.8972 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_51_inst_782/Z  60.7300  67.6272       -6.8972  (VIOLATED) 

    Net: core/n371_CDR1
    max_capacitance     24.6048
  - Capacitance         31.4539
  --------------------------------
    Slack               -6.8491 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U462/ZN      24.6048        31.4539        -6.8491  (VIOLATED) 

    Net: core/n558
    max_capacitance     26.7029
  - Capacitance         33.2348
  --------------------------------
    Slack               -6.5319 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U375/ZN      26.7029        33.2348        -6.5319  (VIOLATED) 

    Net: core/ZBUF_179_25
    max_capacitance     60.7300
  - Capacitance         67.1558
  --------------------------------
    Slack               -6.4258 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_179_inst_3109/Z  60.7300  67.1558     -6.4258  (VIOLATED) 

    Net: core/gre_net_250
    max_capacitance     60.7300
  - Capacitance         67.0643
  --------------------------------
    Slack               -6.3343 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3574/Z  60.7300  67.0643       -6.3343  (VIOLATED) 

    Net: core/n789
    max_capacitance     60.5774
  - Capacitance         66.6606
  --------------------------------
    Slack               -6.0832 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ctmTdsLR_1_3220/ZN  60.5774  66.6606       -6.0832  (VIOLATED) 

    Net: core/n783
    max_capacitance     24.6048
  - Capacitance         30.6681
  --------------------------------
    Slack               -6.0633 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U1014/ZN     24.6048        30.6681        -6.0633  (VIOLATED) 

    Net: core/HFSNET_62
    max_capacitance    242.9200
  - Capacitance        248.8139
  --------------------------------
    Slack               -5.8939 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/HFSINV_222_68/ZN 242.9200  248.8139        -5.8939  (VIOLATED) 

    Net: core/ZBUF_2_733
    max_capacitance     60.7300
  - Capacitance         66.3206
  --------------------------------
    Slack               -5.5906 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_2_inst_2115/Z  60.7300  66.3206       -5.5906  (VIOLATED) 

    Net: core/gre_net_195
    max_capacitance     60.7300
  - Capacitance         66.2587
  --------------------------------
    Slack               -5.5287 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3470/Z  60.7300  66.2587       -5.5287  (VIOLATED) 

    Net: core/n880
    max_capacitance     26.7029
  - Capacitance         31.7003
  --------------------------------
    Slack               -4.9974 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U1189/ZN     26.7029        31.7003        -4.9974  (VIOLATED) 

    Net: core/ZBUF_2_683
    max_capacitance     60.7300
  - Capacitance         65.6391
  --------------------------------
    Slack               -4.9091 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_2_inst_2026/Z  60.7300  65.6391       -4.9091  (VIOLATED) 

    Net: core/n986
    max_capacitance     59.3567
  - Capacitance         64.1381
  --------------------------------
    Slack               -4.7814 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U1265/ZN     59.3567        64.1381        -4.7814  (VIOLATED) 

    Net: core/n482_CDR1
    max_capacitance     24.6048
  - Capacitance         29.3627
  --------------------------------
    Slack               -4.7579 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U613/ZN      24.6048        29.3627        -4.7579  (VIOLATED) 

    Net: core/gre_net_148
    max_capacitance     60.7300
  - Capacitance         65.4504
  --------------------------------
    Slack               -4.7204 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3423/Z  60.7300  65.4504       -4.7204  (VIOLATED) 

    Net: core/ZBUF_54_964
    max_capacitance     60.7300
  - Capacitance         65.3679
  --------------------------------
    Slack               -4.6379 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_54_inst_2591/Z  60.7300  65.3679      -4.6379  (VIOLATED) 

    Net: core/gre_net_142
    max_capacitance     60.7300
  - Capacitance         65.3060
  --------------------------------
    Slack               -4.5760 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3417/Z  60.7300  65.3060       -4.5760  (VIOLATED) 

    Net: core/ZBUF_181_201
    max_capacitance     60.7300
  - Capacitance         65.2992
  --------------------------------
    Slack               -4.5692 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_181_inst_983/Z  60.7300  65.2992      -4.5692  (VIOLATED) 

    Net: core/ZBUF_186_431
    max_capacitance     60.7300
  - Capacitance         65.2508
  --------------------------------
    Slack               -4.5208 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_186_inst_1577/Z  60.7300  65.2508     -4.5208  (VIOLATED) 

    Net: core/gre_net_247
    max_capacitance     60.7300
  - Capacitance         65.0206
  --------------------------------
    Slack               -4.2906 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3571/Z  60.7300  65.0206       -4.2906  (VIOLATED) 

    Net: core/ZBUF_386_973
    max_capacitance     60.7300
  - Capacitance         64.8377
  --------------------------------
    Slack               -4.1077 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_386_inst_2622/Z  60.7300  64.8377     -4.1077  (VIOLATED) 

    Net: core/ZBUF_2_704
    max_capacitance     60.7300
  - Capacitance         64.3586
  --------------------------------
    Slack               -3.6286 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_2_inst_2068/Z  60.7300  64.3586       -3.6286  (VIOLATED) 

    Net: core/n887
    max_capacitance    237.4270
  - Capacitance        241.0478
  --------------------------------
    Slack               -3.6208 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U742/ZN     237.4270       241.0478        -3.6208  (VIOLATED) 

    Net: core/CPU_Xreg_value_a4[24][28]
    max_capacitance     60.7300
  - Capacitance         64.2940
  --------------------------------
    Slack               -3.5640 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[24][28]/Q  60.7300  64.2940  -3.5640 (VIOLATED)

    Net: core/ZBUF_1566_48
    max_capacitance     60.7300
  - Capacitance         64.1259
  --------------------------------
    Slack               -3.3959 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_1566_inst_513/Z  60.7300  64.1259     -3.3959  (VIOLATED) 

    Net: core/ZBUF_181_94
    max_capacitance     60.7300
  - Capacitance         64.1138
  --------------------------------
    Slack               -3.3838 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_181_inst_631/Z  60.7300  64.1138      -3.3838  (VIOLATED) 

    Net: core/ZBUF_386_938
    max_capacitance     60.7300
  - Capacitance         63.8596
  --------------------------------
    Slack               -3.1296 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_386_inst_2437/Z  60.7300  63.8596     -3.1296  (VIOLATED) 

    Net: core/CPU_src2_value_a3[22]
    max_capacitance     60.7300
  - Capacitance         63.8003
  --------------------------------
    Slack               -3.0703 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_src2_value_a3_reg[22]/Q  60.7300  63.8003  -3.0703 (VIOLATED)

    Net: core/gre_net_251
    max_capacitance     60.7300
  - Capacitance         63.5372
  --------------------------------
    Slack               -2.8072 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3575/Z  60.7300  63.5372       -2.8072  (VIOLATED) 

    Net: core/CPU_Xreg_value_a4[25][4]
    max_capacitance     60.7300
  - Capacitance         63.5026
  --------------------------------
    Slack               -2.7726 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[25][4]/Q  60.7300  63.5026  -2.7726 (VIOLATED)

    Net: core/gre_net_242
    max_capacitance     60.7300
  - Capacitance         63.4770
  --------------------------------
    Slack               -2.7470 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3566/Z  60.7300  63.4770       -2.7470  (VIOLATED) 

    Net: core/CPU_Xreg_value_a4[2][19]
    max_capacitance     60.7300
  - Capacitance         63.4661
  --------------------------------
    Slack               -2.7361 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[2][19]/Q  60.7300  63.4661  -2.7361 (VIOLATED)

    Net: core/n1423
    max_capacitance     60.2722
  - Capacitance         62.9262
  --------------------------------
    Slack               -2.6540 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[17][16]/QN  60.2722  62.9262  -2.6540 (VIOLATED)

    Net: core/n1122
    max_capacitance     60.2722
  - Capacitance         62.8513
  --------------------------------
    Slack               -2.5791 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[9][23]/QN  60.2722  62.8513  -2.5791 (VIOLATED)

    Net: core/n1349
    max_capacitance     60.2722
  - Capacitance         62.8150
  --------------------------------
    Slack               -2.5428 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[19][26]/QN  60.2722  62.8150  -2.5428 (VIOLATED)

    Net: core/ZBUF_386_950
    max_capacitance     60.7300
  - Capacitance         63.2540
  --------------------------------
    Slack               -2.5240 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_386_inst_2510/Z  60.7300  63.2540     -2.5240  (VIOLATED) 

    Net: core/n1434
    max_capacitance     60.2722
  - Capacitance         62.7000
  --------------------------------
    Slack               -2.4278 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[17][27]/QN  60.2722  62.7000  -2.4278 (VIOLATED)

    Net: core/gre_net_220
    max_capacitance     60.7300
  - Capacitance         63.0658
  --------------------------------
    Slack               -2.3358 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3544/Z  60.7300  63.0658       -2.3358  (VIOLATED) 

    Net: core/CPU_imm_a3[25]
    max_capacitance     60.7300
  - Capacitance         63.0405
  --------------------------------
    Slack               -2.3105 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_imm_a3_reg[25]/Q  60.7300  63.0405     -2.3105  (VIOLATED) 

    Net: core/n409_CDR1
    max_capacitance     14.4959
  - Capacitance         16.7975
  --------------------------------
    Slack               -2.3016 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U513/ZN      14.4959        16.7975        -2.3016  (VIOLATED) 

    Net: core/CPU_imm_a1[10]
    max_capacitance     28.9917
  - Capacitance         31.1356
  --------------------------------
    Slack               -2.1439 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U64/ZN       28.9917        31.1356        -2.1439  (VIOLATED) 

    Net: core/CPU_Xreg_value_a4[9][17]
    max_capacitance     60.7300
  - Capacitance         62.7183
  --------------------------------
    Slack               -1.9883 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[9][17]/Q  60.7300  62.7183  -1.9883 (VIOLATED)

    Net: core/ZBUF_2_773
    max_capacitance     60.7300
  - Capacitance         62.7097
  --------------------------------
    Slack               -1.9797 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_2_inst_2186/Z  60.7300  62.7097       -1.9797  (VIOLATED) 

    Net: core/ZBUF_736_459
    max_capacitance    181.8850
  - Capacitance        183.8634
  --------------------------------
    Slack               -1.9784 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_736_inst_1646/Z 181.8850 183.8634     -1.9784  (VIOLATED) 

    Net: core/ZBUF_4932_25
    max_capacitance     60.7300
  - Capacitance         62.5619
  --------------------------------
    Slack               -1.8319 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_4932_inst_464/Z  60.7300  62.5619     -1.8319  (VIOLATED) 

    Net: core/ZBUF_2_582
    max_capacitance     60.7300
  - Capacitance         62.4727
  --------------------------------
    Slack               -1.7427 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_2_inst_1873/Z  60.7300  62.4727       -1.7427  (VIOLATED) 

    Net: core/n853
    max_capacitance     60.5774
  - Capacitance         62.2684
  --------------------------------
    Slack               -1.6910 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U1070/ZN     60.5774        62.2684        -1.6910  (VIOLATED) 

    Net: core/CPU_Xreg_value_a4[18][15]
    max_capacitance     60.7300
  - Capacitance         62.2421
  --------------------------------
    Slack               -1.5121 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[18][15]/Q  60.7300  62.2421  -1.5121 (VIOLATED)

    Net: core/CPU_src2_value_a3[21]
    max_capacitance     60.7300
  - Capacitance         62.2064
  --------------------------------
    Slack               -1.4764 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_src2_value_a3_reg[21]/Q  60.7300  62.2064  -1.4764 (VIOLATED)

    Net: core/gre_a_BUF_1045_5
    max_capacitance     60.7300
  - Capacitance         62.2013
  --------------------------------
    Slack               -1.4713 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_a_BUF_1045_inst_3537/Z  60.7300  62.2013  -1.4713 (VIOLATED)

    Net: core/CPU_Xreg_value_a4[3][2]
    max_capacitance     60.7300
  - Capacitance         62.1866
  --------------------------------
    Slack               -1.4566 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[3][2]/Q  60.7300  62.1866  -1.4566 (VIOLATED)

    Net: core/ZBUF_2_677
    max_capacitance     60.7300
  - Capacitance         62.0902
  --------------------------------
    Slack               -1.3602 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_2_inst_2019/Z  60.7300  62.0902       -1.3602  (VIOLATED) 

    Net: core/CPU_Xreg_value_a4[27][18]
    max_capacitance     60.7300
  - Capacitance         62.0539
  --------------------------------
    Slack               -1.3239 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[27][18]/Q  60.7300  62.0539  -1.3239 (VIOLATED)

    Net: core/ZBUF_1954_321
    max_capacitance    121.4600
  - Capacitance        122.7492
  --------------------------------
    Slack               -1.2892 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_1954_inst_1303/Z 121.4600 122.7492    -1.2892  (VIOLATED) 

    Net: core/ZBUF_32_330
    max_capacitance     60.7300
  - Capacitance         61.9750
  --------------------------------
    Slack               -1.2450 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_32_inst_1319/Z  60.7300  61.9750      -1.2450  (VIOLATED) 

    Net: core/n3367
    max_capacitance     23.2315
  - Capacitance         24.4707
  --------------------------------
    Slack               -1.2392 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U1186/ZN     23.2315        24.4707        -1.2392  (VIOLATED) 

    Net: core/CPU_Xreg_value_a4[11][14]
    max_capacitance     60.7300
  - Capacitance         61.8787
  --------------------------------
    Slack               -1.1487 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[11][14]/Q  60.7300  61.8787  -1.1487 (VIOLATED)

    Net: core/n3377
    max_capacitance     23.2315
  - Capacitance         24.3513
  --------------------------------
    Slack               -1.1198 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U985/ZN      23.2315        24.3513        -1.1198  (VIOLATED) 

    Net: core/gre_net_223
    max_capacitance     60.7300
  - Capacitance         61.7727
  --------------------------------
    Slack               -1.0427 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3547/Z  60.7300  61.7727       -1.0427  (VIOLATED) 

    Net: core/n320_CDR1
    max_capacitance     28.9917
  - Capacitance         29.9851
  --------------------------------
    Slack               -0.9934 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U392/ZN      28.9917        29.9851        -0.9934  (VIOLATED) 

    Net: core/ZBUF_14_597
    max_capacitance     60.7300
  - Capacitance         61.6679
  --------------------------------
    Slack               -0.9379 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_14_inst_1892/Z  60.7300  61.6679      -0.9379  (VIOLATED) 

    Net: core/ZBUF_2_719
    max_capacitance     60.7300
  - Capacitance         61.6562
  --------------------------------
    Slack               -0.9262 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_2_inst_2094/Z  60.7300  61.6562       -0.9262  (VIOLATED) 

    Net: core/ZBUF_2_660
    max_capacitance     60.7300
  - Capacitance         61.6501
  --------------------------------
    Slack               -0.9201 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_2_inst_1987/Z  60.7300  61.6501       -0.9201  (VIOLATED) 

    Net: core/CPU_Xreg_value_a4[24][21]
    max_capacitance     60.7300
  - Capacitance         61.4971
  --------------------------------
    Slack               -0.7671 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[24][21]/Q  60.7300  61.4971  -0.7671 (VIOLATED)

    Net: core/gre_net_180
    max_capacitance     60.7300
  - Capacitance         61.3719
  --------------------------------
    Slack               -0.6419 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3455/Z  60.7300  61.3719       -0.6419  (VIOLATED) 

    Net: core/CPU_Xreg_value_a4[26][20]
    max_capacitance     60.7300
  - Capacitance         61.2671
  --------------------------------
    Slack               -0.5371 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[26][20]/Q  60.7300  61.2671  -0.5371 (VIOLATED)

    Net: core/n719
    max_capacitance     16.0217
  - Capacitance         16.5074
  --------------------------------
    Slack               -0.4857 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U136/ZN      16.0217        16.5074        -0.4857  (VIOLATED) 

    Net: core/gre_net_243
    max_capacitance     60.7300
  - Capacitance         61.1441
  --------------------------------
    Slack               -0.4141 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/gre_mt_inst_3567/Z  60.7300  61.1441       -0.4141  (VIOLATED) 

    Net: core/CPU_Xreg_value_a4[2][5]
    max_capacitance     60.7300
  - Capacitance         61.1425
  --------------------------------
    Slack               -0.4125 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[2][5]/Q  60.7300  61.1425  -0.4125 (VIOLATED)

    Net: core/n3361
    max_capacitance     23.2315
  - Capacitance         23.6085
  --------------------------------
    Slack               -0.3770 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U1162/ZN     23.2315        23.6085        -0.3770  (VIOLATED) 

    Net: core/n1461
    max_capacitance     60.2722
  - Capacitance         60.6075
  --------------------------------
    Slack               -0.3353 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[11][5]/QN  60.2722  60.6075  -0.3353 (VIOLATED)

    Net: core/n625
    max_capacitance     26.0544
  - Capacitance         26.3740
  --------------------------------
    Slack               -0.3196 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/U773/ZN      26.0544        26.3740        -0.3196  (VIOLATED) 

    Net: core/ZBUF_382_986
    max_capacitance     60.7300
  - Capacitance         60.8899
  --------------------------------
    Slack               -0.1599 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_382_inst_2710/Z  60.7300  60.8899     -0.1599  (VIOLATED) 

    Net: core/CPU_Xreg_value_a4[9][16]
    max_capacitance     60.7300
  - Capacitance         60.7945
  --------------------------------
    Slack               -0.0645 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/CPU_Xreg_value_a4_reg[9][16]/Q  60.7300  60.7945  -0.0645 (VIOLATED)

    Net: core/ZBUF_8696_514
    max_capacitance    121.4600
  - Capacitance        121.4904
  --------------------------------
    Slack               -0.0304 (VIOLATED)

  List of violating pins on net:
  ---------------------------------------------------------------------------
                             Required        Actual                            
     Pin/Port               Capacitance    Capacitance       Slack  Violation  
  ---------------------------------------------------------------------------
     PIN : core/ZBUF_8696_inst_1754/Z 121.4600 121.4904    -0.0304  (VIOLATED) 

  ---------------------------------------------------------------------------
   Number of max_capacitance violation(s): 141



   Total number of violation(s): 145
1

```
