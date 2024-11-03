# Welcome to the SFALVSD repository! This repository is designed to 
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


 








