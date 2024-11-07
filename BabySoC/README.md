# Introduction to BabySoC and Fundamentals of SoC

##### Problem Statement
This project aims to develop a compact, open-source System on Chip (SoC) that incorporates RVMYTH, a processor core based on the RISC-V architecture. The SoC includes a Phase-Locked Loop (PLL) for precise clock generation and control, along with a 10-bit Digital-to-Analog Converter (DAC) that connects to external analog systems. This DAC allows the BabySoC to convert digital signals into analog, enabling it to communicate with devices that require analog inputs, such as televisions and mobile phones, thus facilitating audio and video output. Ultimately, this SoC, created using Sky130 technology, is designed to be a well-documented educational tool for learning and experimentation. 

<details>
<summary>What is Soc and Why SoC?</summary>
  
```
* SoC is a single-die chip tha has some different IP cores on it. These IPs could vary from microprocessors (completely digital) to 5G broadband modems (completely analog).
* The design of SoC usually includes a Central Processing Unit (CPU), memory, ports for inputs and outputs, secondary storage devices, and peripheral interfaces such as Timers, etc.
* Depending on the requirement it can also consists of a digitalor analog signal processing system or a floating point unit.
* SoC with equivalent functionality will have increased performance and reduced power consumption as well as a smaller semiconductor die area.
```


  
</details>

