# Advanced Synthesis and STA with DC

<details>
<summary>Introduction to Course</summary>
<br>
  
## Agenda

![image](https://github.com/user-attachments/assets/465e7ccd-0e4f-49a3-8499-9ac8be780f3b)

## Tools Used

![image](https://github.com/user-attachments/assets/c39fbdc8-eb36-461b-afae-dcfc6a5b533b)

## Prerequisites required

![image](https://github.com/user-attachments/assets/4c74f209-d0e4-4c10-b9fb-1f3ef7c845ec)

## Outcomes of the course

![image](https://github.com/user-attachments/assets/c4630ed1-c4f6-452c-8f39-a79e89545f7a)

</details>

<details>
<summary>Basics of Digital Logic Design and Synthesis</summary>
<br>

![image](https://github.com/user-attachments/assets/6739f061-1dc8-4d20-b09d-ed649f272e4c)

## The specifications are written in Hardware Description Language

![image](https://github.com/user-attachments/assets/c7514fe8-8341-488d-8690-ca332dce3413)

### Every design starts with target specification. This decides the architecture of the chip.

### This specification represented in programming language is the RTL (Register Transfer Logic)

### Example of RTL. It is nothing but a code

![image](https://github.com/user-attachments/assets/3ab0f50f-b4dc-4b00-b811-17e1be156847)

# What is Synthesis?

![image](https://github.com/user-attachments/assets/9133ceaa-a321-438d-8404-a0b80b180d65)

# What is .lib?

![image](https://github.com/user-attachments/assets/a4722537-28b5-409b-9b93-52caa6356201)

# Why different flavours of gate?

![image](https://github.com/user-attachments/assets/d7d91bd4-58b8-486f-9cbc-a04ae6c4a959)

# Why we need Slow cells?

![image](https://github.com/user-attachments/assets/1318fc94-8234-4f5c-8267-17c5f00d8955)

# Faster Cells Vs Slower Cells

![image](https://github.com/user-attachments/assets/0a6cb594-b2e7-4437-b30d-43edfd3eb2cc)

# Selection of Cells

![image](https://github.com/user-attachments/assets/9d6247f9-bd64-4ac0-8394-4447f142ffa0)

# Synthesis

![image](https://github.com/user-attachments/assets/42b0489c-65d5-42c6-bfea-539d6ddb3ea0)

</details>

<details>
<summary>Logic Synthesis Basics</summary>

## Example

![image](https://github.com/user-attachments/assets/21b0683c-e15b-4de5-9d34-ae4e983b1c37)

## Let us find which is the correct implementation with the following standard cell details

![image](https://github.com/user-attachments/assets/b38c534b-7db0-45c3-a519-5f45ec8abac1)

## Comparison of Implementations

![image](https://github.com/user-attachments/assets/eff8e5f2-f0f7-4df1-8b45-b6a779cddd1e)

# Goals of Logic Synthesis

![image](https://github.com/user-attachments/assets/c3ad1d35-9ca8-4fe0-b92f-2d9d22deaf33)

![image](https://github.com/user-attachments/assets/be39e294-bdab-4897-8164-9e032cae0d42)

</details>

<details>
<summary>Introduction to Design Compiler (DC)</summary>
<br>

## What is DC?

![image](https://github.com/user-attachments/assets/e92a467a-219b-46cb-8373-928c9be94d6a)

## Common Terminologies associated with DC

![image](https://github.com/user-attachments/assets/09f82b5c-7095-4f9b-9807-af1876a47fc6)

## Synopsys Design Constraints (SDC)

![image](https://github.com/user-attachments/assets/0b50a80d-5dc5-4788-8a8e-48fd4bd6990b)

# DC Setup

![image](https://github.com/user-attachments/assets/6e16877b-3593-430c-acb3-5fa1075753b6)

# Implementation flow of ASIC ----> Steps in converting RTL to the Physical database(GDS)

![image](https://github.com/user-attachments/assets/d757a911-6e08-4b7c-bdcc-76d507e668f2)

# DC Synthesis Flow

![image](https://github.com/user-attachments/assets/e68dc3ba-3c2b-4fce-9f80-14a307d63495)

</details>

<details>
<summary>Lab 1: Invoking DC Basic Setup</summary>
<br>

## Understanding sky130_fd_sc_hd__tt_025c_1v80.lib
![image](https://github.com/user-attachments/assets/e900066f-0dac-4371-90ad-7f820b422a13)

## Invoke DC using the commands

* csh
* dc_shell

![image](https://github.com/user-attachments/assets/61c0ae0f-ff85-419a-accf-af0c8afa4e07)

![image](https://github.com/user-attachments/assets/8f44d2dd-5e77-4708-8a80-3aeeb07bd659)

![image](https://github.com/user-attachments/assets/df5924af-1e57-4e8d-8339-5ac1ef458f01)

## Example

```
module lab1_flop_with_en ( input res , input clk , input d , input en , output reg q);
always @ (posedge clk , posedge res)
begin
	if(res)
		q <= 1'b0;
	else if(en)
		q <= d;	
end
endmodule

![image](https://github.com/user-attachments/assets/53a0aea5-5ec6-4129-8bda-e7e073fdf8a5)


```
read_verilog
![image](https://github.com/user-attachments/assets/11473abd-6c3e-4dfa-b3db-5b5a99026130)

write_verilog: write -f verilog -out lab1_net.v

![image](https://github.com/user-attachments/assets/a4d0db8f-a370-482b-840e-c3fafce2c2e0)

gtech library: Virtual library in DC to understand the design

![image](https://github.com/user-attachments/assets/be1f077a-d9d0-46a5-8a64-d1c10ce0ed3e)

read the library as: read_db sky130RTLDesignAndSynthesisWorkshop/DC_Workshop/lib/sky130_fd_sc_hd__tt_025c_1v80.db

![image](https://github.com/user-attachments/assets/6317961b-0820-46e7-8827-8b2b1845d5bb)

set target_library /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db

set link_library {* /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db} (here * signifies libraries in DC memory)

Syntax to link library 

![image](https://github.com/user-attachments/assets/81f2005c-1cbf-4943-bff8-43adf9c9a411)

link

![image](https://github.com/user-attachments/assets/7261fce0-050d-4b4b-863a-5eabc838a743)

compile

![image](https://github.com/user-attachments/assets/5fe5c24e-d4a1-49cd-bdf4-4f41612b4852)

write -f verilog -out lab1_net_with_sky130.v
![image](https://github.com/user-attachments/assets/edb1cdc6-b97d-44a6-87ab-e5527a98ed42)


</details>


<details>
<summary>Lab 2: ddc gui with design_vision</summary>
<br>

## To launch design_vision type

* csh
* design_vision
![image](https://github.com/user-attachments/assets/c689ac9f-04e3-4ec8-9abd-642ce3497dd4)

write -f ddc -out lab1.ddc (write is the syntax to tell the tool to write the information in ddc format)
![image](https://github.com/user-attachments/assets/8601b3d2-af84-4167-9355-6c5837a8b10e)

command to start gui is 
* start_gui
* read_ddc lab1.ddc
![image](https://github.com/user-attachments/assets/a9bdc1ef-49d0-4fb7-b9b8-2ef703a3a4bb)

## Difference between read_verilog and read_ddc

![image](https://github.com/user-attachments/assets/e17a0d77-8cee-4779-8ce7-38c53f2d5e01)

## Schematic View

![image](https://github.com/user-attachments/assets/a61937a9-a29c-4356-9124-3616f5c985cf)

## Got the same design as per expectation

![image](https://github.com/user-attachments/assets/8bbbb024-5a84-491f-9fc8-a7d84489df51)

</details>

<details>
<summary>Lab 3: dc synopsys dc setup</summary>
<br>

* csh
* dc_shell
* echo $target_library
* echo $link_library
* Every time while loading the dc perform the command
  -- set target_library /home/vijayalaxmi/sky130RTLDesignAndSynthesisWorkshop/DC_WORKSHOP/lib/sky130_fd_sc_hd__tt_025C_1v80.db
  -- set link_library {* $target_library}
* Instead of performing repetitative tasks, the solution is to invoke synopsys dc setup
![image](https://github.com/user-attachments/assets/f6b07c50-cbec-4a86-b071-2587dad73802)

gvim .synopsys_dc.setup
![image](https://github.com/user-attachments/assets/245b4b24-f152-49e0-bffb-b30dc8e58998)



</details>

<details>
<summary>TCL Quick Refresher</summary>
<br>

## Set
#### For set $ is not used.
  
![image](https://github.com/user-attachments/assets/aeea0bc9-3618-4422-94a7-9e4630a91faa)

## Conditional Statements
#### Note: Strictly follow the syntax to avoid errors
##### if statement
  
![image](https://github.com/user-attachments/assets/41f23848-58cd-4511-8b1a-d69c5c98fcec)

##### while statement
![image](https://github.com/user-attachments/assets/e9986d69-ba64-476d-a4bd-a174c4b7d836)

##### for loop
![image](https://github.com/user-attachments/assets/4fdf1c9a-e2b0-44bb-b88d-fc55369b44e6)

##### foreach: General TCL statement/command
![image](https://github.com/user-attachments/assets/6a4840c8-a710-41b0-8866-dd93a90f1385)

##### DC specific command
![image](https://github.com/user-attachments/assets/318fb6c8-32ee-408c-b83b-64a1f3d0b33d)

</details>


<details>
<summary>Lab 4: tcl scripting</summary>
<br>

## 

</details>










