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

#### Steps

1. Invoke DC and read the verilog file ----> rvmyth_avsddac.v

2. Read .db file and set target_lib -----> sky130_fd_sc_hd__tt_025c_1v80.lib

#### Commands to convert .lib to .db

1. lc_shell

2. read_lib library.lib

3. write_lib library -format db -output library.db

4. quit

Launch lc_shell

* csh

* lc_shell

![image](https://github.com/user-attachments/assets/eb199708-c581-4f35-9566-4283ce2f353c)


</details>
