# Basics of STA (Static Timing Analysis)

<details>
<summary>Introduction to STA </summary>
<br>

##### Max Delay Constraint
![image](https://github.com/user-attachments/assets/8aa430b2-ce66-4d64-9ed0-eb3a897e0372)

##### Min Delay Constraint

![image](https://github.com/user-attachments/assets/a15699c2-a3b9-420d-8195-69c3aa66cfc5)
![image](https://github.com/user-attachments/assets/1d050675-25e9-42d5-8bb3-ef61b85962dd)

##### Why Delay: Water Bucket Analogy
###### Example 1
![image](https://github.com/user-attachments/assets/f037b92f-3b0f-427e-b35e-8eafe105b42f)

+ Delay is a function of Inflow
+ Inflow of water ----> Inflow of current
+ Therefore Faster current source is having less delay

###### Example 2
Delay = function (load capacitance)

![image](https://github.com/user-attachments/assets/b7844bee-5d1f-4e62-af7d-5270da7296b9)

#### Is delay of cell is constatnt?

###### Delay of gate = function (input transition, output load)

![image](https://github.com/user-attachments/assets/f7db544a-5136-42b7-a651-195aff60e360)

### Timing Arcs

#### Combinational Cell

+ Delay information from every input pin to every output pin which it can control is present in timing arcs
+ Example
![image](https://github.com/user-attachments/assets/0918f0f6-9d08-4c3a-b5b0-e71a6b485a74)

#### Sequential Cell [D flip-flop, D latch]

![image](https://github.com/user-attachments/assets/2476ba4f-85bb-45bf-9a55-b4fa435cbed5)

![image](https://github.com/user-attachments/assets/9780917c-2140-4326-ae93-3ebc5e54675b)

![image](https://github.com/user-attachments/assets/2951cb01-67ca-49c6-8e0d-9b24cd9e20f3)

</details>

<details>
<summary>What are Constraints </summary>
<br>

#### What are timing paths and how it affects design?

###### Example
![image](https://github.com/user-attachments/assets/562cc8c4-3298-408c-9b63-7433c5b74097)

###### Start and End points of timing paths

![image](https://github.com/user-attachments/assets/b78223ce-93cb-44ae-a385-79c638b52fef)

##### Timing Paths Summary

![image](https://github.com/user-attachments/assets/e4d68547-4f3e-4d92-8ea3-8735dc7582af)


#### Constrainig the Design- Why Constraints?

##### Example 1
![image](https://github.com/user-attachments/assets/2308f304-3aa5-45f3-82e7-ff566530c558)

###### Example 2

![image](https://github.com/user-attachments/assets/d42e3127-eece-41f8-a625-e3aa6d1eaa52)


</details>

<details>
<summary>IO Constraints </summary>
<br>

##### Is IO Delay Modelling Sufficient?

![image](https://github.com/user-attachments/assets/d6399d90-606d-41f3-a195-fc4f21ba9b49)

![image](https://github.com/user-attachments/assets/38425de3-8995-4315-96ab-78a8a089e121)

+ Note: 70:30 rule that is 70% (External Delay) and 30% (Internal Delay)

### Summary
![image](https://github.com/user-attachments/assets/8dfd992f-f574-406f-9dcc-478ce064b410)


</details>

<details>
<summary>Lab 5: Timing dot libs </summary>
<br>

## Details about sky130_fd_sc_hd__tt_025c_1v80.lib

#### Max capacitance limit in lib is 1.5 pF because of the following reasons

![image](https://github.com/user-attachments/assets/5da1668e-06e3-40dc-ba38-80d48eec72bf)

#### Delay Model: Look up table

![image](https://github.com/user-attachments/assets/d3902f10-8156-439a-9d24-dbc8e1527712)

* similarly power consumed by the cell is alo LUT (look up table)
* .lib has information about power pins
* max transistion allowed per pin
* For every pin direction is mentioned
* clok pin attribute is true for flops
* functionality is mentioned
* The tool uses unateness information to propagate the transistion
  ![image](https://github.com/user-attachments/assets/44f3bb67-8bf4-4a80-8468-ab4cd9b68db6)


</details>


<details>
<summary>Lab 6: Exploring dot libs part 1 </summary>
<br>

## Sequential timing arcs
* CLK_N pin means active low clock and its attribute is 'TRUE' means it is clock
* for D pin clock attribute is 'FALSE'
![image](https://github.com/user-attachments/assets/eac8a866-2088-4f96-a5fe-370f3ebed833)
* CLK_N is non_unate because Q may be rising or falling depending on the clock.
![image](https://github.com/user-attachments/assets/7dd14784-fe4d-4156-9429-2d17fc15d1f4)

* echo $target_library
* command to look for library cells: get_lib_cells * -filter "is_sequential == true "
* get_lib_cells */* -filter "is_sequential == true"
![image](https://github.com/user-attachments/assets/451af0b3-3347-47c4-bd44-054f2d2ae3d8)

  
</details>


<details>
<summary>Lab 7: Exploring dot libs part 2 </summary>
<br>

* list_lib shows the library that is already loaded
![image](https://github.com/user-attachments/assets/81b12b70-ffd0-4555-83ae-bc7b9a9a0c4a)

* command to see the AND gates available in library: get_lib_cells */*and*

![image](https://github.com/user-attachments/assets/165c933d-f728-461f-8a51-1be5f839e19a)

## To display the cells one by one
* foreach_in_collection my_lib_cell [get_lib_cells */*and*] { 
set my_lib_cell_name [get_object_name $my_lib_cell]; echo $my_lib_cell_name; 
}
![image](https://github.com/user-attachments/assets/cea88f16-8db8-4677-a5bc-aa91c1523a67)

* To see what are all the pins in particular cell: get_lib_pins sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__and2_0/*
![image](https://github.com/user-attachments/assets/b73cedec-36f7-4812-8b78-48d9000baeff)

* Script to display the direction of pin
* foreach_in_collection my_pins [get_lib_pins sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__and2_0/*] {
  set my_pin_name [get_object_name $my_pins];
  set pin_dir [get_lib_attribute $my_pin_name direction];
  echo $my_pin_name $pin_dir
  }
![image](https://github.com/user-attachments/assets/c686c1aa-f28d-4333-8839-a17f0bb19993)

*command to check the functionality: get_lib_attribute sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__and2_0/X function

![image](https://github.com/user-attachments/assets/46d5a09d-6d3e-4b92-be8c-214202f6bc14)
* Similarly we can check for nand gate
![image](https://github.com/user-attachments/assets/81ec3e9c-4041-445e-92ae-e6481a5397d3)

* get_lib_pins sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__nand4_1/*
* foreach_in_collection my_pins [get_lib_pins sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__nand4_1/*] {
  set my_pin_name [get_object_name $my_pins];
  set pin_dir [get_lib_attribute $my_pin_name direction];
  echo $my_pin_name $pin_dir
  }

  ![image](https://github.com/user-attachments/assets/84e1e8ca-bacb-49ba-b924-1b958c486960)

## Let see what is sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__and2b_1
* get_lib_pins sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__and2b_1/*
* foreach_in_collection my_pins [get_lib_pins sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__and2b_1/*] {
  set my_pin_name [get_object_name $my_pins];
  set pin_dir [get_lib_attribute $my_pin_name direction];
  echo $my_pin_name $pin_dir
  }
* get_lib_attribute sky130_fd_sc_hd__tt_025C_1v80/sky130_fd_sc_hd__and2b_1/X function
  
![image](https://github.com/user-attachments/assets/7bde1731-9d0d-424c-84c2-61a5b16b5b8a)

  
</details>

