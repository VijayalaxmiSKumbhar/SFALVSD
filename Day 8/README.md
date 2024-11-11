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



</details>

<details>
<summary>Lab 17: Sequential optimizations </summary>
<br>


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


</details>

<details>
<summary>Lab 19: Register Retiming </summary>
<br>


</details>

<details>
<summary>Lab 20: Isolating output ports </summary>
<br>


</details>

<details>
<summary>Lab 21: MultiCycle Path </summary>
<br>


</details>

