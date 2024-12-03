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
  
* `read_verilog /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/lab8_circuit_modified.v`

![image](https://github.com/user-attachments/assets/c55b9a9e-eb9c-44bc-a238-9a0ad89288e6)


* `set target_library /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db`
* `set link_library {* /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db}'
* `link'

![image](https://github.com/user-attachments/assets/bf9b7543-d446-4250-b29f-58005a41d390)


* `source /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/lab8_cons_modified.tcl`
* `compile_ultra`

![image](https://github.com/user-attachments/assets/1a256031-6852-4511-b79a-d96d15371182)
![image](https://github.com/user-attachments/assets/d537d329-a200-4a53-a0cc-8ebe64abaa84)

* `report_timing -sig 4 -nosplit -trans -cap -nets -inp > t1.rpt`
* `sh gvim t1.rpt`

![image](https://github.com/user-attachments/assets/d0876bec-f56e-49cf-9386-e111ee2e8dab)
![image](https://github.com/user-attachments/assets/18fb0689-32d3-4304-90e6-b762cdd7792f)
![image](https://github.com/user-attachments/assets/efa48ed4-eef4-46c9-a1ae-9067fccafd7d)
![image](https://github.com/user-attachments/assets/25dc526e-df52-4c42-89b6-3cc72a984681)



</details>

<details>
<summary>Lab: Check_timing, Check_design, Set_max_capacitance, HFN </summary>
<br>


</details>

