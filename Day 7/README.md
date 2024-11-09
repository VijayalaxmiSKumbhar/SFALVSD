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
* 
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

* As show here all the register to register paths are constrained
* Input and output paths are unconstrained
  
![image](https://github.com/user-attachments/assets/a812b4a6-df39-4b26-a09b-1c80268419d8)


* report_timing -from IN_A
Path is unconstained

![image](https://github.com/user-attachments/assets/4ccbae47-4b45-436f-8a0e-5017061e43ac)

* report_timing -to OUT_Y
Path is unconsrained
![image](https://github.com/user-attachments/assets/4b19fc9f-527b-4479-b8fc-69b91654656e)

* report_port -verbose: tell all the details like direction, transition, load etc

![image](https://github.com/user-attachments/assets/64f581db-cba8-4c75-89a3-fde10812a315)


## Modelling of Inputs
* set_input_delay -max 5 -clock [get_clocks MYCLK] [get_ports IN_A]
* set_input_delay -max 5 -clock [get_clocks MYCLK] [get_ports IN_B]
* report_port -verbose

![image](https://github.com/user-attachments/assets/7c2c24a1-cf02-48cf-b2e4-337c3bf0ddf1)

* report_timing -from IN_A
* Now path is constrained
![image](https://github.com/user-attachments/assets/3dfa9a26-5d62-4c6e-9cb7-46cd43e0c41d)

* report_timing -from IN_A -trans -net -cap -nosplit -delay_type min
* Path is unconstrained because min delay is not modelled
  
![image](https://github.com/user-attachments/assets/42761f62-d371-4662-b732-31d3877efd40)

#### Modelling of min delay

* report_timing -from IN_A -trans -net -cap -nosplit -delay_type min
* Now Path is constrained because min delay is modelled

![image](https://github.com/user-attachments/assets/2167155e-c3ba-4ee1-b966-7ca91de67121)

* report_timing -from IN_A -trans -net -cap -nosplit > a
* sh gvim a &
  
![image](https://github.com/user-attachments/assets/3d7e9d9e-33bd-4dce-9435-d35dde4309ed)

## Modelling Input Transistion

* set_input_transition -max 0.3 [get_ports IN_A]
* set_input_transition -max 0.3 [get_ports IN_B]
* set_input_transition -min 0.1 [get_ports IN_A]
* set_input_transition -min 0.1 [get_ports IN_B]

![image](https://github.com/user-attachments/assets/c60dd94e-548e-4852-ad46-a366e70429da)

![image](https://github.com/user-attachments/assets/434e910c-635c-409d-8823-f8e12eddac67)

## Model the output delay

* set_output_delay -max 5 -clock [get_clocks MYCLK] [get_ports OUT_Y]
* set_output_delay -min 1 -clock [get_clocks MYCLK] [get_ports OUT_Y]
* report_timing -to OUT_Y

  ![image](https://github.com/user-attachments/assets/498f3437-9668-4c12-a4f7-c520a461b4c1)

* report_timing -to OUT_Y -cap -trans -nosplit
  
## Modelling of load
* set_load -max 0.4 [get_ports OUT_Y]
* report_timing -to OUT_Y -cap -trans -nosplit
  
  ![image](https://github.com/user-attachments/assets/9cff154c-ebcb-46cc-be2c-a7e1fad1d0b7)
  
* report_timing -to OUT_Y -cap -trans -nosplit > out_load
* sh gvim out_load &
  
![image](https://github.com/user-attachments/assets/385ce8e0-5f08-4d64-bf9c-dab7ef536bdd)

</details>

<details>
<summary> SDC Part 3 generated_clocks </summary>
<br>

#### Example

![image](https://github.com/user-attachments/assets/af8b97ff-b05e-4e07-8628-028393175735)

#### The solution to above problem is generated clock
![image](https://github.com/user-attachments/assets/949b7d82-49d8-411e-9c68-b8d73215a3a2)

#### Constraining the design
![image](https://github.com/user-attachments/assets/b94f48e0-f6c6-4748-a867-8f34e3b1c3e4)




</details>

<details>
<summary>Lab 13: generated_clocks </summary>
<br>

## Example to understand what is generated_clock and why it is required?

![image](https://github.com/user-attachments/assets/12f1d0d8-c739-4a61-b363-85154fe0c60f)

* create_generated_clock -name MYGEN_CLK -master MYCLK -source [get_ports clk] -div 1 [get_ports out_clk]
* report_clocks *

![image](https://github.com/user-attachments/assets/d37a3782-a668-4e2e-9340-c3509ff1274f)

* get_attribute [get_clocks MYGEN_CLK] is _generated
* get_attribute [get_clocks MYCLK] is _generated

![image](https://github.com/user-attachments/assets/f34c3536-f3b0-4aa1-a1b2-ac659bf53924)

* report_port -verbose

![image](https://github.com/user-attachments/assets/66ecf027-3a32-413c-842f-6a4ead61ece8)

* report_timing -to OUT_Y

![image](https://github.com/user-attachments/assets/a8060ba1-40cc-4525-b57d-3fa18c19ca95)

#### Modelling of MYGEN_CLK
* set_clock_latency -max 1 [get_clocks MYGEN_CLK]
* set_output_delay -max 5 -clock [get_clocks MYGEN_CLK] [get_ports OUT_Y]
* set_output_delay -min 1 -clock [get_clocks MYGEN_CLK] [get_ports OUT_Y]
* report_timing -to OUT_Y

![image](https://github.com/user-attachments/assets/ae09371b-e5dc-4d75-a00f-4af825872ea2)

#### Example lab8_circuit_modified.

```
module lab8_circuit (input rst, input clk , input IN_A , input IN_B , output OUT_Y , output out_clk , output reg out_div_clk);
reg REGA , REGB , REGC ; 

always @ (posedge clk , posedge rst)
begin
	if(rst)
	begin
		REGA <= 1'b0;
		REGB <= 1'b0;
		REGC <= 1'b0;
		out_div_clk <= 1'b0;
	end
	else
	begin
		REGA <= IN_A | IN_B;
		REGB <= IN_A ^ IN_B;
		REGC <= !(REGA & REGB);
		out_div_clk <= ~out_div_clk; 
	end
end

assign OUT_Y = ~REGC;

assign out_clk = clk;

endmodule
```


* reset_design
* read_verilog /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/lab8_circuit_modified.v

![image](https://github.com/user-attachments/assets/52150569-2e31-4836-9301-aa1cd1118aa4)

* sh gvim lab8_cons.tcl

```
create_clock -name MYCLK -per 10 [get_ports clk];
set_clock_latency -source 2 [get_clocks MYCLK];
set_clock_latency 1 [get_clocks MYCLK];
set_clock_uncertainty -setup 0.5 [get_clocks MYCLK];
set_clock_uncertainty -hold 0.1 [get_clocks MYCLK];
set_input_delay -max 5 -clock [get_clocks MYCLK] [get_ports IN_A];
set_input_delay -max 5 -clock [get_clocks MYCLK] [get_ports IN_B];
set_input_delay -min 1 -clock [get_clocks MYCLK] [get_ports IN_A];
set_input_delay -min 1 -clock [get_clocks MYCLK] [get_ports IN_B];
set_input_transition -max 0.4 [get_ports IN_A];
set_input_transition -max 0.4 [get_ports IN_B];
set_input_transition -min 0.1 [get_ports IN_A];
set_input_transition -min 0.1 [get_ports IN_B];
create_generated_clock -name MYGEN_CLK -master MYCLK -source [get_ports clk] -div 1 [get_ports out_clk];
create_generated_clock -name MYGEN_DIV_CLK -master MYCLK -source [get_ports clk] -div 2 [get_ports out_div_clk]; 
set_output_delay -max 5 -clock [get_clocks MYGEN_CLK] [get_ports OUT_Y];
set_output_delay -min 1 -clock [get_clocks MYGEN_CLK] [get_ports OUT_Y];
set_load -max 0.4 [get_ports OUT_Y];
set_load -min 0.1 [get_ports OUT_Y];

```

* source /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/verilog_files/lab8_cons.tcl
* report_clocks

![image](https://github.com/user-attachments/assets/d2cabcbc-ce3c-4717-b7a3-7914157f2cbb)

* get_generated_clocks

![image](https://github.com/user-attachments/assets/17bb7ab3-52c2-432f-818c-87fd0e228ab5)

* report_port -verbose

![image](https://github.com/user-attachments/assets/5929c20d-a72e-4dcd-bad2-9fe8edd00dbe)



</details>

<details>
<summary> SDC Part 4 Vclk, max_latency, rise_fall, IO Delays </summary>
<br>

## Input Delay

![image](https://github.com/user-attachments/assets/5597049b-1c70-44d7-962f-d5fbf8436eca)

## Output Delay

![image](https://github.com/user-attachments/assets/d443896a-05a7-4e41-b2f8-f2aeb648d63e)

## set_max_latency is used to constrain the pure combinational forms

![image](https://github.com/user-attachments/assets/d5f75295-f902-44bc-a266-69b7ebaa7fb1)

## One more way of constraining the path is by using VIRTUAL CLOCK

![image](https://github.com/user-attachments/assets/e531f8e9-c9da-444d-87ad-ed507dce1897)

## IO Constraints

![image](https://github.com/user-attachments/assets/bcd42f22-d48a-4c5e-bb7d-986fc362f87a)

![image](https://github.com/user-attachments/assets/1538f878-0d70-4cdf-b522-3ede90ba424b)

## set_driving_cell: Recommended for module level IO

![image](https://github.com/user-attachments/assets/b664fcbb-61e0-43e3-b310-90cf3156fd60)

</details>

<details>
<summary>Lab 15: Part 1 Set_Max_delay </summary>
<br>


</details>

<details>
<summary>Lab 15: Part 2 VCLK </summary>
<br>


</details>


