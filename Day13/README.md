# PVT (Process Voltage Temperature) Analysis

#### Integrated circuits are designed in such a way that they can function in a wide variety of vltages and temperatures, rather than a single voltage and temperature. These must function in variety of contexts including various conditions, electrical setup, user environments etc.

<details>
<summary>What is PVT?</summary>
<br>

* `Process (P)` : There are millions of transistors on a singke chip as we are going to lower nodes and all the transistors in a chip cannot have same properties. Process variation is the deviation in parameters of the transistors during fabrication.

* `Voltage (V)`: As we are going to lower nodes the supply voltage for a chip is also going to less. Let's say the chip is operating at 1.2 V. So, there are chances that at certain instances of time this voltage may vary.

* `Temperature (T)`: When a chip is operating, the temperature can vary throught the chip. This is due to power dissipation in MOS- transistors.
  
</details>

<details>
<summary>Corners of PVT?</summary>
<br>

* In order to make our chip to work after fabrication in all the possible conditions, we simulate it at different corners of process, voltage and temperature.
  
* These conditions are called corners. All these three parameters directly affect the delay of the cell.

  * `Transistor corners (fast, typical, slow)`
 
  * `Voltage`
 
  * `Temperature`

##### PVT Corner details

| Name         |Process {PMOS, NMOS}|  Voltage (V) |  Temperature (°C) | Lib file (.lib) |
| ------------  | ------------ | ------------ | ------------ | ------------ |
|`tt_025c_1v80` |   {T, T}|1.8   |25°C   |sky130_fd_sc_hd__tt_025c_1v80.lib (Typical)   |
| `ss_100c_1v60` |   {S, S}|1.6   |100°C   |sky130_fd_sc_hd__ss_100c_1v60.lib (Slow)  |  
|   `ff_n40c_1v95` |   {F, F}|1.95   |-40°C   |sky130_fd_sc_hd__ff_n40c_1v95.lib (Fast) |   
  
</details>

<details>
  <summary> PVT Graphs </summary>
  <br>

  ![image](https://github.com/user-attachments/assets/1696ea53-ecee-4069-b4ac-1a9e9463e705)

</details>

<details>
  <summary> PVT Analysis </summary>
  <br>

#### In this analysis SKY130PDK PVT Libs are used

* Download the libraries from `(https://github.com/efabless/skywater-pdk-libs-sky130_fd_sc_hd.git)`

* convert .lib files to .db format using synopsys `LC` shell

* TCL script to convert .lib file to .db format

```
# convert_lib_to_db.tcl
set lib_files_dir "/home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/skywater-pdk-libs-sky130_fd_sc_hd/timing";
set db_output_dir "/home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/timinglibs";
foreach lib_file [glob -nocomplain $lib_files_dir/*.lib] {
set base_name [file rootname [file tail $lib_file]]
set db_file "$db_output_dir/${base_name}.db"

if {[llength [list_libs]] > 0} {
    remove_lib [lindex [list_libs] 0]
}

read_lib $lib_file

write_lib $base_name -format db -output $db_file

if {[llength [list_libs]] > 0} {
    remove_lib [lindex [list_libs] 0]
}
}
exit

```
.db files

![image](https://github.com/user-attachments/assets/2ff4d9f6-7ca1-423e-b8f1-eeab2cc4589c)

#### To synthesize the VSDBabySoC for different PVT corners follow the steps

* create a `multi_pvt_corners.tcl` file
  
* copy the following code into the above file

```

set m1 ""
   set pvt ""
   set FH [open report_timing.rpt w] ;# create timing report file
   puts $FH "PVT_Corner\tWNS\tWHS"
   
   set lib_files [glob -directory /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/timinglibs/ -type f *.db]
   
   foreach lib_file_paths $lib_files {
   
   regexp {.*\/sky130_fd_sc_hd__(.*)\.db$} $lib_file_paths m1 pvt
   
   set timing_report_fast_mode true
   
   
   set target_library $lib_file_paths
   set link_library {* /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/avsdpll.db /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/avsddac.db}
   lappend link_library $target_library
   set search_path {/home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/include /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/module}
   read_file {sandpiper_gen.vh  sandpiper.vh  sp_default.vh  sp_verilog.vh clk_gate.v rvmyth.v rvmyth_gen.v vsdbabysoc.v} -autoread -top vsdbabysoc
   source /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/sdc/vsdbabysoc_synthesis.sdc
   link
   compile_ultra ;# to synthesize the design using currently set target PVT corner
   
   set wns [get_attribute [get_timing_paths -delay_type max -max_paths 1] slack] ;# Determine worst negative slack (setup) for current pvt corner
   set whs [get_attribute [get_timing_paths -delay_type min -max_paths 1] slack] ;# Determine worst hold slack of current pvt corner.
   
   puts $FH "$pvt\t$wns\t$whs" ;# Write out pvt and their corresponding wns and whs in the timing report
   
   reset_design
   }
   
   close $FH

```

* Invoke `dc_shell`

* source `/home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/multi_pvt_corners.tcl`

* open the report_timing.rpt text file from the present working directory to get the information about WNS and WHS for different PVT corners

##### Table showing the Worst Negative Slack (WNS) and Worst Hold Slack (WHS) for different PVT corners available in SKY130PDK for synthesized VSDBabySoC design


| PVT_Corner| WNS  | WHS  |
| ------------ | ------------ | ------------ |
| ff_100C_1v65 |  0.0865402|  0.255021|
| ff_100C_1v95  | 1.73898  | 0.201382  |
| ff_n40C_1v56  |0.0162086   |  0.298206 |
|  ff_n40C_1v65 |  0.0113392 | 0.26137  |
|  ff_n40C_1v76 |1.19031   | 0.230204  |
| ff_n40C_1v95  | 1.74468  |  0.192912 |
| ss_100C_1v40  |0.00199986   | 0.895194  |
| ss_100C_1v60  |3.20255   | 0.64934  |
|ss_n40C_1v28   |  -0.966409 | 1.7782  |
|ss_n40C_1v35   |0.000314713   | 1.30867  |
| ss_n40C_1v40  | 0.000483513  | 1.13354  |
| ss_n40C_1v44  | 0.00174999  |  0.973081 |
|  ss_n40C_1v60 | 0.00452137  |0.669568   |
| ss_n40C_1v76  | 0.00879574  | 0.510206  |
| tt_025C_1v80  |  0.0324135 | 0.31604  |
|tt_100C_1v80   | 0.0135527  |  0.31977 |



#### Graphs

----
##### Worst Negative Slack (WNS)


![image](https://github.com/user-attachments/assets/35c650db-8622-4da2-8d01-5c17bfa4609d)

-----

##### Worst Hold Slack

![image](https://github.com/user-attachments/assets/7355c7bf-240d-4195-a703-2b67b021f118)

-----


</details>

