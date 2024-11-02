# Day 3: Combinational and Sequential Optimizations

## Introduction to optimizations

### Combinational Logic Optimization methods

![image](https://github.com/user-attachments/assets/931a7aed-2f51-4c75-ae71-4db1b1e526f1)

### Constant Propagation Example: 

+ ### Using this the number of transistors are reduced

![image](https://github.com/user-attachments/assets/4a2b6c11-1c08-42a3-a04b-211ff2d9b0a1)

### Boolean Logic Optimisation

### The complex expression is converted into the simplified one

![image](https://github.com/user-attachments/assets/f6e14690-fcc2-4fb8-8a92-8854cf9f577c)

# Sequential Logic Optimization Techniques

![image](https://github.com/user-attachments/assets/ebb3fdec-a0ce-4b5b-9fa5-1c28d4d47b58)

+ ## Sequential Constant Propagation

![image](https://github.com/user-attachments/assets/9508cadd-1cbb-45fc-b241-e228294cfef5)

+ ## Example where Q value is not constant, instead it depends on the nature of set or clk

![image](https://github.com/user-attachments/assets/e48b0d95-ee26-4f84-ada7-136e870ff02b)

## Advanced Optimization Techniques

![image](https://github.com/user-attachments/assets/8064ddc8-1a37-4024-aecb-bfd91550c8e6)

# Labs on  Combinational Logic Optimization 

## Following examples are used to understand optimization

![image](https://github.com/user-attachments/assets/ac6c9007-e3ad-4c77-a7cd-abe5216118bf)

### Example opt_check (Two input AND Gate)

```
module opt_check (input a , input b , output y);
	assign y = a?b:0;
endmodule

```

![image](https://github.com/user-attachments/assets/0cd228e4-9308-4cf1-b5e0-929251dfd333)

# Synthesis

```
1. read_liberty -lib /home/comp/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
2. read_verilog /home/comp/sky130RTLDesignAndSynthesisWorkshop/verilog_files/opt_check.v
3. synth -top opt_check
4. command for optimization: opt_clean -purge
5. abc -liberty /home/comp/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. show

```
![image](https://github.com/user-attachments/assets/bfd0a79d-d065-4d0f-8eee-cd3f8ba13a9f)

![image](https://github.com/user-attachments/assets/9df4c4d7-c4dc-4b8e-b00f-a67cd4192f21)




### Example opt_check2 (Two input OR Gate)

```
module opt_check2 (input a , input b , output y);
	assign y = a?1:b;
endmodule

```
![image](https://github.com/user-attachments/assets/465c7df4-b48e-4cbc-8942-9b4ff923c176)

# Synthesis

![image](https://github.com/user-attachments/assets/fffd65a7-6f9d-460e-baa8-7c42ee0a185d)

### Example opt_check3 (Three input AND Gate)

```
module opt_check3 (input a , input b, input c , output y);
	assign y = a?(c?b:0):0;
endmodule

```
![image](https://github.com/user-attachments/assets/77b2d030-9f04-45f5-ad87-7cd7c807e76f)

# Synthesis

![image](https://github.com/user-attachments/assets/2eccd524-8836-4277-a557-c4b330e5ac0a)

# Labs on Sequential Optimization Techniques

### Example

![image](https://github.com/user-attachments/assets/1a2ef660-0c3a-4a70-9ef2-6ed770806145)


![image](https://github.com/user-attachments/assets/b641839c-d854-4130-8b80-f5e3ae86a3ef)

# Simulation of dff_const1.v

![image](https://github.com/user-attachments/assets/ba9f6635-33ea-433e-bf21-2205653f4cc9)

![image](https://github.com/user-attachments/assets/9f16501d-7068-4373-bc38-6ec7d7f9891c)

# Synthesis

```
1. read_liberty -lib /home/comp/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
2. read_verilog /home/comp/sky130RTLDesignAndSynthesisWorkshop/verilog_files/dff_const1.v
3. synth -top dff_const1
4. dfflibmap -liberty /home/comp/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
5. abc -liberty /home/comp/sky130RTLDesignAndSynthesisWorkshop/lib/sky130_fd_sc_hd__tt_025C_1v80.lib
6. show

```

![image](https://github.com/user-attachments/assets/354cdcec-bd85-4933-b104-4d08db253ffb)


# Simulation of dff_const2.v

### In this example of irrespective of clock and reset Q is always one.

![image](https://github.com/user-attachments/assets/89cc5721-4114-488a-b7aa-47e8f972720c)

![image](https://github.com/user-attachments/assets/051f91c1-636f-472d-9e84-eb7355df1e71)

### Difference between dff_const1 and dff_const2

![image](https://github.com/user-attachments/assets/53a24021-c390-4609-b5e0-3d31ee01820b)

# Synthesis

![image](https://github.com/user-attachments/assets/0ac0fcc7-d569-4911-8d7c-00ba6e220f6a)

# Simulation of dff_const3.v

```
module dff_const3(input clk, input reset, output reg q);
reg q1;

always @(posedge clk, posedge reset)
begin
	if(reset)
	begin
    	q <= 1'b1;
    	q1 <= 1'b0;
	end
	else
	begin
    	q1 <= 1'b1;
    	q <= q1;
	end
end

endmodule

```

![image](https://github.com/user-attachments/assets/586dea9f-bf59-46d2-9cf0-513601e75069)

![image](https://github.com/user-attachments/assets/cd6b19ca-e65f-4335-9a9b-310f69278c32)

# Synthesis

![image](https://github.com/user-attachments/assets/c01eb273-577f-4781-8896-10a8299dc041)


# Sequential optimzations for unused outputs

### Example counter_opt.v

```
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = count[0];

always @(posedge clk ,posedge reset)
begin
	if(reset)
    	count <= 3'b000;
	else
    	count <= count + 1;
end

endmodule

```

![image](https://github.com/user-attachments/assets/89cb5025-16ea-4208-9c9f-8f509e4445fa)

#Synthesis

![image](https://github.com/user-attachments/assets/89dd87ff-c939-4401-a8a9-839689af0647)


![image](https://github.com/user-attachments/assets/3759f888-7c5c-40ab-88a5-14551b0be549)

### Example counter_opt2.v

```
module counter_opt (input clk , input reset , output q);
reg [2:0] count;
assign q = (count[2:0] == 3'b100);

always @(posedge clk ,posedge reset)
begin
	if(reset)
    	count <= 3'b000;
	else
    	count <= count + 1;
end

endmodule

```


# Synthesis

![image](https://github.com/user-attachments/assets/6c3b9b24-417d-43cb-a481-de4154e406eb)

![image](https://github.com/user-attachments/assets/d16b37b0-f5a3-4498-ad59-f005c52a9c28)

![image](https://github.com/user-attachments/assets/b26e5b4b-e003-4b60-8c2d-71b86b18bb9f)














