# STA using Prime Time

<details>
  <summary>STA using PT</summary>
  <br>

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
set link_path "* /home/vijayalaxmi/SFAL-VSD/VSDBabySoC/src/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.db /home/vijayalaxmi/SFAL-VSD/VSDBabySoC/src/lib/avsdpll.db /home/vijayalaxmi/SFAL-VSD/VSDBabySoC/src/lib/avsddac.db"

read_verilog /home/vijayalaxmi/SFAL-VSD/VSDBabySoC/output/vsdbabysoc_post_route_net_max_cap_post_eco.v
current_design vsdbabysoc
link_design
set_min_library -min_version /home/vijayalaxmi/SFAL-VSD/VSDBabySoC/src/timing_libs/sky130_fd_sc_hd__ff_n40C_1v95.db /home/vijayalaxmi/SFAL-VSD/VSDBabySoC/src/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.db

read_sdc /home/vijayalaxmi/SFAL-VSD/VSDBabySoC/output/vsdbabysoc_post_route.sdc
#read_parasitics /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/vsdbabysoc_parasitics.temp1_25.spef
read_parasitics /home/vijayalaxmi/SFAL-VSD/VSDBabySoC/output/vsdbabysoc_parasitics_max_cap_post_eco.temp1_25.spef

update_timing -full

report_analysis_coverage > /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/reports/prime_time_analysis_coverage.rpt
report_constraint -all_violators > /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/reports/prime_time_constraint.rpt
report_timing -delay_type max -capacitance -input_pins -nets -transition_time -nosplit -significant_digits 4 > /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/reports/prime_time_setup_timing.rpt
report_timing -delay_type min -capacitance -input_pins -nets -transition_time -nosplit -significant_digits 4 > /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/reports/prime_time_hold_timing.rpt

```
* `run pt_shell`

![image](https://github.com/user-attachments/assets/91456ece-7cf8-403c-8923-e4d1e7dff876)

* `source /home/vijayalaxmi/Desktop/pdflow/prime_time_sta.tcl`
</details>

