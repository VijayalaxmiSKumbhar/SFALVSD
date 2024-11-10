# Post-Synthesis Simulation

<details>
<summary> Introduction </summary>
<br>

* Post-synthesis simulation is essential for validating the functionality, performance, and reliability of the designs before they are fabricated.
  
* Purpose of Post-synthesis simulation:
  
  1. Verification
  
  2. Timing Analysis
  
  3. Power Analysis
  
  4. Functional Validation
  
* Stages of Post-Synthesis Simulation
  
  1. Gate-Level Simulation
  
  2. Static Timing Analysis (STA)
  
  3. Dynamic Simulation
  
  4. Power Simulation 

</details>

<details>
<summary> Why do Pre-synthesis? Why not just do post-synthesis?</summary>
<br>

* Pre-synthesis simulation done according to the logic designed -----> It only checks the functionality
  
* Post-synthesis simulation/ `'Gate Level Simulation'` is done after synthesis considering each and every gate delays into account. Reports the violations both in functionality and timing.
  
* This also shows the mismatches that are due to wrong usage of operators and inference of latches.
  
  For example: Using `'X'` (Simulator terms/ synthesizer terms) - `"Unknown"/"Don't care"` 

</details>

<details>
<summary> Inrduction to GLS (Gate Level Simulation) </summary>
<br>

* The term `gate level ` refers to netlist view of the circuit.

* RTL simulation is pre-synthesis, GLS is post-synthesis.

* The netlist view is complete connection list consisting of gates and IP models with full functional and timing behavior.

* RTL Simulation is zero delay environment and events generally occur on active clock edge.

* GLS can be zero delay also, but is more often used in unit delay or full timing mode.

* GLS helps in verifying the dynamic behavior of the circuit, which cannot be verified accurately by static methods.


</details>

<details>
<summary> Synthesis using Synopsys's DC Shell (Design Compiler) </summary>
<br>

#### Commands to convert .lib to .db

###### converting `avsddac.lib` to `avsddac.db`

* cd vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib

![image](https://github.com/user-attachments/assets/82481af1-1254-4c88-ac13-9841b747d83c)

* Launch lc_shell

  1. csh
    
  2. lc_shell

![image](https://github.com/user-attachments/assets/6f1faec7-ebe7-4c31-9365-9ef7c28c1417)

* Reading avsddac library: `read_lib avsddac.lib`
  
![image](https://github.com/user-attachments/assets/7e5fb172-86ba-421d-b80c-563ec724250a)

* Writing .db file: `write_lib avsddac -format db -output avsddac.db`  

![image](https://github.com/user-attachments/assets/68b19d40-5077-42ee-b8e7-67a28b189636)

###### converting `avsdpll.lib` to `avsdpll.db`

* cd vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib

![image](https://github.com/user-attachments/assets/7a5c2e22-ea6f-4145-ad9e-4e415aec10b0)



* Launch lc_shell

  1. csh
    
  2. lc_shell

![image](https://github.com/user-attachments/assets/546a1001-8577-4bf8-b62b-693940a1c86d)

* Reading avsdpll library: `read_lib avsdpll.lib`
  
After running the above command will get the errors, the corrected avsdpll.lib is as given here

```
library (avsdpll) {
  time_unit : "1ns";
  voltage_unit : "1V";
  current_unit : "1uA";
  pulling_resistance_unit : "1kohm";
  leakage_power_unit : "1nW";
  capacitive_load_unit(1, pf);

  slew_lower_threshold_pct_fall : 20.000000000;
  slew_lower_threshold_pct_rise : 20.000000000;
  slew_upper_threshold_pct_fall :  80.00000000;
  slew_upper_threshold_pct_rise :  80.00000000;
  input_threshold_pct_fall : 50.000000000;
  input_threshold_pct_rise : 50.000000000;
  output_threshold_pct_fall : 50.000000000;
  output_threshold_pct_rise : 50.000000000;

  cell (avsdpll) {
    pin(CLK) {
      direction : output;
      capacitance : 0.001;
    }

    pin (VCO_IN) {
      direction : input;
      max_transition : 2.5;
      capacitance : 0.001;
    }

    pin (ENb_CP) {
      direction : input;
      max_transition : 2.5;
      capacitance : 0.001;
    }
    
	  pin (ENb_VCO) {
      direction : input;
      max_transition : 2.5;
      capacitance : 0.001;
    }

    pin (REF) {
      direction : input;
      max_transition : 2.5;
      capacitance : 0.001;
    }

    pin (GND) {
      direction : input;
      max_transition : 2.5;
      capacitance : 0.001;
    }

    
    pin (VDD) {
      direction : input;
      max_transition : 2.5;
      capacitance : 0.001;
    }
    
    
  }
}

```


![image](https://github.com/user-attachments/assets/5af6ee3f-1a38-4f3e-b3c1-1ecd6c0c7942)



* Writing .db file: `write_lib avsdpll -format db -output avsdpll.db`  


![image](https://github.com/user-attachments/assets/e713e901-0f97-4fca-b1a1-ce4f857e68e3)



###### converting `sky130_fd_sc_hd__tt_025C_1v80.lib` to `sky130_fd_sc_hd__tt_025C_1v80.db`



* cd vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib
  

![image](https://github.com/user-attachments/assets/82481af1-1254-4c88-ac13-9841b747d83c)


* Launch lc_shell

  1. csh
    
  2. lc_shell

![image](https://github.com/user-attachments/assets/6f1faec7-ebe7-4c31-9365-9ef7c28c1417)


* Reading sky130_fd_sc_hd__tt_025C_1v80 library: `read_lib sky130_fd_sc_hd__tt_025C_1v80.lib`
  
  
![image](https://github.com/user-attachments/assets/f278308c-249e-4ca6-b615-b1dd5f95c85d)


* Writing .db file: `write_lib sky130_fd_sc_hd__tt_025C_1v80 -format db -output sky130_fd_sc_hd__tt_025C_1v80.db`
  

![image](https://github.com/user-attachments/assets/fea0bddb-18d3-4d6c-ba69-8d0c6ac162db)


#### Synthesis and Gate Level Simulation

* cd vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib
  

![image](https://github.com/user-attachments/assets/82481af1-1254-4c88-ac13-9841b747d83c)


* Launch dc_shell

  1. `csh`
    
  2. `dc_shell`


![image](https://github.com/user-attachments/assets/da1a09c3-5f01-4986-a723-5669cc877d04)


* `set target_library /home/vijayalaxmi/Desktop/VLSI/VSDBabySOC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db`

![image](https://github.com/user-attachments/assets/917a6483-5a53-44fc-9d89-c93113bbb9d2)

* `set link_library {* /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.db /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/avsdpll.db /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/src/lib/avsddac.db}`

![image](https://github.com/user-attachments/assets/f46fa143-156d-4713-bf9f-d6611e9c0df9)

`set search_path {/home/vijayalaxmi/Desktop/VLSI/VSDBabySOC/src/include /home/vijayalaxmi/Desktop/VLSI/VSDBabySOC/src/module}'

![image](https://github.com/user-attachments/assets/3c2ea7c3-a322-4387-971f-edf58fa288ba)


* `read_file {sandpiper_gen.vh  sandpiper.vh  sp_default.vh  sp_verilog.vh clk_gate.v rvmyth.v rvmyth_gen.v vsdbabysoc.v} -autoread -top vsdbabysoc`


![image](https://github.com/user-attachments/assets/2ef06d19-4dcc-4ea7-9470-b8e2252fe0cb)

![image](https://github.com/user-attachments/assets/685a3eae-7d95-4a0b-b783-42b31b2af961)

* `link`

![image](https://github.com/user-attachments/assets/6c350122-9812-4668-a532-2c40987e4be4)


* `compile_ultra`

![image](https://github.com/user-attachments/assets/736ddfc0-8019-4e0c-a124-0471dce06177)

![image](https://github.com/user-attachments/assets/87922c90-6b3a-4c73-a995-d97ad4d8330f)

![image](https://github.com/user-attachments/assets/43fe1c01-7b76-41d8-9110-7064e0586988)

![image](https://github.com/user-attachments/assets/ebce9502-404f-4239-9e4b-9cb98b9a0f7b)

![image](https://github.com/user-attachments/assets/134c0fa4-08e5-4975-b302-997b986fa5d2)

![image](https://github.com/user-attachments/assets/5006bebb-088b-47bb-be54-a5d2af29297c)


* `write_file -format verilog -hierarchy -output /home/vijayalaxmi/Desktop/VLSI/VSDBabySoC/output/vsdbabysoc_net.v`

![image](https://github.com/user-attachments/assets/f2721970-1a85-424a-9175-244830c9366f)



* `report_qor > report_qor.txt`


![image](https://github.com/user-attachments/assets/7d2d081d-f339-47b0-b593-f4037f467a91)
![image](https://github.com/user-attachments/assets/8646c7e6-da1d-4930-b44c-c4f07175c10b)
![image](https://github.com/user-attachments/assets/8e8f695c-bdc8-43cb-b5ac-40b60588d1b5)



## Post-synthesis Simulation

`iverilog -DFUNCTIONAL -DUNIT_DELAY=#1 -o ./output/post_synth_sim.out ./src/gls_model/primitives.v ./src/gls_model/sky130_fd_sc_hd.v ./output/vsdbabysoc_net.v ./src/module/avsdpll.v ./src/module/avsddac.v ./src/module/testbench.v`

![image](https://github.com/user-attachments/assets/a548cd73-86ad-4b34-bcbd-aef938573cc5)

* Remove the errors

Comment `GND, VDD of avsdpll in the vsdbabysoc_net.v file`

comment `VSSA, VDDA of avsddac in the vsdbabysoc_net.v file`

* `cd VSDBabySoC/ouput`

* `./post_synth_sim.out`

![image](https://github.com/user-attachments/assets/add894e4-d464-426c-9be8-1977d6d0936d)

* `gtkwave dump.vcd`

![image](https://github.com/user-attachments/assets/0fe1bffa-427a-49f5-aaac-4c27a996b22b)


![image](https://github.com/user-attachments/assets/4cd9355e-5f99-4021-917e-14cc6e3fe99a)


</details>
