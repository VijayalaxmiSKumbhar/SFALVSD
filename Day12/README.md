# Post-Synthesis Simulation

<details>
<summary>Why do Pre-synthesis? Why not just do post-synthesis?</summary>

* Pre-synthesis simulation done according to the logic designed -----> It only checks the functionality
* Post-synthesis simulation/ `'Gate Level Simulation'` is done after synthesis considering each and every gate delays into account. Reports the violations both in functionality and timing.
* This also shows the mismatches that are due to wrong usage of operators and inference of latches.
  ---- For example: Using `'X'` (Simulator terms/ synthesizer terms) - `"Unknown"/"Don't care"` 

</details>
