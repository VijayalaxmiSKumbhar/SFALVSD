# VSDBabySoC Modelling
VSDBabySoC contains three IP cores `RVMYTH (RISC-V based CPU)`, `PLL` and `DAC` along with a wrapper that acts as the `SoC` and also a separate `testbench` module. Here will model and simulate the VSDBabySoC using `Iverilog`, and the results are presented using `GTKWave` tool. Initial input signals will be applied to the VSDBabySoC module to trigger the `PLL`, enabling it to generate the appropriate clock signal for the circuit. This clock signal will allow the `RVMYTH` to execute instructions stored in its instruction memory. Consequently, the register r17 will be populated with values over several cycles. These values will be utilized by the `DAC` core to produce the final output signal, referred to as `OUT`.

# Tools Required
* __Iverilog__
* __GTKWave__
