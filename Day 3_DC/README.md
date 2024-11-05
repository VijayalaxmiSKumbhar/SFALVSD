# Advanced Constraints

<details>
<summary> SDC (Synopsys Design Constraints) Part 1 Clock-Clock Tree Modelling-Uncertainity </summary>
<br>

#### Clock Generation

![image](https://github.com/user-attachments/assets/9eaa3e01-78dc-42a1-b1f0-4ec2d4590e11)

#### Clock Distribution

![image](https://github.com/user-attachments/assets/47b59124-3c0d-4143-8226-b38496555dd5)

#### Clock Skew

![image](https://github.com/user-attachments/assets/f00ec1cb-14d5-4c65-846e-072598ac6503)

#### Factors to be considered for clock Modelling

![image](https://github.com/user-attachments/assets/a0391b97-6515-4d3d-819d-58418337dcdf)

![image](https://github.com/user-attachments/assets/eeac7e23-212c-4ee8-8025-c35418b73daa)

#### Various Constraints

![image](https://github.com/user-attachments/assets/6791d375-80b0-466b-8ed2-d5a3b867996c)

</details>

<details>
<summary>SDC Part 2 IO Delays </summary>
<br>

## How to Constraint the design in DC

![image](https://github.com/user-attachments/assets/b033d2ef-c601-48a2-b82f-12b9cd35cb69)

## getting the ports in DC

![image](https://github.com/user-attachments/assets/a2df36af-334b-446d-b546-125be8224099)

## getting the clocks in DC

![image](https://github.com/user-attachments/assets/82fc0db8-31b7-4da3-9bec-b9633ec1c26b)

## Querying the cells in design

![image](https://github.com/user-attachments/assets/566d82fb-46af-4c59-ba94-a0d1a5be0293)

## Command to Create Clock

![image](https://github.com/user-attachments/assets/63862391-87d9-4166-952b-bcd4ad35b6cf)

## Practicalities of Clock Network

* ### Latency
* ### Uncertainity

![image](https://github.com/user-attachments/assets/52502fbc-5b23-4464-8740-dcf69a4e0d0f)

## Clocks-Waveform

![image](https://github.com/user-attachments/assets/503c3bd4-2147-4404-b343-47d6c08840f9)

## How to constraint the Input Path?

![image](https://github.com/user-attachments/assets/718a3076-f15a-4151-af79-c6e8c603dfcc)

## How to constraint the Output Path?

![image](https://github.com/user-attachments/assets/3f5df8f9-ec63-4908-ba93-02d0ef52b1ef)

## Summary of SDC Commands

![image](https://github.com/user-attachments/assets/5f8467b7-e588-4d34-829c-ff72978076c9)

</details>

<details>
<summary>Lab 8: Loading design get_cells, get_ports, get_nets </summary>
<br>

## Example: Implementation of the circuit

![image](https://github.com/user-attachments/assets/71d2547d-607e-4a7d-a99e-3ea45a94662d)


* Verilog Code

```
module lab8_circuit (input rst, input clk , input IN_A , input IN_B , output OUT_Y , output out_clk);
reg REGA , REGB , REGC ; 

always @ (posedge clk , posedge rst)
begin
	if(rst)
	begin
		REGA <= 1'b0;
		REGB <= 1'b0;
		REGC <= 1'b0;
	end
	else
	begin
		REGA <= IN_A | IN_B;
		REGB <= IN_A ^ IN_B;
		REGC <= !(REGA & REGB); 
	end
end

assign OUT_Y = ~REGC;

assign out_clk = clk;

endmodule

```

* csh
* dc_shell
* echo $target_library
* echo $link_library
* read_verilog /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/lab8_circuit.v
![image](https://github.com/user-attachments/assets/9fd48c84-0b5e-401a-9f89-6d3134d1617f)

*link

*compile_ultra

![image](https://github.com/user-attachments/assets/cf351e9f-9f59-47b9-8342-ab78c0b1eebb)

* get_ports
* foreach_in_collection my_port [get_ports *] {
  set my_port_name [get_object_name $my_port] ; echo $my_port_name; }

![image](https://github.com/user-attachments/assets/b21a1a88-20e8-48bc-a98d-999d1cc57d06)

# To know the direction of ports
* get_ports rst
* get_attribute [get_ports rst] direction

![image](https://github.com/user-attachments/assets/c8d29256-af66-45a0-8f6d-1287c68a7fae)

# Script to print direction of all ports
* foreach_in_collection my_port [get_ports *] {
set my_port_name [get_object_name $my_port] ;
set dir [get_attribute [get_ports $my_port_name] direction]
echo $my_port_name $dir;
}

![image](https://github.com/user-attachments/assets/bf5e5710-dfa4-4c7e-a25d-6a315fdff7ad)

# To know whether the cells are logical or physical

* get_cells *
* get_attribute [get_cells U9] is_hierarchical
* get_attribute [get_cells U12] is_hierarchical
* get_attribute [get_cells REGA_reg] is_hierarchical
* get_cells * -hier -filter "is_hierarchical == false"
* get_cells * -hier -filter "is_hierarchical == true"

![image](https://github.com/user-attachments/assets/c343d169-b030-467e-9770-9bb9dc71a992)

* Example illustrating logical/phyiscal cells
![image](https://github.com/user-attachments/assets/7e10e33a-b057-4193-bceb-649dfeedb340)

* ref_name: name of physical cell in .lib
* Difference between instance and reference name
  
![image](https://github.com/user-attachments/assets/671dbf6e-1ff1-4833-be69-9782154b5d07)

# To find the reference name
* get_attribute [get_cells REGA_reg] ref_name
![image](https://github.com/user-attachments/assets/d7fd193c-8f09-478c-8e76-c1f217071d4c)

# To know the reference name of all cells
* foreach_in_collection my_cell [get_cells * -hier] {
  set my_cell_name [get_object_name $my_cell];
  set rname [get_attribute [get_cells $my_cell_name] ref_name]
  echo $my_cell_name $rname
  }
![image](https://github.com/user-attachments/assets/d4cb0fe4-c3ec-4e07-b013-d923f5fcf072)

#### Command to write ddc file
* write -f ddc -out lab8_circuit.ddc
![image](https://github.com/user-attachments/assets/9300eb36-1314-42d9-9134-b8e7ecf274ce)

#### Launch design vision
* csh
* design_vision
* read_ddc lab8_circuit.ddc
![image](https://github.com/user-attachments/assets/8fdb8769-c1d7-4149-b728-2719ec6b3fff)
![image](https://github.com/user-attachments/assets/cb1617ff-72d8-4bf5-99f4-64ffafdd717e)

* Implementation of the circuit in the above image is
![image](https://github.com/user-attachments/assets/bc95b127-90ad-49b8-8087-6c7017fce3cb)

#### To get information about nets
* get_nets *
* To know what nets are connected command is : all_connected N1
![image](https://github.com/user-attachments/assets/d4c0163d-4371-4f1f-af3d-bd66bb24fc54)

## Net can have only one driver in digital design

![image](https://github.com/user-attachments/assets/a8142c4a-8bf2-4646-91c1-b3718970c591)

* all_connected n5
![image](https://github.com/user-attachments/assets/9505283e-a73e-444b-a24c-62b897f15b8f)

* foreach_in_collection my_pin [all_connected n5] {
  set pin_name [get_object_name $my_pin];
  set dir [get_attribute [get_pins $pin_name] direction];
  echo $pin_name $dir;
  }

![image](https://github.com/user-attachments/assets/03c5bec2-8d59-421c-9178-8853f5d62dc1)

</details>

<details>
<summary>Lab 9: get_pins, get_clocks, querying_clocks </summary>
<br>

* get_pins *
* 
# To list all the pins

* foreach_in_collection my_pin [get_pins *] {
  set pin_name [get_object_name $my_pin];
  echo $pin_name;
  }

![image](https://github.com/user-attachments/assets/b27f6fe1-ec80-4495-bc70-9486ede53896)

## To check some attributes
* get_attribute [get_pins REGC_reg/RESET_B] direction
* get_attribute [get_pins REGC_reg/RESET_B] clock
* get_attribute [get_pins REGC_reg/CLK] clock

![image](https://github.com/user-attachments/assets/0f9f5376-f0ec-4a31-af2f-1eb5f7e72e88)

## To know what all pins are the clock pins in my design
*The attribute clock is defined on input pins
#### Script for finding the direction of pins
* foreach_in_collection my_pin [get_pins *] {
  set my_pin_name [get_object_name $my_pin];
  set dir [get_attribute [get_pins $my_pin_name] direction];
  echo $my_pin_name $dir;
  }
![image](https://github.com/user-attachments/assets/accf9c08-dd2b-40a8-84bf-c9ddab03efb0)

* foreach_in_collection my_pin [get_pins *] {
  set my_pin_name [get_object_name $my_pin];
  set dir [get_attribute [get_pins $my_pin_name] direction];
  if { [regexp $dir in] } {
  if { [get_attribute [get_pins $my_pin_name] clock] } {
  echo $my_pin_name;
  }
  }
  }
  ![image](https://github.com/user-attachments/assets/26fe4f4a-2d39-4739-ac17-31ae28e66301)
  
* Output: showing all the clock pins
![image](https://github.com/user-attachments/assets/8f9f5223-2ba6-4358-8253-e7b21f49c289)

# Difference between clock and clocks

![image](https://github.com/user-attachments/assets/71db9d97-010d-48e4-aa6d-1b8432ff97dc)

![image](https://github.com/user-attachments/assets/8140d80f-5123-4a93-a441-92da13a038ab)

* get_clocks * (it tells what are the clocks in design)

![image](https://github.com/user-attachments/assets/34378469-1aff-44b2-989d-d3a6fd4b2aaa)


</details>

<details>
<summary>Lab 10: create_clock waveform </summary>
<br>


</details>

<details>
<summary>Lab 11: Clock Network Modelling - Uncertainity, report_timing </summary>
<br>


</details>

<details>
<summary>Lab 12: IO Delays </summary>
<br>


</details>

<details>
<summary>Lab 13: generated_clocks </summary>
<br>


</details>

<details>
<summary>Lab 15: Part 1 Set_Max_delay </summary>
<br>


</details>

<details>
<summary>Lab 15: Part 2 VCLK </summary>
<br>


</details>



