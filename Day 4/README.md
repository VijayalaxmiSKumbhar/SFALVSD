# Day 4: GLS, blocking vs non-blocking and Synthesis-Simulation mismatch

## Introduction Gate Level Simulation (GLS), Synthesis-Simulation mismatches

### What is GLS and Why GLS?

![image](https://github.com/user-attachments/assets/43b84a9f-3c12-4d05-8366-ea6307aff677)

### GLS using iverilog

![image](https://github.com/user-attachments/assets/d60ec4fa-c240-4763-b9b1-f1093bb89d6e)

### GLS with example

![image](https://github.com/user-attachments/assets/c754cb26-0347-4c77-ad55-275797d9a434)

## Synthesis-Simulation mismatch

![image](https://github.com/user-attachments/assets/73867b06-17aa-43a3-aad9-125f3b3e259a)

### Missing Sensitivit List

![image](https://github.com/user-attachments/assets/46693612-003b-4aef-aea5-3173337d5a70)

# Blocking and Non-blocking Statements in verilog

![image](https://github.com/user-attachments/assets/12f24d1a-69cf-4309-9afd-dffb5e7bd179)

### Example 1: Caveats with Blocking Statements

![image](https://github.com/user-attachments/assets/3140adf7-5f9b-4f2d-82ba-44bc72e0dbf6)

### Written with Non-Blocking statements: Use these statements to write sequential circuits

![image](https://github.com/user-attachments/assets/27a8db0b-133d-4975-9dbb-878a12b797e0)

### Example 2: Caveats with Blocking Statements

![image](https://github.com/user-attachments/assets/e9f16714-a83e-4ba0-920b-47bce3ee7a78)


#  Labs on GLS and Synthesis-Simulation Mismatch

### Examples to understand GLS

![image](https://github.com/user-attachments/assets/ad2191fc-a72f-4d31-96cb-05dc6aa41f27)

### Ternary operator (?)

![image](https://github.com/user-attachments/assets/0b5971f2-2995-4ae8-8395-46c4bb866ed4)

# RTL Simulation

![image](https://github.com/user-attachments/assets/18dc8b8c-b05f-4e92-a073-1a6ef07b4749)

### Output

![image](https://github.com/user-attachments/assets/1a4f9543-5979-49e2-907a-defabf22db1f)

### Synthesis

![image](https://github.com/user-attachments/assets/e4ccc2de-0334-4ec5-bee0-23a5ece20487)

![image](https://github.com/user-attachments/assets/1b113711-a087-40fe-b0ba-80a71abbe4de)


![image](https://github.com/user-attachments/assets/a120c12d-d0cb-45d3-b54d-ca50ca2d36df)

### GLS Output: It has _6_, _7_, _8_ which was not there in RTL, it clearly indicates GLS.

![image](https://github.com/user-attachments/assets/8601072b-7581-4afe-ad44-89f15226c3b6)

## Example bad_mux.v

### RTL Simulation

![image](https://github.com/user-attachments/assets/75e106bc-295d-4d7b-9dff-00e0abfdb61d)

### The waveform clearly indicates that it is not functioning as mux. It is lookin as if as flop.

![image](https://github.com/user-attachments/assets/09743a29-f8cb-4efd-86fd-057ac71affac)

## Synthesis

![image](https://github.com/user-attachments/assets/31ea3a33-21c1-45c7-a9af-e23a4ef6d474)

![image](https://github.com/user-attachments/assets/789c34d5-5a07-41f3-b3ac-1fca387d9e49)

# GLS Output bad_mux.v

![image](https://github.com/user-attachments/assets/df78f3c2-e938-49cb-8b48-417a0470d6e9)

![image](https://github.com/user-attachments/assets/04e36312-f114-4f80-b793-ab2f201e3fb4)

# Synthesis-Simulation mismatch due to missing sensitivity list

![image](https://github.com/user-attachments/assets/8e360189-be33-4526-9e79-5b7cea54e0bd)

# Labs on synth-sim mismatch for blocking statement

### Example: blocking_caveat.v

```
module blocking_caveat (input a , input b , input  c, output reg d);
reg x;
always @ (*)
begin
	d = x & c;
	x = a | b;
end
endmodule

```

![image](https://github.com/user-attachments/assets/b2ba6b7f-5621-411f-af85-758d6ab29cfc)








