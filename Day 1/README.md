# Introduction to Verilog RTL design and Synthesis

<details>
<summary>Introduction to open-source simulator iverilog</summary>
<br>
    
## What is Simulator?
•	Simulator is a tool for checking design
•	iverilog is the simulator
## What is Design?
Design is the actual Verilog code which has the intended functionality to meet with the required specifications.
## What is testbench?
Testbench is the setup to apply the stimulus(test_vectors) to the design to check its functionality.
## How Simulator Works?
+ Simulator looks for changes on the input signals
+ Upon change to the input signal output is evaluated
  + If no change to the input signal no change to output

# Structure of Test bench
![image](https://github.com/user-attachments/assets/2f569a76-30e5-4877-973d-08c21420b8e2)

 ## Note:
+ Design may have one or more primary inputs, one or more primary outputs.
+ Testbench does not have Primary input or primary outputs.
  
# Iverilog based simulation flow

 ![image](https://github.com/user-attachments/assets/27709a8f-e3c5-4143-a09a-3c2bc9b32673)

</details>


# Labs using iverilog and gtkwave

#### Lab 1: Introduction

<details>
<summary>Tools Setup</summary>
<br>
    
+ git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
+ my_lib contains all the library files which are needed.
+ lib contains sky130 standard cell library used for synthesis
+ verilog_files contains the Verilog source files and test bench files. For each iverilog file there is respective testbench. 

![image](https://github.com/user-attachments/assets/e45be6c9-2d73-46b8-8336-1672bb8fd392)
![image](https://github.com/user-attachments/assets/f21382fc-a1b7-4ae6-826e-49222dd80c3a)
![image](https://github.com/user-attachments/assets/306fc5d3-8a91-42a8-8203-7de857132bd7)

</details>


#### Lab 2: Introduction to iverilog gtkwave part1

<details>
<summary>iverilog</summary>
<br>
    
+ Step 1: go to Verilog_files

+ Step 2: Load the design using the command iverilog good_mux.v tb_good_mux.v
![image](https://github.com/user-attachments/assets/960353a2-4f02-46f3-9743-baf389e9f150)

+ A file called a.out is created
![image](https://github.com/user-attachments/assets/3d25deef-cd6e-47a9-920e-93b91eb8dfbe)

 
Step 3: Execute using ./a.out, it will dump the vcd file
![image](https://github.com/user-attachments/assets/3844b902-36e7-49d4-a109-d9a76fc2f8ad)

 
Step 4: load vcd file in simulator gtkwave tb_good_mux.vcd
![image](https://github.com/user-attachments/assets/065b4cd5-e06f-4be6-b7f7-db270dab6e3a)

 
Click on tb good mux, inputs and outputs signal will appear drag and drop them and click on Zoom fit.
![image](https://github.com/user-attachments/assets/0152fba5-f30a-4f38-b9e8-2c6f41be64fb)

 
To see the transitions of particular input
![image](https://github.com/user-attachments/assets/9e38417f-8401-47af-9856-35975db1110c)

 </details>

#### Lab 2: Introduction to iverilog gtkwave part2

<details>
<summary>file structure</summary>
<br>
    
+ Let us look into the file structure
![image](https://github.com/user-attachments/assets/7ebdbed0-8a04-4559-a316-6106f9c7219a)

![image](https://github.com/user-attachments/assets/f70afea0-2f11-4060-9a2f-b27b147d81a3)

</details>

<details>
<summary>Introduction to Yosys and Logic Synthesis</summary>
<br>

## What is Synthesizer?
+ It is tool used for converting RTL into netlist
+ Yosys is the synthesizer
+ Yosys Setup
![image](https://github.com/user-attachments/assets/23aee282-28ca-4a9c-a525-c308a8d635b8)

 
+ Netlist file is the representation of the design in the form of standard cells present in .lib
## How to verify synthesis?
 ![image](https://github.com/user-attachments/assets/6a144544-ed09-4135-ac51-f43168cd4f5d)


## Note: 
The set of primary inputs/outputs remains same between RTL design and synthesized netlist
Same test bench can be used

</details>

<details>
<summary>Introduction to Logic Synthesis Part1</summary>  
<br>

## What is RTL design?
It is the behavioral representation of the required specification
## What happens in Synthesis?
![image](https://github.com/user-attachments/assets/ef3971f2-15f2-4fc6-b67c-123a2f052655)

## What is .lib?
+ Collection of logical modules
+ Includes basic logic gates like AND, OR, NOT, ….. etc
+ Different flavors of same gate
  2 input AND Gate
              -Slow
              -Medium
              -Fast
  3 input AND Gate
              -Slow
              -Medium
              -Fast

  4 input AND Gate
 …………
 …………
## Why different flavors of gate?

![image](https://github.com/user-attachments/assets/9c71cd91-988e-48f0-b33e-dad715dc77a6)

</details>

<details>
<summary>Introduction to Logic Synthesis Part2</summary>
<br>
    
## Why do we need Slow cells?

![image](https://github.com/user-attachments/assets/3fd7187e-6492-47ee-af6e-e272937baddd)

 
## Faster Cells Vs Slower Cells

![image](https://github.com/user-attachments/assets/4f5f40b5-c88b-4282-b28c-59c0c861fe3f)

## Selection of Cells 

![image](https://github.com/user-attachments/assets/ad834dc4-2776-4b0b-b3b3-e665fecf5de9)

 
## Synthesis Illustration

![image](https://github.com/user-attachments/assets/10febcab-302b-4a18-8fa4-419b80738bab)

 </details>
 
# Labs using Yosys and Sky130 PDKs

#### Lab 3: Yosys 1 good mux part1 

<details>
<summary>yosys good mux</summary>
<br>
    
+ ## Step 1: Invoke yosys
  
 ![image](https://github.com/user-attachments/assets/d6f3d17b-d8d5-4add-b114-9acf0b848704)

+ ## Step 2: Command to read library is
  
> ## read_liberty -lib /home/comp/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

![image](https://github.com/user-attachments/assets/a1a96698-b8ed-4412-ad97-fff77933e889)

+ ## Step 3: Command to read design is
  
> ## read_verilog good_mux.v

![image](https://github.com/user-attachments/assets/c0687f96-15d8-443b-bb8f-e705014f290a)

+ ## Step 4: Mention the module name which you want to synthesize
  
> ## synth -top good_mux

![image](https://github.com/user-attachments/assets/9094144f-2d32-4eb9-9b24-96c3e9be9cc9)

+ Step 5: Generate the netlist
  
> ## abc  -liberty  /home/comp/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

### abc is the command that will convert RTL into gates and what gates it has to link to is specified in the library.
### The logic of good_mux is realized using standard cells available in library sky130_fd_sc_hd__tt_025C_1v80.

![image](https://github.com/user-attachments/assets/cc266e73-3017-4bab-93db-1404230c7eaf)


![image](https://github.com/user-attachments/assets/5e28937b-03ac-4fe6-b703-378838d11d89)



+ ## Step 6: The command to see what logic it has realized is
> ## show

![image](https://github.com/user-attachments/assets/cffe304a-b4ec-408e-ab9b-a63d9454f8e3)


+ ## Step 7: How to write netlist
> ## write_verlig good_mux_netlist.v

![image](https://github.com/user-attachments/assets/6301c3ec-c996-420a-a96a-d6e426033e66)

> ## !gvim good_mux_netlist.v

![image](https://github.com/user-attachments/assets/29ae03fa-49c7-4e68-a139-34ee3c32b7be)

> ## To see a simplified netlist modify the command as
> ## write_verilog -noattr good_mux_netlist.v
> ## gvim good_mux_netlist.v

![image](https://github.com/user-attachments/assets/1cc12e5e-4a79-4d20-a710-ff7801539aca)

![image](https://github.com/user-attachments/assets/bd4eebca-ea02-43af-8005-04bf2dc21818)

</details>










