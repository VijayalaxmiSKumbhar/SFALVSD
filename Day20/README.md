## ECO using Prime Time

<details>
  <summary>ECO in VLSI Design</summary>
  <br>
  
* ECO stands for `Engineering Change Order` in the context of VLSI (Very Large Scale Integration) design.
  
* It refers to a formalized process for implementing changes in a hardware design after the initial design has been completed.
  
* ECOs are often used to address issues such as bugs, performance improvements, or changes in specifications that occur after the design has been finalized but before or after fabrication.

## Purpose of ECO:

* To correct errors or defects in the original design.
  
* To implement functional changes or enhancements.
  
* To accommodate changes in specifications or requirements.

## ECO Process

* `Identification:` The need for an ECO is identified, often through testing, simulation, or customer feedback.
  
* `Assessment:` Engineers assess the impact of the proposed changes on the overall design, including compatibility, functionality, and timing.
  
* `Modification:` The design is modified according to the ECO, which may include changes in the schematics, layout, or HDL (Hardware Description Language) code.
  
* `Verification:` The modified design undergoes verification through simulations and checks to ensure that the changes achieved the desired effects without introducing new issues.
  
* `Documentation:` The ECO process is documented for future reference, including the rationale for changes, the details of the modifications, and testing results.

## Types of ECO

#### The engineering change orders can be classified into two categories:

* `All layers ECO:` In this, the design change is implemented using all layers. This kind of ECO provides advantage in terms of cycle time and engineering costs.
  It is implemented whenever the change is not possible to be carried out without all layer change e.g. there is an updation in a hard macro cell or the change may require updation of 100’s of cells. It is almost impossible to contain such a large change to a few layers only.
  
* `Metal-only ECO:` Sometimes, it may not be practical to use all the layers (base + metal) to do the ECO. In that case, to minimize the cost, it is required to be completed with changes only in minimal number of metal layers. These days, it is expected that every design will be re-opened for the ECOs. So, an adequate number of spare cells are sprinkled during the implementation all over the design to be used later on. These cells are spread uniformly over the design. The inputs of these cells are tied. Whenever the need for an ECO arises, the cells to be implemented can be mapped into the existing spare cells. Hence, there is no need to change the base layers in such a case. Only the connections need to be updated which can be done by changing the metal layers only. Hence, the base layer cost is saved.


## Challenges in ECO:

* `Version Control:` Managing changes and keeping track of different design versions can be complex.
  
* `Integration:` Ensuring that the ECO does not negatively affect other parts of the design or the overall system.
  
* `Timing Analysis:` Changes might affect timing, requiring thorough timing analysis after modifications.

## Conclusion

ECO plays a significant role in adapting and refining hardware designs to keep up with evolving requirements and to resolve issues identified post-design.

</details>

<details>
<summary>Lab: Timing ECO using Prime Time for VSDBabySoC design</summary>
<br>

* Script to setup prime time ECO:

```

set link_path "* /home/vijayalaxmi/SFAL-VSD/src/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.db /home/vijayalaxmi/SFAL-VSDsrc/lib/avsdpll.db /home/vijayalaxmi/SFAL-VSD/src/lib/avsddac.db"

read_verilog /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/vsdbabysoc_post_route_net.v
current_design vsdbabysoc
link_design
set_min_library -min_version /home/vijayalaxmi/SFAL-VSD/src/timing_libs/sky130_fd_sc_hd__ff_n40C_1v95.db /home/vijayalaxmi/SFAL-VSD/src/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.db

read_sdc /home/vijayalaxmi/SFAL-VSD/output/vsdbabysoc_post_route.sdc
read_parasitics /home/vijayalaxmi/SFAL-VSD/output/vsdbabysoc_parasitics.temp1_25.spef

update_timing -full

report_analysis_coverage > /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/reports/prime_time_analysis_coverage.rpt
report_constraint -all_violators > /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/reports/prime_time_constraint.rpt
report_timing -delay_type max -capacitance -input_pins -nets -transition_time -nosplit -significant_digits 4 > /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/reports/prime_time_setup_timing.rpt
report_timing -delay_type min -capacitance -input_pins -nets -transition_time -nosplit -significant_digits 4 > /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/reports/prime_time_hold_timing.rpt


```

![image](https://github.com/user-attachments/assets/642f5846-d1c1-4d5e-94e0-98aa0b14e5e4)

## To fix setup violations: `fix_eco_timing -type setup`

![image](https://github.com/user-attachments/assets/61123ad9-0208-42a4-9f1b-fc66bc9294ba)

## To fix hold violations by inserting buffers:
`fix_eco_timing -type hold -methods insert_buffer -buffer_list {sky130_fd_sc_hd__buf_1 sky130_fd_sc_hd__buf_2 sky130_fd_sc_hd__buf_4 sky130_fd_sc_hd__buf_8}`

![image](https://github.com/user-attachments/assets/b543d930-a004-45b5-a0b8-fb3e343d410e)

## Prime Time Analysis Coverage Report after `ECO Fixing`:

![image](https://github.com/user-attachments/assets/2eff90b1-498e-483b-91fc-65dec3b2406b)


* `write_changes -format icc2tcl -output /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/vsdbabysoc_eco.tcl`

#### Screenshot of netlist changes obtained after `fix_eco_timing` and `write_changes` command execution :

![image](https://github.com/user-attachments/assets/4e97cbaa-0759-437f-b935-369ae9f467e0)

## Applying ECO changes in ICC2 Shell

* Load the generated script into ICC2 Shell using the following command:

`source /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/vsdbabysoc_eco.tcl`

* `check_legality` after sourcing vsdbabysoc_eco.tcl in ICC2 Compiler to perform ECO and fix Timing Violations : :

![image](https://github.com/user-attachments/assets/2e64ab31-fad1-42d7-ae00-3a05a951ab45)

* `route_eco` -The route_eco command performs ECO routing. It first connects the open nets and then fixes the DRC violations. The options control which nets are connected and in which areas of the chip the DRC violations are fixed. Use this command only after signal routing has been completed.

![image](https://github.com/user-attachments/assets/cdabe9ab-1c4e-4177-af8b-2889b6786061)
![image](https://github.com/user-attachments/assets/1902f64a-a304-448e-8c97-e5272828a28c)

* We have to again extract .SPEF file and post_route netlist and perform Prime Time STA,to check if our timing violations have been fixed by the ECO or not.

* Script to setup Prime Time STA for post-ECO database :

```

set link_path "* /home/vijayalaxmi/SFAL-VSD/src/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.db /home/vijayalaxmi/SFAL-VSD/src/lib/avsdpll.db /home/vijayalaxmi/SFAL-VSD/src/lib/avsddac.db"

read_verilog /home/vijayalaxmi/SFAL-VSD/output/vsdbabysoc_post_route_net_max_cap.v
current_design vsdbabysoc
link_design
set_min_library -min_version /home/vijayalaxmi/SFAL-VSD/src/timing_libs/sky130_fd_sc_hd__ff_n40C_1v95.db /home/vijayalaxmi/SFAL-VSD/src/timing_libs/sky130_fd_sc_hd__tt_025C_1v80.db

read_sdc /home/vijayalaxmi/SFAL-VSD/output/vsdbabysoc_post_route.sdc

read_parasitics /home/vijayalaxmi/SFAL-VSD/output/vsdbabysoc_parasitics_max_cap.temp1_25.spef

update_timing -full

report_analysis_coverage > /home/vijayalaxmi/Desktop/pdflow1/output/reports/prime_time_analysis_coverage.rpt
report_constraint -all_violators > /home/vijayalaxmi/Desktop/pdflow1/output/reports/prime_time_constraint.rpt
report_timing -delay_type max -capacitance -input_pins -nets -transition_time -nosplit -significant_digits 4 > /home/vijayalaxmi/Desktop/pdflow1/output/reports/prime_time_setup_timing.rpt
report_timing -delay_type min -capacitance -input_pins -nets -transition_time -nosplit -significant_digits 4 > /home/vijayalaxmi/Desktop/pdflow1/output/reports/prime_time_hold_timing.rpt

```

* report_analysis_coverage report in Prime Time using post_eco database :

![image](https://github.com/user-attachments/assets/3334b5d4-6edf-41e0-82c9-ca12947c391f)


</details>
