#### Script to run Prime Time STA analysis for all available PVT Corners :

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

read_verilog /home/vijayalaxmi/SFAL-VSD/output/vsdbabysoc_post_route_net_max_cap.v
current_design vsdbabysoc

link_design
read_sdc /home/vijayalaxmi/SFAL-VSD/output/vsdbabysoc_post_route.sdc
read_parasitics /home/vijayalaxmi/SFAL-VSD/vsdbabysoc_parasitics_max_cap.temp1_25.spef

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

#### Table for Worst Negative/Setup Slack (WNS) & Worst Hold Slack (WHS) for different available PVT corners from Prime Time Analysis, for our BabySoC Design :

| PVT_Corner   | WNS         | WHS        |
| ------------ | ----------- | ---------- |
| ff_100C_1v65 | 3.124938    | \-0.235642 |
| ff_100C_1v95 | 4.522051    | \-0.291165 |
| ff_n40C_1v56 | 1.436169    | \-0.193214 |
| ff_n40C_1v65 | 2.510405    | \-0.230101 |
| ff_n40C_1v76 | 3.476581    | \-0.261722 |
| ff_n40C_1v95 | 4.582528    | \-0.300085 |
| ss_100C_1v40 | \-12.455952 | 0.59104    |
| ss_100C_1v60 | \-5.715736  | 0.236287   |
| ss_n40C_1v28 | \-48.670876 | 1.840496   |
| ss_n40C_1v35 | \-31.053354 | 1.181901   |
| ss_n40C_1v40 | \-23.332808 | 0.867832   |
| ss_n40C_1v44 | \-18.90251  | 0.674178   |
| ss_n40C_1v60 | \-8.493254  | 0.244431   |
| ss_n40C_1v76 | \-3.560485  | 0.040591   |
| tt_025C_1v80 | 1.610215    | \-0.166896 |
| tt_100C_1v80 | 1.694567    | \-0.156524 |


![image](https://github.com/user-attachments/assets/932985e0-ea3b-4d31-b94b-c016c0102817)

![image](https://github.com/user-attachments/assets/7403a1f5-77ab-4be1-bd23-fc6307a806a1)


