# Day 1: Tools Installation

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



# Iverilog
## Steps to install iverilog


```
sudo apt-get update
sudo apt-get install iverilog
```

![iverilog](https://github.com/user-attachments/assets/512b794e-c63a-423a-8caa-252b191db63e)

# gtkwave

## Steps to install gtkwave


```
sudo apt-get update
sudo apt install gtkwave

```


