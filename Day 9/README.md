# Generating Timing Reports and Analyzing QoR

#### Quality Checks

<details>
<summary>Report Timing </summary>
<br>

## Generating Timing Reports

![image](https://github.com/user-attachments/assets/6df64a73-4865-42b1-a33d-e9c089d7bd7d)

#### Quick look at Propagation Delay

![image](https://github.com/user-attachments/assets/ba53953d-b672-40f8-af3f-4bf72eb16f9e)

#### Timing Paths Further Details

![image](https://github.com/user-attachments/assets/b8dfa4eb-cd80-4922-a3ce-a0363c8f6a53)

![image](https://github.com/user-attachments/assets/ded772e0-0343-4f88-9a8f-68f3f40f7b68)

#### What is Max_path and Nworst?

![image](https://github.com/user-attachments/assets/f8f63a09-76a8-4570-b4da-34f60b03b16d)


</details>

<details>
<summary> Lab: Report Timing </summary>
<br>

## Example is lab8_circuit_modified.v

* Invoke `dc_shell`
  
* `read_verilog /home/vijayalaxmi/lab8_circuit_modified.v`

![image](https://github.com/user-attachments/assets/50a33220-283a-4f0d-bfb0-5bf9b61c0c79)

* `set target_library /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db`
* `set link_library {* /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db}'
* `link'
![image](https://github.com/user-attachments/assets/f0f894ac-df3a-404c-a95f-526e4a0cf9cb)

* `source /home/vijayalaxmi/lab8_cons_modified.tcl`
* `compile_ultra`
* `report_timing -sig 4 -nosplit -trans -cap -nets -inp`


</details>

<details>
<summary>Lab: Check_timing, Check_design, Set_max_capacitance, HFN </summary>
<br>


</details>

