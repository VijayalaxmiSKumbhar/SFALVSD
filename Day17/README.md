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


