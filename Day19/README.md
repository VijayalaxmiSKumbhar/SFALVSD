# STA using Prime Time (PT) Tool


#### Extract parasitics information in .SPEF format by using following command :

`write_parasitics -corner func1 -output /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/vsdbabysoc_parasitics`

![image](https://github.com/user-attachments/assets/e8f0fba8-060a-45c0-a903-9c04f247ef35)

* `.SPEF file:`

![image](https://github.com/user-attachments/assets/0d1fd085-ac77-4621-8c61-46ebd66a838e)

* In ICC2_shell, we can also write out the post_route netlist :

`write_verilog /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/vsdbabysoc_post_route_net.v`

![image](https://github.com/user-attachments/assets/b274ed74-9533-4932-ae41-3166da379bcb)
![image](https://github.com/user-attachments/assets/3e24a496-33a6-494d-9200-083989a69bef)


* Now we can use Prime Time tool for timing analysis using following script:

```
set m1 ""
set pvt ""
set wns ""
set whs ""
set FH [open report_timing_prime_time.rpt w]
puts $FH "PVT_Corner\tWNS\tWHS"


set lib_files [glob -directory /home/vijayalaxmi/SFAL-VSD/src/timing_libs/ -type f *.db]

foreach lib_file_paths $lib_files {
	

regexp {.*\/sky130_fd_sc_hd__(.*)\.db$} $lib_file_paths m1 pvt

set link_path "* /home/vijayalaxmi/SFAL-VSD/src/lib/avsdpll.db /home/vijayalaxmi/SFAL-VSD/src/lib/avsddac.db"
lappend link_path $lib_file_paths

read_verilog /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/vsdbabysoc_post_route_net.v
current_design vsdbabysoc

link_design
read_sdc /home/vijayalaxmi/SFAL-VSD/output/vsdbabysoc_post_route.sdc
read_parasitics /home/vijayalaxmi/SFAL-VSD/output/vsdbabysoc_parasitics.temp1_25.spef


set wns [get_attribute [get_timing_paths -delay_type max -max_paths 1] slack]
set whs [get_attribute [get_timing_paths -delay_type min -max_paths 1] slack]

puts $FH "$pvt\t$wns\t$whs"

remove_annotated_parasitics -all
reset_design
remove_design -all
remove_lib -all

}


close $FH


```
* `run pt_shell`

![image](https://github.com/user-attachments/assets/91456ece-7cf8-403c-8923-e4d1e7dff876)

* `source prime_time_sta_mul_pvt.tcl`

![image](https://github.com/user-attachments/assets/ee5fc8c7-c787-4b6a-92de-feca92a78c95)
![image](https://github.com/user-attachments/assets/9f04ebe7-fb4c-4d8e-8955-00e511f89415)

* Worst Negative/Setup Slack `(WNS)` & Worst Hold Slack `(WHS)` for different available PVT corners from Prime Time Analysis

![image](https://github.com/user-attachments/assets/8e9138fc-d5b7-4d71-b744-be039c0faad3)


|   PVT_Corner|WNS	   | WHS  |
| ------------ | ------------ | ------------ |
| ff_100C_1v65	|2.865155	|-0.150222 |
|  ff_100C_1v95	|4.298244	|-0.222546|
|ff_n40C_1v56	|1.151838	|-0.101215|
|ff_n40C_1v65	|2.232299	|-0.143085|
|ff_n40C_1v76	|3.196659	|-0.184872|
|ff_n40C_1v95	|4.313583	|-0.232505|
|ss_100C_1v40	|-15.293417	|0.764794|
|ss_100C_1v60	|-7.442810	|0.391557|
|ss_n40C_1v28	|-53.881828	|1.855523|
|ss_n40C_1v35	|-34.470398	|1.287956|
|ss_n40C_1v40	|-26.077168	|1.026193|
|ss_n40C_1v44	|-21.215034	|0.879572|
|ss_n40C_1v60	|-9.887131	|0.434462|
|ss_n40C_1v76	|-4.473462	|0.184826|
|tt_025C_1v80	|1.071807	|-0.068473|
|tt_100C_1v80	|1.179451	|-0.058827 |

#### `WNS V/s PVT_Corner`

![image](https://github.com/user-attachments/assets/62a4a0fc-6cb7-4612-9d3f-acc7045e32a1)

#### `WHS V/s PVT_Corner`

![image](https://github.com/user-attachments/assets/7d6dc55c-9e64-4ca9-9cbd-232f3987f774)
