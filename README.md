# Day 0: Summary of Digital VLSI SoC Design and Planning

## Chip Modelling

![Capture](https://github.com/user-attachments/assets/09f91696-937b-4bd8-9045-fafd02103e19)

+ Write the C code for an application and compile it using the gcc in Linux and measure the output O0 as given in the figure.
+ Model the entire specifications of the application in C environment, compile it and measure the output O1
+ Ensure that output O0 == O1.

## RTL architect

![Capture](https://github.com/user-attachments/assets/67ed0c25-662e-45d9-908e-40c8590bfa1b)

+ Understand the specifications and represent the specifications in one of the hardware language like Verilog.
+ Take the same application, run on the hardware and measure O2.
+ Make sure that O2 == O1, so that functionality is retained.

## SoC Design Flow

![image](https://github.com/user-attachments/assets/a9bc6248-f968-4043-a921-8ee7465092e7)

+ Divide the verilog code into multiple links like Processor as one part and Peripherals/IPs on another part
+ Processor Verilog code is synthesizable that is the code is converted into Gates

![image](https://github.com/user-attachments/assets/ec3647a8-9005-47a8-83b6-6ad7f39e5a3a)

+ Make sure that verilog code written for processor is synthesizable, so that it can be easily converted into Gates
+ Prepherals/IPs are divided into Macros and Analog IPs. The more popular analog IP is 10-bit ADC.
+ Processor and Macros are synthesizable, whereas analog IPs need not be synthesizable.

## SoC Integration

![image](https://github.com/user-attachments/assets/6167041f-2659-419b-99ec-b7677c223eff)

## RTL2GDS
+ RTL2GDS refers to the process of converting a Register Transfer Level (RTL) design, typically described in a Hardware Description Language (HDL) such as VHDL or Verilog, into a GDSII file, which represents the geometric layout of the integrated circuit for fabrication.

## GDSII (Graphical Data Stream Information Interchange)

+ It is a file which contains only metal layers. Information about the fabrication of chip.
+ GDSII will go for DRC/LVS checks, to retain the connectivity.
+ GDSII file is then sent to factory. This process of sending GDSII to the factory is knowns as tapeout. Receiving the chips back from factory is called tapein.

## Prepare a Board

![image](https://github.com/user-attachments/assets/a09eeac5-feee-4e0f-b715-ca52fb76da4d)

# Conclusion
Digital VLSI SoC design and planning encompasses the design, integration, and implementation of complex electronic systems within a single chip. 
 

# Day 1: Tools Installation


***
## Yosys
```
$ sudo apt-get update
$ git clone https://github.com/YosysHQ/yosys.git
$ cd yosys
$ sudo apt install make (If make is not installed please install it) 
$ sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
$ make config-gcc
$ make 
$ sudo make install
```

![yosys](https://github.com/user-attachments/assets/5d02e3c8-1915-4843-8b31-253f72423556)  

---

# Iverilog
## Steps to install iverilog


```
sudo apt-get update
sudo apt-get install iverilog
```

![iverilog](https://github.com/user-attachments/assets/512b794e-c63a-423a-8caa-252b191db63e)


---

# gtkwave

## Steps to install gtkwave


```
sudo apt-get update
sudo apt install gtkwave

```

![gtkwave](https://github.com/user-attachments/assets/a3b185f9-e798-4742-a72c-387be8f40abb)


# Day 1: Introduction to Verilog RTL design and Synthesis

+ Introduction to open-source simulator iverilog
++ Introduction to iverilog design test bench
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


# Labs using iverilog and gtkwave

## Lab 1: Introduction to lab
# Tools Setup 
+ git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git
+ my_lib contains all the library files which are needed.
+ lib contains sky130 standard cell library used for synthesis
+ verilog_files contains the Verilog source files and test bench files. For each iverilog file there is respective testbench. 

![image](https://github.com/user-attachments/assets/e45be6c9-2d73-46b8-8336-1672bb8fd392)
![image](https://github.com/user-attachments/assets/f21382fc-a1b7-4ae6-826e-49222dd80c3a)
![image](https://github.com/user-attachments/assets/306fc5d3-8a91-42a8-8203-7de857132bd7)


# Lab 2: Introduction to iverilog gtkwave part1
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

 

# Lab 2: Introduction to iverilog gtkwave part2
+ Let us look into the file structure
![image](https://github.com/user-attachments/assets/7ebdbed0-8a04-4559-a316-6106f9c7219a)

![image](https://github.com/user-attachments/assets/f70afea0-2f11-4060-9a2f-b27b147d81a3)


# Introduction to Yosys and Logic Synthesis
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

# Introduction to Logic Synthesis Part1
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


# Introduction to Logic Synthesis Part2
## Why do we need Slow cells?
![image](https://github.com/user-attachments/assets/3fd7187e-6492-47ee-af6e-e272937baddd)

 
## Faster Cells Vs Slower Cells
![image](https://github.com/user-attachments/assets/4f5f40b5-c88b-4282-b28c-59c0c861fe3f)

## Selection of Cells 
![image](https://github.com/user-attachments/assets/ad834dc4-2776-4b0b-b3b3-e665fecf5de9)

 
## Synthesis Illustration
![image](https://github.com/user-attachments/assets/10febcab-302b-4a18-8fa4-419b80738bab)

 
# Labs using Yosys and Sky130 PDKs
## Lab 3: Yosys 1 good mux part1 
+ Step 1: Invoke yosys
 ![image](https://github.com/user-attachments/assets/d6f3d17b-d8d5-4add-b114-9acf0b848704)

+ Step 2: Command to read library is 
> read_liberty -lib  .. /my_lib/lib/sky130_fd_sc__hd_tt_025c_1v80.lib
## Lab 3: Yosys 1 good mux part2 
## Lab 3: Yosys 1 good mux part2 







