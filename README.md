# Day 0: Summary of Digital VLSI SoC Design and Planning

## Step1: Chip Modelling

![Capture](https://github.com/user-attachments/assets/09f91696-937b-4bd8-9045-fafd02103e19)

+ Write the C code for an application and compile it using the gcc in Linux and measure the output O0 as given in the figure.
+ Model the entire specifications of the application in C environment, compile it and measure the output O1
+ Ensure that output O0 == O1.

## Step 2: RTL architect

![Capture](https://github.com/user-attachments/assets/67ed0c25-662e-45d9-908e-40c8590bfa1b)

+ Understand the specifications and represent the specifications in one of the hardware language like Verilog.
+ Take the same application, run on the hardware and measure O2.
+ Make sure that O2 == O1, so that functionality is retained.

## Step 3: SoC Design Flow

![image](https://github.com/user-attachments/assets/a9bc6248-f968-4043-a921-8ee7465092e7)

+ Divide the verilog code into multiple links like Processor as one part and Peripherals/IPs on another part
+ Processor Verilog code is synthesizable that is the code is converted into Gates

![image](https://github.com/user-attachments/assets/ec3647a8-9005-47a8-83b6-6ad7f39e5a3a)

+ Make sure that verilog code written for processor is synthesizable, so that it can be easily converted into Gates
+ Prepherals/IPs are divided into Macros and Analog IPs. 


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




