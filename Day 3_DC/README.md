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

#### current_design tells name of top module

![image](https://github.com/user-attachments/assets/f015c834-03ac-4395-8f81-d85ed1897eeb)

![image](https://github.com/user-attachments/assets/afbc2f23-23c0-4bda-bec4-ecd90d6190df)

#### Command to create the clock is
* create_clock -name MYCLK -per 10 [get_ports clk]

![image](https://github.com/user-attachments/assets/25f043b7-0458-47e7-8474-a6211311e4c5)

* report_clocks * (lists all clocks in my design)
![image](https://github.com/user-attachments/assets/a9568c7a-ac8a-4e6d-bfb9-627f869f7ca9)

* get_attribute [get_pins REGA_reg/CLK] clocks
* get_attribute [get_ports out_clk] clocks

![image](https://github.com/user-attachments/assets/336a7eec-e2b7-4425-8fe3-7f8fc0a6f957)

![image](https://github.com/user-attachments/assets/1cf36f25-0a5c-4e94-b776-d6ad29363f04)

## Script
*sh gvim query_clock_pin.tcl &

![image](https://github.com/user-attachments/assets/bf465acb-f087-40a7-b585-793ed9986b99)

* source gvim query_clock_pin.tcl

![image](https://github.com/user-attachments/assets/60bc1c4e-653b-49a7-a440-b9e943abda11)

# Let us create BAD_CLK 

![image](https://github.com/user-attachments/assets/ad055e64-add7-4fc6-a3a1-211c806d843f)

# command to remove the wrong clock is
* remove_clock BAD_CLK

![image](https://github.com/user-attachments/assets/2f13ea0b-f178-443d-8f8f-91f08cb3b5e5)

# Creating Waveform

![image](https://github.com/user-attachments/assets/bcf1837c-f812-4865-bd21-a4962cd97300)

* create_clock -name MY_CLK -per 10 [get_ports clk] -wave {5 10}

![image](https://github.com/user-attachments/assets/3d5f252b-8812-407a-a954-23fdbdf72db2)

#### To create 25% duty cycle clock

* create_clock -name MY_CLK -per 10 [get_ports clk] -wave {0 2.5} (here if we change the order tool will create waveform)

![image](https://github.com/user-attachments/assets/a74e77ed-6427-4a66-aecc-cc685e00fccb)

* 10 ns Clock with first rising edge at 15 ns
  
![image](https://github.com/user-attachments/assets/294ca7b6-c4cc-45a7-a737-3b7fdd0e708e)




  
</details>

<details>
<summary>Lab 11: Clock Network Modelling - Uncertainity, report_timing </summary>
<br>

## Clock Network Modelling

#### Clock Network Attributes
* Source Latency
* Network Latency
* Clock Skew
* Clock Jitter

![image](https://github.com/user-attachments/assets/aab76170-2b02-424c-91ea-f8137ab7eaad)


# Modelling Source latency, network latency (without source), Uncertainity

* set_clock_latency -source 1 [get_clocks MY_CLK]
* set_clock_latency 1 [get_clocks MY_CLK]
* set_clock_uncertainty 0.5  [get_clocks MY_CLK] (for max delay)
* set_clock_uncertainty -hold 0.1  [get_clocks MY_CLK] (for min delay)

![image](https://github.com/user-attachments/assets/17e64a15-7d22-4b2b-9251-8c2688558dfc)

## How the above parameters affect the design?

#### command to check timing is

* report_timing
* It is saying path is uncontrained
![image](https://github.com/user-attachments/assets/dc73fdae-7e7b-484e-b300-bef483fd9e04)

* report_timing -to REGC_reg/D
  
![image](https://github.com/user-attachments/assets/798388f3-c92d-4dc9-b347-3430cd31bc59)

* create_clock -name MYCLK -per 10 [get_ports clk]
* report_timing -to REGC_reg/D

![image](https://github.com/user-attachments/assets/ac298fde-57f5-4ec8-bca2-67dceb3a0cff)

# Arrival & required time

![image](https://github.com/user-attachments/assets/a50843ae-c2f7-4c92-892f-68923e9e4ec9)

#### Clock behavior model
* set_clock_latency -source 2 [get_clocks MYCLK]
* set_clock_latency  2 [get_clocks MYCLK]
* set_clock_uncertainty -setup 0.5  [get_clocks MYCLK]
* set_clock_uncertainty -setup 0.1  [get_clocks MYCLK]
![image](https://github.com/user-attachments/assets/bb921422-d9c5-4f63-87e5-129168db168a)
* The above calculations are according to the equations given here
![image](https://github.com/user-attachments/assets/26dbb45d-34c0-450a-84b0-a1af53322bd3)

![image](https://github.com/user-attachments/assets/25d0ea5c-f9a8-4626-a228-5b26eab51d3d)

#### report_port -verbose

![image](https://github.com/user-attachments/assets/8bea7625-4115-448c-96b6-cebd83a11859)

![image](https://github.com/user-attachments/assets/1569d5d7-4ad1-40ca-aad8-57d3f5c48900)

#### report_timing -from IN_A

![image](https://github.com/user-attachments/assets/4ccbae47-4b45-436f-8a0e-5017061e43ac)

* reg-reg paths are constrained
* Input paths are not constrained, therefore IN_A path is unconstrained.


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



