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
