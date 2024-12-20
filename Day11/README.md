# VSDBabySoC Modeling
VSDBabySoC contains three IP cores `RVMYTH (RISC-V based CPU)`, `PLL` and `DAC` along with a wrapper that acts as the `SoC` and also a separate `testbench` module. Here will model and simulate the VSDBabySoC using `Iverilog`, and the results are presented using `GTKWave` tool. Initial input signals will be applied to the VSDBabySoC module to trigger the `PLL`, enabling it to generate the appropriate clock signal for the circuit. This clock signal will allow the `RVMYTH` to execute instructions stored in its instruction memory. Consequently, the register r17 will be populated with values over several cycles. These values will be utilized by the `DAC` core to produce the final output signal, referred to as `OUT`.

# Tools Required
-----
* __Iverilog:__ Used to Compile and Simulate.
* __GTKWave:__ To see the waveforms and debug.
-----

#### Steps
```
VSDBabySoC Project/
├── README.md
├── src/
│ ├── vsdbabysoc.v                # Top-level module
│ ├── rvmyth.v                    # RISC-V based core module
│ ├── avsdpll.v                   # Phase-locked loop module
│ └── avsddac.v                   # Digital-to-analog converter module
├── sim/
│ ├── testbench.v                 # Testbench
│ └── run_simulation
├── Output/

```

    

##### VSDBabySoC Module Descriptions

-----

1. `VSDBabySoC.v`
This is the primary module that combines the rvmyth, pll, and dac modules. (https://github.com/manili/VSDBabySoC?tab=readme-ov-file#vsdbabysoc-modeling)
* Inputs
  
  `reset:` This signal is used to reset the core processor of the SoC. When activated, it initializes or clears the state of the system.
  
  `VCO_IN:` This is the input signal for the Voltage-Controlled Oscillator (VCO), which plays a critical role in generating clock signals.
  
  `ENb_CP:`This is an enable signal for the charge pump (CP), which is used in Phase-Locked Loop (PLL) circuits to regulate the output frequency.
  
  `ENb_VCO:` This signal serves to enable or disable the VCO.
  
  `REF:`This is a reference signal utilized by the PLL for frequency comparison and stabilization.
  
  `VREFH:` This is the high reference voltage for the DAC. It provides the necessary voltage level that determines the range of output voltages from the DAC.
  
* Outputs
  
  `OUT:` This is the analog output from a Digital-to-Analog Converter (DAC)
  
* Internal wires
  
  `CLK:` This is used to carry the clock signal generated by the PLL. It is crucial for synchronizing activities within the SoC.
  
  `RV_TO_DAC:`This is a 10-bit wide signal that connects the output signals from a RISC-V core to the input of the DAC. The width suggests that it can carry values 
   ranging from 0 to 1023 (in decimal), allowing for 1024 different values to be sent to the DAC.

-----

  
2. `rvmyth.v`
It is a RISC-V based IP core. That gives 10-bit digital as the output `(OUT)`

* Inputs

  `CLK:` rvmyth accepts a clock signal called CLK. This clock signal is important for synchronizing operations within the module.

  `reset:' rvmyth takes an external reset signal named reset. When asserted, this signal resets the state of the rvmyth module back to its initial conditions, 
   which is a common feature in digital systems to manage states safely.

* Output 
  `OUT(RV_TO_DAC):` The output of the rvmyth module is connected to the RV_TO_DAC wire defined in the parent module. The RV_TO_DAC wire is 10 bits wide, indicating 
   that the output from this module contains digital data that can be directed to a DAC (Digital-to-Analog Converter).

------


3. `avsdpll.v`
    This is a Phase-Locked Loop (PLL) designed to synchronize its output frequency with a reference frequency. 

* Inputs
  
  `VCO_IN(VCO_IN):' This input is connected to the Voltage-Controlled Oscillator (VCO) input, allowing the PLL to adjust the output frequency.
  
  `ENb_CP(ENb_CP):` This is the enable (or disable) signal for the Charge Pump (CP) inside the PLL. When low, it enables the Charge Pump.
  
  `ENb_VCO(ENb_VCO):` This is the enable (or disable) signal for the VCO. It controls whether the VCO operates or is disabled.
  
  `REF(REF):` This is the reference signal that the PLL aims to lock onto. It provides the frequency or timing reference for the PLL operation.

* Outputs
  
  `CLK(CLK):` This is the primary clock input for the PLL. It provides timing for operations within the PLL.


------

4. `avsddac.v`
   This module is a Digital-to-Analog Converter (DAC) that translates digital signals into corresponding analog voltages. T

* Inputs
  `RV_TO_DAC:` This input represents the digital value to be converted to an analog signal. It is typically a binary signal that defines the output voltage level.

  `VREFH(VREFH):` This is the high reference voltage for the DAC. It establishes the range of output voltages by providing a reference against which the digital 
   values are converted.

* Ouputs
  
  `OUT:` This is the output of the DAC, which provides the resulting analog voltage based on the digital input.



`testbench_vsdbabysoc.v`



It is a simulation environment for the `VSDBabySoC` module. It initializes the necessary signals, instantiates the Device Under Test `(DUT)`, manages waveform dumping for analysis, and generates a sequence of input signals to observe the response of the SoC design under test. This produces pre-synthesis and post-synthesis simulations through conditional compilation.

#### Simulation Steps


* Pre-synthesis Simulation
  
1. git clone https://github.com/manili/VSDBabySoC.git
2. cd VSDBabySoC
3. rvmyth.v file (https://github.com/Devipriya1921/VSDBabySoC_ICC2) is added to VSDBabySoC/src/module
4. rvmyth_gen.v file (https://github.com/Devipriya1921/VSDBabySoC_ICC2) is added to VSDBabySoC/src/include
5. mkdir -p output/pre_synth_sim
6. iverilog -o output/pre_synth_sim/pre_synth_sim.out -DPRE_SYNTH_SIM -I src/include -I src/module src/module/testbench.v
7. cd output/pre_synth_sim
8. /pre_synth_sim.out
9. gtkwave pre_synth_sim.vcd

    
![image](https://github.com/user-attachments/assets/b8fd67c0-c37b-4c97-9f3d-0a00489d4ad9)

* To view the waveform in gtkwave give the following command
  
  `gtkwave pre_synth_sim.vcd`

* Drag and drop the signals CLK, reset, OUT(DAC) (select the format as `analog step`), RV TO DAC [9:0]

![image](https://github.com/user-attachments/assets/b55a67d5-ca03-4823-b56b-d417c670d4c7)

##### yosys 

`read_verilog /home/comp/VSDBabySoC/src/module/vsdbabysoc.v`

![image](https://github.com/user-attachments/assets/cb2628d8-f471-41ef-a531-e4f81e4db681)

`read_verilog -I /home/comp/VSDBabySoC/src/include  /home/comp/VSDBabySoC/output/compiled_tlv/rvmyth.v`

![image](https://github.com/user-attachments/assets/1cc571cb-b21a-460c-ae96-236d94c2cfd1)

`read_verilog -I /home/comp/VSDBabySoC/src/include  /home/comp/VSDBabySoC/src/module/clk_gate.v`

![image](https://github.com/user-attachments/assets/c12ab4da-1730-4422-847a-21e14188875d)

```
read_liberty -lib /home/comp/VSDBabySoC/src/lib/avsdpll.lib
read_liberty -lib /home/comp/VSDBabySoC/src/lib/avsddac.lib
read_liberty -lib /home/comp/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib

```

![image](https://github.com/user-attachments/assets/c95f7c7a-0159-42a1-951f-ffaba8cb3f3a)


`synth -top vsdbabysoc`

![image](https://github.com/user-attachments/assets/e6ef0494-d6f7-4274-890b-089098cf09b5)
![image](https://github.com/user-attachments/assets/e479f3c9-70bb-42b6-a2a2-597f80fcbdae)
![image](https://github.com/user-attachments/assets/c5386d9c-a6fe-4e2a-96ed-36a1b115a065)
![image](https://github.com/user-attachments/assets/65c878e5-c1bb-4ad8-b956-42f6f9cd7ddc)
![image](https://github.com/user-attachments/assets/56adb6f5-11e6-4453-baf2-6b264d5faa15)


`dfflibmap -liberty /home/comp/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib`

![image](https://github.com/user-attachments/assets/b4a5447f-ecc2-4a9f-9125-283d222a6e85)

`opt`

![image](https://github.com/user-attachments/assets/b4214304-562e-4b2a-bd1d-ed24ef3f83d4)

`abc -liberty /home/comp/VSDBabySoC/src/lib/sky130_fd_sc_hd__tt_025C_1v80.lib -script +strash;scorr;ifraig;retime;{D};strash;dch,-f;map,-M,1,{D}`

![image](https://github.com/user-attachments/assets/b08126a3-4dc2-4e49-8fb5-11ff53c2e645)


```

flatten
setundef -zero
clean -purge
rename -enumerate

```

![image](https://github.com/user-attachments/assets/c8ea3fb9-f405-43a3-84fb-94b30896b8b1)

`stat`

![image](https://github.com/user-attachments/assets/956efc75-2e69-458f-ad9b-f3e9ea02554a)
![image](https://github.com/user-attachments/assets/a2e281d8-2bf2-424c-aa75-1668903742e6)
![image](https://github.com/user-attachments/assets/7e089d64-5f7b-4a73-a868-dee495e6f1b9)


`write_verilog -noattr /home/comp/VSDBabySoC/output/synth/vsdbabysoc.synth.v`

![image](https://github.com/user-attachments/assets/85cc466c-f409-4df1-b49f-ea51a8904131)


##### Post-Synthesis

```

* sudo make synth

* sudo make post_synth_sim

```

![image](https://github.com/user-attachments/assets/49bc5d8d-df3c-487f-8feb-5a7c3f471d7e)


##### To see the waveforms

`gtkwave output/post_synth_sim/post_synth_sim.vcd`


![image](https://github.com/user-attachments/assets/81488686-06f3-472c-9569-cbfc7a772038)


##### Waveforms

![image](https://github.com/user-attachments/assets/447f2281-f958-4f55-8fd4-dfcea3fcfc51)



