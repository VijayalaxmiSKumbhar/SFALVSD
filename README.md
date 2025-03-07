# Welcome to the SFAL-VSD SoC Design Program Repository 

#### This repository documents a semiconductor design basics, including floorplanning, placement, clock tree synthesis (CTS), routing, optimization, and verification organized by VSD.

### Project: 
##### VSDBabySoC: ICC2 Implementation & PVT-Aware Timing Optimization

##### The primary objectives of the project include the implementation of advanced design methodologies and the optimization of timing performance by considering PVT (Process, Voltage, Temperature) variations.

##### Key components of the project include:

* `ICC2 Implementation`: Leveraging the capabilities of IC Compiler II to create a robust SoC design that incorporates automated design processes for efficiency and reliability.

* `PVT-Aware Timing Optimization`: Implementing techniques that account for variations in process, voltage, and temperature to ensure accurate timing analysis and adjustments. This approach aims to enhance chip performance and stability under varying conditions.

* `Performance Enhancements`: Aiming for improved power efficiency and timing closure, ensuring that the integrated circuits can operate reliably across different conditions while meeting specified performance metrics.



# Summary of Digital VLSI SoC Design and Planning

<details>
<summary> Chip Modelling </summary>
<br>
 
![Capture](https://github.com/user-attachments/assets/09f91696-937b-4bd8-9045-fafd02103e19)

+ Write the C code for an application and compile it using the gcc in Linux and measure the output O0 as given in the figure.
+ Model the entire specifications of the application in C environment, compile it and measure the output O1
+ Ensure that output O0 == O1.

</details>

<details>
<summary> RTL architect </summary>
<br>

![Capture](https://github.com/user-attachments/assets/67ed0c25-662e-45d9-908e-40c8590bfa1b)

+ Understand the specifications and represent the specifications in one of the hardware language like Verilog.
+ Take the same application, run on the hardware and measure O2.
+ Make sure that O2 == O1, so that functionality is retained.

</details>

<details>
<summary> SoC Design Flow </summary>
<br>

![image](https://github.com/user-attachments/assets/a9bc6248-f968-4043-a921-8ee7465092e7)

+ Divide the verilog code into multiple links like Processor as one part and Peripherals/IPs on another part
+ Processor Verilog code is synthesizable that is the code is converted into Gates

![image](https://github.com/user-attachments/assets/ec3647a8-9005-47a8-83b6-6ad7f39e5a3a)

+ Make sure that verilog code written for processor is synthesizable, so that it can be easily converted into Gates
+ Prepherals/IPs are divided into Macros and Analog IPs. The more popular analog IP is 10-bit ADC.
+ Processor and Macros are synthesizable, whereas analog IPs need not be synthesizable.

</details>


<details>
<summary>SoC Integration</summary>
<br>

![image](https://github.com/user-attachments/assets/6167041f-2659-419b-99ec-b7677c223eff)

</details>


<details>
<summary>RTL2GDS</summary> 
<br>
 
+ RTL2GDS refers to the process of converting a Register Transfer Level (RTL) design, typically described in a Hardware Description Language (HDL) such as VHDL or Verilog, into a GDSII file, which represents the geometric layout of the integrated circuit for fabrication.

</details>

<details>
 
<summary>GDSII (Graphical Data Stream Information Interchange)</summary>
<br>

+ It is a file which contains only metal layers. Information about the fabrication of chip.
+ GDSII will go for DRC/LVS checks, to retain the connectivity.
+ GDSII file is then sent to factory. This process of sending GDSII to the factory is knowns as tapeout. Receiving the chips back from factory is called tapein.

</details>

<details>
<summary>Prepare a Board</summary>
<br>

![image](https://github.com/user-attachments/assets/a09eeac5-feee-4e0f-b715-ca52fb76da4d)

</details>

# Repo Organization

<div style="overflow-x: auto; white-space: nowrap;">
  <pre>
1. Daily Progress Overview: Each folder includes a comprehensive overview of daily activities, including learning summaries, tool installations, relevant code and design files.
2. Tools: Detailed, step-by-step documentation of the necessary tools for the program, along with installation instructions and screenshots.
  </pre>
</div>

# Aim and Objectives

```
* Understand the basics of System on Chip (SoC) design.
* Acquire practical experience using industry-standard tools and processes.
* Documentation of daily tasks.
* Present projects and the results of learning.

```

# Learning Goals


### Task Repository

| Day  | Description  |Folder  |
| ------------ | ------------ | ------------ |
|[Day 0](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day%200 "Day 0") | Tools Installation  |Day 0|
|[Day 1](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day%201 "Day 1") | Introduction to Verilog RTL design and Synthesis  |Day 1 |
|[Day 2](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day%202%20 "Day 2") | Timing libs, hierarchical vs flat synthesis and efficient flop coding styles   |Day 2 |
| [Day 3](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day%203 "Day 3")| Combinational and Sequential Optimizations   |Day 3 |
| [Day 4](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day%204 "Day 4")| GLS, blocking vs non-blocking and Synthesis-Simulation mismatch   |Day 4 |
|[Day 5](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day%205 "Day 5") | Advanced Synthesis and STA with DC  |Day 5 |
|[Day 6](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day%206 "Day 6") | Basics of STA (Static Timing Analysis)  |Day 6 |
| [Day 7](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day%207 "Day 7")| Advanced Constraints  |Day 7 |
| [Day 8](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day%208 "Day 8")| Optimizations   |Day 8 |
|[Day 9](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day%209 "Day 9") | Generating Timing Reports and Analyzing QoR   |Day 9 |
| [Day 10](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day10 "Day 10")| Introduction to VSDBabySoC and Fundamentals of SoC   |Day 10 |
| [Day 11](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day11 "Day 11")| VSDBabySoC Modeling   |Day 11 |
|[Day 12](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day12 "Day 12") | Post-Synthesis Simulation    |Day 12 |
|[Day 13](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day13 "Day 13") | PVT (Process Voltage Temperature) Analysis   |Day 13 |
| [Day 14](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day14 "Day 14")| Inception of open-source EDA, OpenLANE and Sky130 PDK  |Day 14 |
| [Day 15](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day15 "Day 15")| Good floorplan Vs bad floorplan and introduction to library cells  |Day 15 |
|[Day 16](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day16 "Day 16") | ICC2 ( IC Compiler II)  |Day 16 |
|[Day17](http://https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day17 "Day17")   |  RVMYTH CORE |Day 17 |
|  [Day18](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day18 "Day18") |  VSDBabySoC ICC2 flow |Day 18|
|[Day19](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day19 "Day19")|STA using Prime Time (PT) Tool|Day 19|
|  [Day20](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day20 "Day20") |  ECO using Prime Time | Day 20  |
| [Day21](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day21 "Day21")  | STA Analysis & ECO Second Iteration  | Day 21  |
| [Day22](https://github.com/VijayalaxmiSKumbhar/SFALVSD/tree/main/Day22 "Day22") | STA Analysis & ECO Third Iteration  | Day 22  |



![Vijayalaxmi_SFAL_VSD ceritificate_page-0001](https://github.com/user-attachments/assets/b25114f0-def4-4950-8425-3e0475c9f6d8)




##### Acknowledgements

* Kunal Ghosh, Co-founder VSD Coporation Private Limited.

* Nickson P Jose, Physical Design Engineer, Intel Corporation.

* R. Timothy Edwards, Senior Vice President of Analog and Design, efabless Corporation.



 
















