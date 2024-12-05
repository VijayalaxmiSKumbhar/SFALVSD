# Optimizations

<details>
<summary>Optimizations Combinational Opt </summary>
<br>

## Optimization Goals

![image](https://github.com/user-attachments/assets/a8135796-1f45-4329-bc6d-37f2554d8085)

## Combinational Logic Optimisation

![image](https://github.com/user-attachments/assets/28991cd8-3449-4930-aed5-4969281bdfd5)


#### Constant Propagation Example

![image](https://github.com/user-attachments/assets/6da28658-835c-439c-8978-1183678a96e6)

#### Boolean Logic Optimisation

![image](https://github.com/user-attachments/assets/bdd5c08a-1f42-469a-9f12-d081c6bcdcd6)

#### Resource Sharing (Very Important)

![image](https://github.com/user-attachments/assets/bafde63c-5c60-41c0-87d6-a49f8ca1a979)

#### Logic Sharing: Look for common logic across multiple expressions and does logic sharing (Very Important)

![image](https://github.com/user-attachments/assets/6ff72061-aee8-4f19-a05f-d7147bbfcfa7)

#### Balanced Vs Preferential Implementation

![image](https://github.com/user-attachments/assets/5c818d0a-a33a-4fa8-ab92-fe1db0c69edc)

</details>

<details>
<summary>Sequential Optimizations </summary>
<br>

## Sequential Logic Optimisations

![image](https://github.com/user-attachments/assets/74069174-b6ce-4640-af78-935cd3e3a5af)

#### Case-I (Sequential constant)

![image](https://github.com/user-attachments/assets/8ebdaca2-f613-4150-9990-26b568ebe76c)

#### Case-II (Sequential constant)

![image](https://github.com/user-attachments/assets/74ee4723-aa13-4432-b2fb-d7db5ba1da32)

#### case-III (Not a Sequential constant)

* As the circuit is retained as it is, it will not be optimized.

![image](https://github.com/user-attachments/assets/efe3d221-8f84-4361-a81b-5bb2f1278d6e)

#### Case-IV (Not a sequential constant)

![image](https://github.com/user-attachments/assets/444c9df8-e8fb-4b44-a691-8150eec73718)

#### Example of sequential optimization with sequential constant and constant propogation

![image](https://github.com/user-attachments/assets/61ecad4f-bbda-48ba-bbce-2250525abbf6)

#### Optimization of Unloaded Outputs

![image](https://github.com/user-attachments/assets/68ff42ec-28d0-44b6-9357-46a24948adf4)

#### Controlling Sequential Optimizations in DC

![image](https://github.com/user-attachments/assets/f2da94c2-689a-426e-9486-b0aa34bea781)


</details>

<details>
<summary>Lab 16: Part 1 Combinational_optimizations </summary>
<br>

* `sh gvim opt_check*.v -o`

![image](https://github.com/user-attachments/assets/6f4ab869-8298-4f42-9097-803e81ee25ac)

* `opt_check.v` functionality is

![image](https://github.com/user-attachments/assets/7fb8f0ed-e776-4a41-9667-3934355c2a34)

* `read_verilog opt_check.v`

![image](https://github.com/user-attachments/assets/aabd2c2e-5aa7-43f0-884b-505f44f62cfa)
![image](https://github.com/user-attachments/assets/85034c06-5a4d-44b2-851d-594192cba763)

* `report_timing`

![image](https://github.com/user-attachments/assets/be9213be-3b9d-4453-ad54-d1f8e9031382)

* `link`
* `compile_ultra`

![image](https://github.com/user-attachments/assets/23dd4e9c-1df1-4eac-b7f9-6b9ae18079c0)

* `report_timing`

![image](https://github.com/user-attachments/assets/b9ff8680-f764-4158-92b1-3a99ff1c2142)

* `get_cells *`
* `report_timing -to y2`

![image](https://github.com/user-attachments/assets/a85d035c-5ae5-47a7-87a1-379499c8709c)
![image](https://github.com/user-attachments/assets/d25aa38e-7d1b-48e5-9297-d4f741bfd493)

* Launch design_vision

![image](https://github.com/user-attachments/assets/0c2ebe6f-bb5c-4f4e-827d-d5121943796e)

* in dc_shell: `write -f ddc -out opt_check.ddc`

![image](https://github.com/user-attachments/assets/1db117e7-fbd4-4f20-9c47-d98148d6be8a)

* in design_vision: `read_ddc opt_check.ddc`

![image](https://github.com/user-attachments/assets/92a85710-046a-46d8-bb14-04600d9137d7)

##### y1 = a.b and y2 = c bar

![image](https://github.com/user-attachments/assets/c9bb4038-1f30-41f2-94d6-801b5077e368)

* To load the other designs `reset_design` in dc_shell as well design_vision

* The functionalities implemented by opt_check2.v, opt_check3.v and opt_check4.v are as follows

![image](https://github.com/user-attachments/assets/2cb3f5a9-c7b6-4aa7-bb59-4a331a2ad167)

##### In design_vision give the following commands

* `read_verilog opt_check2.v`

![image](https://github.com/user-attachments/assets/27c37063-b2d5-4a8b-8bb5-c3f4d6332215)

* `link`
* `compile`

![image](https://github.com/user-attachments/assets/32083478-9e38-4740-8d37-c65b18f66481)
![image](https://github.com/user-attachments/assets/1a15d8ae-bc15-4804-88a2-0fe16aace093)

#### Similarly for opt_check3.v

* `read_verilog opt_check3.v`
* `link`
* `compile`

![image](https://github.com/user-attachments/assets/1f184984-03d9-4a0e-a616-330e84617ed9)

#### Similarly for opt_check4.v

* `read_verilog opt_check4.v`
* `link`
* `compile`

![image](https://github.com/user-attachments/assets/af6c6f94-b4ca-41e8-9118-2ea5d4aa802e)

* `report_timing -to y`

![image](https://github.com/user-attachments/assets/347c19c8-7cd1-473d-bcc3-82b15477067b)

* `set_max_delay 0.06 -from [all_inputs] -to [get_ports y]`

![image](https://github.com/user-attachments/assets/c1115a48-3a98-4f44-ab65-bd0458e007cf)

* `report_timing`

![image](https://github.com/user-attachments/assets/d908476a-4325-4c4a-a782-c400bad61424)

* `compile_ultra`
* `report_timing`
* In the result still SLACK is Violated means further optimization is not done
  
![image](https://github.com/user-attachments/assets/2f36e74b-9bcf-4ecb-84de-091554b4f5ee)

##### To optimize the design further

* get_lib_cells */sky130_fd_sc_hd__xnor2*

![image](https://github.com/user-attachments/assets/aa9b9dda-8088-4091-a046-506c3a894704)

* `size_cell U3 sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__xnor2_4` (`size_cell` is the command used to up size or down size the cell)
  
![image](https://github.com/user-attachments/assets/f91d9288-3885-419c-a8a5-5b360bc1c6a2)

* `report_timing`

![image](https://github.com/user-attachments/assets/a33f2076-7328-481e-bbb9-85047a5e37d0)

##### Commands used for executing `opt_check4.v`

```

csh
design_vision
read_verilog opt_check4.v
link
compile
report_timing -to y
set_max_delay 0.06 -from [all_inputs] -to [get_ports y]
report_timing
compile_ultra
report_timing
get_lib_cells */sky130_fd_sc_hd__xnor2*
size_cell U4 sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__xnor2_4
size_cell U3 sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__xnor2_4
report_timing
compile_ultra
report_timing

```

</details>

<details>
<summary>Lab 16: Part 2 resource sharing optimizations </summary>
<br>

#### Note : All the dc commands work in design_vision als

* Launch the design_vision

* `csh`
* `design_vision`

##### Example here is resource_sharing_mult_check.v

![image](https://github.com/user-attachments/assets/c61658a9-aa5d-4539-9c1b-ab23125183b4)

```
* read_verilog resource_sharing_mult_check.v
* link
* compile_ultra

```

![image](https://github.com/user-attachments/assets/e548ece9-5566-4e1c-8c02-0fecd4af2686)

* To know the area of design : `report_area`

![image](https://github.com/user-attachments/assets/f770a72f-0cc9-4241-b479-5222991bc949)
![image](https://github.com/user-attachments/assets/5d6f0866-fded-40ff-9a4e-d67089e9aa37)
![image](https://github.com/user-attachments/assets/97de5c56-0f42-43cc-82ee-8d80b8a1c114)
![image](https://github.com/user-attachments/assets/70e5eda2-65d5-4bbd-8fb2-11bf51e3850a)


* `set_max_delay -from [all_input] -to [all_outputs]`

![image](https://github.com/user-attachments/assets/c6e314e3-ce04-475d-ab83-22dd1bcf6635)

* `report_timing`

![image](https://github.com/user-attachments/assets/514f5326-aeb7-408e-9309-177be8e35ccf)

* `compile_ultra`
* `report_timing`
* `report_area`

![image](https://github.com/user-attachments/assets/88f3fca8-be32-4c40-9691-d2a938bdb456)
![image](https://github.com/user-attachments/assets/c88f55b0-a749-4c46-b4b4-ac866dca71f7)
![image](https://github.com/user-attachments/assets/7078672f-5b18-4238-9f3d-cf48f8117a77)

##### The following delays are given to further improve the area

![image](https://github.com/user-attachments/assets/7d23c20f-4af1-47c9-a0ee-65b2665cfa4b)

* ` set_max_delay -from sel -to [all_outputs] 0.1'

![image](https://github.com/user-attachments/assets/321421d6-8fcf-4503-a585-b06f38955dff)

* `report_timing`
![image](https://github.com/user-attachments/assets/0ca705df-4fd7-41f1-add2-86544807e10f)
![image](https://github.com/user-attachments/assets/6fcdd6c6-5ceb-4ed7-9fe6-8b9721eac4af)

* `compile_ultra`
* `report_area`

![image](https://github.com/user-attachments/assets/6deab9ab-a4c9-4553-a3f5-59ddf5826696)
![image](https://github.com/user-attachments/assets/828a9927-0a84-4302-a9e0-2c6ca25ceadd)

##### After executing the above commands the tool is pushing the 2:1 mux towards output

![image](https://github.com/user-attachments/assets/103806a2-3df8-479d-bc93-c6a2efc5b569)

* `report_timing -sig 4`

![image](https://github.com/user-attachments/assets/22f66cfe-a17a-408e-880a-9fb72c008eec)

* command to constrain the area is: `set_max_area 800`

![image](https://github.com/user-attachments/assets/60e9dd4c-ed4e-4e65-a568-ab47a4120b01)

* `compile_ultra`
* `report_area`

![image](https://github.com/user-attachments/assets/a067c2ed-3cd9-491c-97b3-83b92d844a81)
![image](https://github.com/user-attachments/assets/f9bb3896-f797-4f77-a361-5365a8b715f5)
![image](https://github.com/user-attachments/assets/8a725af2-90d8-415d-aaed-c118e2c9d4c3)


##### Summary of results

![image](https://github.com/user-attachments/assets/c00ef366-410a-4722-bf0d-81ffa88e10ca)


</details>

<details>
<summary>Lab 17: Sequential optimizations </summary>
<br>

##### Examples used for sequential optimization are:

![image](https://github.com/user-attachments/assets/c3a8ff0b-6e44-447a-90be-02d9917d4398)

##### Launch dc_shell

* `csh`
* `dc_shell`

* `read_verilog dff_const1.v`

![image](https://github.com/user-attachments/assets/958e3c1c-62cc-4614-ac4f-c7f2c7f2cc32)

* `link`
* `compile`
* `get_cells`

![image](https://github.com/user-attachments/assets/fc04c89e-893a-446b-a8ed-74d743b372c5)

* ` foreach_in_collection my_cell [get_cells *] {
    set cell_name [get_object_name $my_cell];
    echo $cell_name;
    } `

![image](https://github.com/user-attachments/assets/d8562abd-aea8-473f-b562-c81edeb94aae)

* ` foreach_in_collection my_cell [get_cells *] {
    set cell_name [get_object_name $my_cell];
    set rn [get_attribute [get_cells $cell_name] ref_name];
    echo $cell_name $rn;
    } `

![image](https://github.com/user-attachments/assets/97209f43-1e8e-4be1-92a2-f3d910d1af16)

##### Now launch design_vision

* `csh`
* `design_vision`

* `read_verilog dff_const1.v`

![image](https://github.com/user-attachments/assets/ea04f7b7-ffd8-4edd-8504-ec9a596684b2)


  
</details>

<details>
<summary> Special optimizations </summary>
<br>

#### Example for illustration

![image](https://github.com/user-attachments/assets/76a8a5c7-d584-41f2-8d00-246d239e1d95)

#### Let us see how to improve the frequency of above circuit

* The solution to improvise the frequency is retiming.
* By reducing the critical path delay frequency can be improved.

![image](https://github.com/user-attachments/assets/1d1de245-e699-4ed0-b4fc-1bb30331f31b)

* The total criticalpath delay of 48 ns is divided into 3 parts and frequency is improved. Earlier it was 20 MHz, after register retiming frequency is increased to 50 MHz.

![image](https://github.com/user-attachments/assets/06f9f8db-e965-4f57-9164-0da8f6334545)

#### Boundary Optimization

![image](https://github.com/user-attachments/assets/219d5346-188b-4b07-90a3-879b606aaed5)

* Switch to control the boundary oprimization is
![image](https://github.com/user-attachments/assets/cdea923b-d34a-4b69-b32c-44fb31d72f1c)

#### Multi-cycle Paths

![image](https://github.com/user-attachments/assets/93645bc3-99a7-41ea-b73f-3de29878282d)

#### False Paths

![image](https://github.com/user-attachments/assets/8516cb62-e8d8-429d-b50f-368472486052)

#### External Load Vs Internal Loads

* Example Illustration
  
![image](https://github.com/user-attachments/assets/74a474c8-0982-44b3-a490-63092d048291)

* Solution is set_isolate_ports

![image](https://github.com/user-attachments/assets/a89b0a51-2dca-4703-89fd-992f39eb4e8a)

 </details>

<details>
<summary>How Paths are timed Multi Cycle Path (MCP)?</summary>
<br>

#### How DC/STA tool checks timing?

* Example 1: Single Cycle Paths

![image](https://github.com/user-attachments/assets/8bf221bb-66e8-4149-bb15-ef8fadc9eb69)

* Half Cycle Paths: Only half cycle of the clock is involved.

 ![image](https://github.com/user-attachments/assets/3ccf3b6d-c845-4bbf-8286-1ce5e854557a)

 * Multi cycle path for setup

![image](https://github.com/user-attachments/assets/76915c48-030e-4692-83a5-ec21973d2490)

![image](https://github.com/user-attachments/assets/caa7ccff-5318-4619-bf49-0efb2f0a65a7)

![image](https://github.com/user-attachments/assets/06d7fa6a-db6e-4b9a-9163-936e18b3f3bc)

</details>

<details>
<summary>Lab 18: Boundary optimizations </summary>
<br>

## What is boundary optimization?

![image](https://github.com/user-attachments/assets/f57e99d4-fb73-434a-ac9c-c5829d962860)

## Example is check_bounday.v

* ` sh gvim /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_boundary.v`
  
![image](https://github.com/user-attachments/assets/386e89dd-7475-4e1a-ace7-0722397b0d9f)

## Above program implements the following logic

![image](https://github.com/user-attachments/assets/ce101132-a162-497e-9b56-ca591917e40e)

* `reset_design`
* `read_verilog /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_boundary.v`

![image](https://github.com/user-attachments/assets/84d9bda8-0db6-458c-9516-4eaa399d7149)

 * `set target_library /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db`
 * `set link_library {* /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db}`
 * `link`
 
  ![image](https://github.com/user-attachments/assets/ecdd965e-14e4-416a-9268-0fc6ffbe0fc8)

 * ` compile_ultra`

![image](https://github.com/user-attachments/assets/dd88db25-38cd-4acf-8a25-b8c427f61404)
![image](https://github.com/user-attachments/assets/ad5f6782-b4a3-4c2e-b2af-ff919c11bd3f)

* ` write -f ddc -out boundary.ddc `
*  ` get_cells `

![image](https://github.com/user-attachments/assets/34cbd4b6-4e43-413b-9ddb-0f31a49f17a3)

## Launch design_vision

* ` read_ddc /home/vijayalaxmi/boundary.ddc `

![image](https://github.com/user-attachments/assets/d6fcbcff-9292-47d5-9fec-e06105358688)
![image](https://github.com/user-attachments/assets/e31cf82d-af29-4ce0-89c8-41fcd23d33d8)
![image](https://github.com/user-attachments/assets/1212a71f-932f-4acb-9ffb-4053fa461438)

## In dc_shell give the command ` get_pins u_im/* `: This shows that boundary optimization has happened.

![image](https://github.com/user-attachments/assets/931b89de-7266-4f14-ac96-1e8d1933db7d)

```

* Commands given in design_vision are as follows: 

dc_shell> gui_start
4.1.1
design_vision> read_verilog /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_boundary.v
Loading db file '/usr/synopsys/syn/T-2022.03-SP5-6/libraries/syn/gtech.db'
Loading db file '/usr/synopsys/syn/T-2022.03-SP5-6/libraries/syn/standard.sldb'
  Loading link library 'gtech'
Loading verilog file '/home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_boundary.v'
Detecting input file type automatically (-rtl or -netlist).
Reading with Presto HDL Compiler (equivalent to -rtl option).
Running PRESTO HDLC
Warning: Can't read link_library file '$target_library'. (UID-3)
Compiling source file /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_boundary.v

Inferred memory devices in process
        in routine check_boundary line 5 in file
                '/home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_boundary.v'.
===============================================================================
|    Register Name    |   Type    | Width | Bus | MB | AR | AS | SR | SS | ST |
===============================================================================
|     val_out_reg     | Flip-flop |   4   |  Y  | N  | Y  | N  | N  | N  | N  |
===============================================================================

Inferred memory devices in process
        in routine internal_module line 18 in file
                '/home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_boundary.v'.
===============================================================================
|    Register Name    |   Type    | Width | Bus | MB | AR | AS | SR | SS | ST |
===============================================================================
|       cnt_reg       | Flip-flop |   3   |  Y  | N  | Y  | N  | N  | N  | N  |
===============================================================================
Presto compilation completed successfully.
Current design is now '/home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_boundary.db:check_boundary'
Loaded 2 designs.
Current design is 'check_boundary'.
check_boundary internal_module
Current design is 'check_boundary'.
design_vision> link
Warning: Can't read link_library file '$target_library'. (UID-3)

  Linking design 'check_boundary'
  Using the following designs and libraries:
  --------------------------------------------------------------------------
  * (2 designs)               /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_boundary.db, etc

1
design_vision> get_cells
{u_im val_out_reg[3] val_out_reg[2] val_out_reg[1] val_out_reg[0] U1}
design_vision> get_pins u_im/*
{u_im/clk u_im/res u_im/cnt_roll}
design_vision> set_boundary_optimization u_im false
1
design_vision> compile_ultra

```

![image](https://github.com/user-attachments/assets/416cee8f-da02-445b-bc3f-0237f1df01a7)
![image](https://github.com/user-attachments/assets/487741b6-6b74-4a98-9026-4e75cbe1ceba)


</details>

<details>
<summary>Lab 19: Register Retiming </summary>
<br>

## Example is check_reg_retime.v

![image](https://github.com/user-attachments/assets/fee3adff-3942-4a67-bcca-ddc7df67d06f)

## Launch design_vision

* ` sh gvim /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_reg_retime.v `
  
![image](https://github.com/user-attachments/assets/ca4c353a-37c0-4778-a868-5324115034ae)

* ` read_verilog /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_reg_retime.v `
*  `link`
*  `compile`

![image](https://github.com/user-attachments/assets/06f20093-bc5b-4071-a0b0-f1a604f72c67)

* `report_timing`

![image](https://github.com/user-attachments/assets/758dfe6f-38b4-4027-8454-53c68381b2e1)
![image](https://github.com/user-attachments/assets/39e046d1-5db7-410a-aa71-2ea3e66ac721)
![image](https://github.com/user-attachments/assets/f3f4cdb1-cb4f-4c1b-acc2-222feed97d44)
![image](https://github.com/user-attachments/assets/ea07f8f2-3c3b-47cc-b388-a7db3524c5b6)

* ` source /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/reg_retime_cons.tcl `

![image](https://github.com/user-attachments/assets/e209ad97-48e9-44ea-8897-c73b36f44afb)

* ` report_clocks `

![image](https://github.com/user-attachments/assets/d8cfe221-7767-44d5-9eec-2e611b7fef35)

*  ` report_timing `

 ![image](https://github.com/user-attachments/assets/9d38f480-c01f-4e1d-8882-346237cd280e)

* ` compile_ultra -retime `

![image](https://github.com/user-attachments/assets/2d96dd9c-82db-4a46-9546-c08f686eacfe)
![image](https://github.com/user-attachments/assets/34932710-32a1-4a1e-aac2-6e6933d48082)

* ` report_timing `

![image](https://github.com/user-attachments/assets/c3f82bf4-9942-4ac0-92b1-3d6a300bc40a)

* ` report_timing -from [all_inputs] `
* ` report_timing -from [all_inputs] -trans -cap -nosplit -sig 4 `

![image](https://github.com/user-attachments/assets/0eeb64a6-dec8-4dec-ad4c-0fb9913e8eec)


</details>

<details>
<summary>Lab 20: Isolating output ports </summary>
<br>

## Lab example is check_boundary.v

![image](https://github.com/user-attachments/assets/b9b21efd-3a1f-4247-a5bd-e6ab4d1d162f)

## Invoke design vision

* `sh gvim /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_boundary.v`

![image](https://github.com/user-attachments/assets/ec904cdf-c998-4398-92b6-5a422f4033e4)
![image](https://github.com/user-attachments/assets/42959631-5323-4955-adc2-845d795f1372)

* ` read_verilog /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_boundary.v`
*  `link`
*  `compile_ultra`

![image](https://github.com/user-attachments/assets/1191f681-f414-4f19-abf1-c02a6598a7b3)

* `set_isolate_ports -type buffer [all_outputs]`
* `compile_ultra`

![image](https://github.com/user-attachments/assets/308ff029-ff67-4e84-b4cb-6998cf13c904)

## Buffers added at the output can be observed in screenshot

![image](https://github.com/user-attachments/assets/69bc2d1a-24d0-47a1-84fb-9d33d22482d8)

## Launch dc_shell

* ` read_verilog /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/check_boundary.v`
* `set target_library /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db`
* `set link_library {* /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db}`
*  `link`

![image](https://github.com/user-attachments/assets/62dce77d-ef8a-4b97-8812-4bf94bf48c88)

*  `compile_ultra`

![image](https://github.com/user-attachments/assets/5a9727ff-02f5-4be3-b412-572b4314c567)

* `create_clock -per 5 -name myclk [get_ports clk]`
* `set_input_delay -max 2 [all_inputs] -clock myclk`
* `set_output_delay -max 2 [all_outputs] -clock myclk`
* `set_input_delay -max 2 [all_inputs] -clock myclk`

![image](https://github.com/user-attachments/assets/826619e5-c7ef-4a26-8828-e6d453b0b34f)

* `report_timing`

![image](https://github.com/user-attachments/assets/5cc94ce2-94c3-4989-bd48-c9ed58337ff1)

* `report_timing -nosplit -inp -cap -trans -sig 4`

![image](https://github.com/user-attachments/assets/69c9b5ba-ab2e-47b1-a567-14fca73ccf66)

* `set_isolate_ports -type buffer [all_outputs]`
* `compile_ultra`

![image](https://github.com/user-attachments/assets/9e3dd868-98d3-4e88-b1e2-9c0bfad6175e)

* `report_timing -nosplit -inp -cap -trans -sig 4`

![image](https://github.com/user-attachments/assets/ba9fe8c8-890d-4286-a803-16ca9b3c9f10)


</details>

<details>
<summary>Lab 21: MultiCycle Path </summary>
<br>

## Lab example is mcp_check.v

![image](https://github.com/user-attachments/assets/d1eab26a-5b97-427f-b39f-b2d86f15e3bb)

* ` sh gvim /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/mcp_check.v `

![image](https://github.com/user-attachments/assets/d4a069a4-bc1e-4fd8-8e17-d2b8b8a4bc0f)

* ` read_verilog /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/mcp_check.v`

![image](https://github.com/user-attachments/assets/c0e593c6-735a-4d2d-b5f1-e47b69e0a78c)

* `set target_library /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db`
* `set link_library {* /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db}`
*  `link`
*  `compile_ultra`

![image](https://github.com/user-attachments/assets/88eb8a59-4aef-4d32-a307-9506a164a579)
![image](https://github.com/user-attachments/assets/5260613d-31f7-4af1-aaf7-a20ad8a4008f)


## Constraint file used here is mcp_check_cons.tcl

* `sh gvim /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/mcp_check_cons.tcl`

![image](https://github.com/user-attachments/assets/69ba17bc-e8c5-4da4-bbb6-76ae255594a5)

* `source /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/mcp_check_cons.tcl`
* `report_timing`

![image](https://github.com/user-attachments/assets/81f99282-5c7e-4564-abc3-27cddf5644de)
![image](https://github.com/user-attachments/assets/96b7e82a-037c-4516-935e-e707c0558bd6)
![image](https://github.com/user-attachments/assets/f94679a6-3356-44ef-9fbc-475ebc531aee)

* `compile_ultra`

![image](https://github.com/user-attachments/assets/40b30d52-7bea-4e7b-a1a2-96a75674173a)

* `report_timing`

![image](https://github.com/user-attachments/assets/bbcf1649-f233-4f5e-b9ec-879d7765ff6f)
![image](https://github.com/user-attachments/assets/4b749ec8-c4de-4371-bfb1-55a85e331099)


</details>

