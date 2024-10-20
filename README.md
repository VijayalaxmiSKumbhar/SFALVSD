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

https://private-user-images.githubusercontent.com/170864002/378218964-5d02e3c8-1915-4843-8b31-253f72423556.png?jwt=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJnaXRodWIuY29tIiwiYXVkIjoicmF3LmdpdGh1YnVzZXJjb250ZW50LmNvbSIsImtleSI6ImtleTUiLCJleHAiOjE3Mjk0NTE5NjcsIm5iZiI6MTcyOTQ1MTY2NywicGF0aCI6Ii8xNzA4NjQwMDIvMzc4MjE4OTY0LTVkMDJlM2M4LTE5MTUtNDg0My04YjMxLTI1M2Y3MjQyMzU1Ni5wbmc_WC1BbXotQWxnb3JpdGhtPUFXUzQtSE1BQy1TSEEyNTYmWC1BbXotQ3JlZGVudGlhbD1BS0lBVkNPRFlMU0E1M1BRSzRaQSUyRjIwMjQxMDIwJTJGdXMtZWFzdC0xJTJGczMlMkZhd3M0X3JlcXVlc3QmWC1BbXotRGF0ZT0yMDI0MTAyMFQxOTE0MjdaJlgtQW16LUV4cGlyZXM9MzAwJlgtQW16LVNpZ25hdHVyZT0wMWZkNGNiZTIxZWIwMWFjOTA3OGZmYjYzZmY3YTlhOGI1Njc3NzI0NDM2NDgzYmE4NzE3YjNlZWE5YTZlNTg1JlgtQW16LVNpZ25lZEhlYWRlcnM9aG9zdCJ9.lNTeyLzXPxpKv0lnPCaTpLDVa-i0f9IwMMcjL-HMavM


# Iverilog
## Steps to install iverilog


```
sudo apt-get update
sudo apt-get install iverilog
```

# gtkwave

## Steps to install gtkwave


```
sudo apt-get update
sudo apt install gtkwave

```


