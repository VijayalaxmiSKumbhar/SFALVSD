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

```
* Note: Clues to identify whether it is setup check or hold check
  * `Path type: max`, therefore it is doing setup check
  * The launch edge and capture edge are not same
  * `Library setup time` is printed in the report
  * In the report it is `setup slack = data required time-data arrival time`, this is for `max` path.
```

* `report_timing -sig 4 -nosplit -trans -cap -nets -inp -from IN_A > t1.rpt`

![image](https://github.com/user-attachments/assets/6ce12c6f-70ea-4e8b-9921-e6fde3ca3c95)

* `report_timing -rise_from IN_A -sig 4 -nosplit -trans -cap -nets -inp > t2.rpt`
* `sh gvim t1.rpt -o t2.rpt`

![image](https://github.com/user-attachments/assets/6bfbc38e-92b1-431e-bdbf-a50b73005a4d)
![image](https://github.com/user-attachments/assets/25f6d5ba-d7bc-4733-98ba-7eb30c9db184)

* `report_timing -rise_from IN_A -sig 4 -nosplit -trans -cap -nets -inp -to REGA_reg/D > t3.rpt`
* `sh gvim t1.rpt -o t3.rpt &`

![image](https://github.com/user-attachments/assets/e0ce7310-166a-4575-9418-6b143233ff63)

## Min timing report

* ` report_timing -delay min -from IN_A `

![image](https://github.com/user-attachments/assets/6d312b7a-6350-4caf-ab51-48fd6b7edd7f)
![image](https://github.com/user-attachments/assets/e4c24856-8803-472b-9f26-368cf045fe32)

```
* Note: Clues to identify whether it is setup check or hold check
  * `Path type: min`, therefore it is doing hold check
  * The launch edge and capture edge are same (it is doing `zero cycle` check)
  * `Library hold time` is printed in the report
  * In the report it is `setup slack = data arrival time-data required time` (don't go by sign), this is for `min` path. 
```
* ` report_timing -thr U15/Y `

![image](https://github.com/user-attachments/assets/e8d60242-c82c-43e5-806f-c772a13fdef1)
![image](https://github.com/user-attachments/assets/78f2afad-d4a4-4b48-a0f9-23ffa68377a8)

* ` report_timing -thr U15/Y -delay min `

![image](https://github.com/user-attachments/assets/d277a314-b193-4ec0-85fb-05eb7b9e50a3)
![image](https://github.com/user-attachments/assets/3fede56a-c40c-4cfd-b8e1-eff6b4785b45)


</details>

<details>
<summary>Lab: Check_timing, Check_design, Set_max_capacitance, HFN </summary>
<br>

## Example is lab8_circuit_modified.v

* Invoke `dc_shell`
  
* `read_verilog /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/lab8_circuit_modified.v`

![image](https://github.com/user-attachments/assets/83e5394b-385c-4cbd-a154-e0f67c946fe9)

* `set target_library /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db`
* `set link_library {* /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db}'
* `link'

![image](https://github.com/user-attachments/assets/2309bf12-0ef3-4c32-9ffc-74c6f82e82b8)

* `check_design`

![image](https://github.com/user-attachments/assets/2db72843-38e7-4b83-966d-e5807c74b4e1)

* `compile_ultra`

![image](https://github.com/user-attachments/assets/1b61634f-b660-418b-a5f2-ba8bc35b3f32)

* `check_timing`: This command will ensure whether the design is properly constrained or not

![image](https://github.com/user-attachments/assets/7fe1c429-3661-4a29-afc3-66eaa24859c2)

* `report_constraints`

![image](https://github.com/user-attachments/assets/4d100e76-19f8-4e6d-9887-f6cbcda618cb)

* `source /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/lab8_cons_modified.tcl`
* `check_timing`

![image](https://github.com/user-attachments/assets/875ca490-a7a5-4cc1-993c-7b215d2b05ff)

* `report_timing`

![image](https://github.com/user-attachments/assets/5200bf7e-7cdb-4c7d-85b6-bf5a1938b08f)

* `report_constraints`

![image](https://github.com/user-attachments/assets/9ccebc7e-fe88-445e-acfb-e1c268cc65f5)
![image](https://github.com/user-attachments/assets/77825f6c-e415-4472-a651-356685d65667)

## Let us consider an example of 4:1 multiplexer to understand what is max_transistion, max_capacitance etc constraints

* `sh gvim /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/mux_generate.v`

![image](https://github.com/user-attachments/assets/47dfeff2-0b41-4834-aa99-f2f4d1770988)

* In GVIM write `( :sp mux_generate_128_1.v)` to change the design to 128:1 mux

![image](https://github.com/user-attachments/assets/766f2a14-d84b-453e-b22f-c2188313384a)

* mux_generate_128_1.v
```
module mux_generate (input [127:0] in, input [6:0] sel, output reg y);
integer k;
always @ (*)
begin
for(k = 0; k < 128; k=k+1) begin
	if(k == sel)
		y = in[k];
end
end
endmodule

```

* `read_verilog /home/vijayalaxmi/mux_generate_128_1.v`

![image](https://github.com/user-attachments/assets/9b9d7950-c448-4744-83c1-429e4fe37078)

* `check_design`
* `set target_library /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db`
* `set link_library {* /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db}'
* `link'

![image](https://github.com/user-attachments/assets/1c4b088a-2792-4556-aae5-29b90a2794b0)

* `compile_ultra`

![image](https://github.com/user-attachments/assets/45bd769f-cec7-4905-884f-1872cc885fd9)

* `write -f verilog -out mux_generate_128_1_net.v`

![image](https://github.com/user-attachments/assets/ccba62cd-2df6-4bcc-812a-03c3d8c1a2a3)

* `sh gvim /home/vijayalaxmi/mux_generate_128_1_net.v`

![image](https://github.com/user-attachments/assets/70e05d05-3f62-418d-aef0-3b416819a5b4)
![image](https://github.com/user-attachments/assets/3bd055c1-6049-4c4d-9133-bfd0b1bcac65)

* `get_cells * -hier -filter "is_sequential == true" `
* `get_cells * -hier -filter "is_sequential == false"`

![image](https://github.com/user-attachments/assets/99b29a1e-9e7a-4fbb-bec7-e8e00348ef0d)

* `report_timing -net -cap`

![image](https://github.com/user-attachments/assets/cfeb444f-22f7-47b4-a594-38fd8badb070)
![image](https://github.com/user-attachments/assets/74e01a22-802c-428e-9cad-75f8ad25275d)

* `check_timing` (y is unconstrained)

![image](https://github.com/user-attachments/assets/423a750c-7fae-461b-b7b5-137287405496)

* `set_max_delay -from [all_inputs] -to [all_outputs] 3.5`
* `report_timing`

![image](https://github.com/user-attachments/assets/65e75bec-b47c-4463-84bd-39407d340aa5)
![image](https://github.com/user-attachments/assets/54c95435-7fe8-4bca-9359-41b7ea20aabb)

* `set_max_capacitance 0.025 [current_design]`
* Command to check all the violating constraints: `report_constraint -all_violators`

![image](https://github.com/user-attachments/assets/7e498e5e-1a82-46f5-b75e-066b9d645e31)
![image](https://github.com/user-attachments/assets/71304ae4-fba1-47b0-bc13-0c84c087ed63)

* `compile_ultra`
* 'check_timing`

![image](https://github.com/user-attachments/assets/c3d84ebd-8f9f-42d2-ab4e-ac71f8641dd3)

* `report_constraints`

![image](https://github.com/user-attachments/assets/b94be1c4-7d09-49cd-a65e-8947eb0bed38)
![image](https://github.com/user-attachments/assets/b6c70839-c0a0-424b-a34f-32492f60a1d1)

* `report_timing`

![image](https://github.com/user-attachments/assets/b1f2bdc1-5a0a-4dfa-a7b6-2e35fb6ba2b6)
![image](https://github.com/user-attachments/assets/e5616397-3494-4310-ad75-36f274f3cb06)

* `report_timing -net -cap -sig 4`
  * Limit the capacitance so that high fanout nets are buffered properly

![image](https://github.com/user-attachments/assets/98c6429a-11c5-4094-bab3-cdba0b380f70)
![image](https://github.com/user-attachments/assets/519a8ef5-3633-4056-9c4d-c2e17528993d)

# High Fanout Net (HFN) : As the complexity of circuit increases, net will be heavily loaded due to large `fanout` this is called HFN

* Example of 128:1 mux scenario is shown here

![image](https://github.com/user-attachments/assets/a901f965-c0be-4c15-a445-1c23eaaf3f7b)

# Another example of HFN is given here:

![image](https://github.com/user-attachments/assets/29f4f978-dda5-477c-bd2e-b26d2acf3fc9)

## Let us execute the above example in dc_shell

* `gvim en_128.v`

![image](https://github.com/user-attachments/assets/4197719e-045f-46d9-8921-43d3de111ea6)


* Invoke `dc_shell`
* read_verilog /home/vijayalaxmi/en_128.v

![image](https://github.com/user-attachments/assets/53809ea4-8104-4609-b733-39c407507fb3)

* `set target_library /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db`
* `set link_library {* /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db}'
* `link'

![image](https://github.com/user-attachments/assets/54c71499-2d64-4eb1-8564-304c92273346)

* `compile_ultra`
* `report_timing`

![image](https://github.com/user-attachments/assets/8ac00e9d-463e-4996-867f-cb93b5532a99)
![image](https://github.com/user-attachments/assets/b27bd73f-0575-48eb-a737-69f52e27ebce)

* `report_timing -from en -inp -nets -cap`

![image](https://github.com/user-attachments/assets/8c6c915d-9aea-47db-8410-90f5bf9107ac)

* `set_max_capacitance 0.03 [current_design]`
* 'report_constraints`

![image](https://github.com/user-attachments/assets/5b312230-c9b0-4e0b-8b61-a426e3f5b397)

* `compile_ultra`
* `report_timing -from en -inp -nets -cap -sig 4`

![image](https://github.com/user-attachments/assets/9a9a4d42-18a0-449f-bb6e-6c9882822542)
![image](https://github.com/user-attachments/assets/2ee72f0d-8933-40ba-b2f1-f8462783dc81)

* `write -f ddc -out en_128.ddc`

![image](https://github.com/user-attachments/assets/797b8c3d-08bc-4380-96f9-202425676e73)

* Launch `design_vision`
* `read_ddc /home/vijayalaxmi/en_128.ddc`

![image](https://github.com/user-attachments/assets/6c5b2719-88f2-403e-bd84-0265615cb784)
![image](https://github.com/user-attachments/assets/dca4b23b-437b-481d-aa98-0cf389657961)
![image](https://github.com/user-attachments/assets/2fae0247-34db-4977-b74d-9178a8d44b6e)

</details>

