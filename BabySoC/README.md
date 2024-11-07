# Introduction to VSDBabySoC and Fundamentals of SoC

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

##### Advantages of SoCs
1. __Integration:__ Combines multiple functions into a single chip, reducing the need for separate components.
2. __Size and Portability:__ Smaller form factor allows for compact designs in devices like smartphones, tablets, and wearables.
3. __Power Efficiency:__ Optimized for low power consumption, making them suitable for battery-powered devices.
4. __Cost-Effectiveness:__ Reduces manufacturing and assembly costs by minimizing the number of discrete components.
5. __Performance:__ SoCs are designed for efficiency, with specialized architectures that enhance speed and responsiveness.

##### Applications of SoCs
1. __Mobile Devices:__ SoCs are commonly used in smartphones and tablets, integrating the CPU, GPU, memory, and other components onto a single chip for improved performance and power efficiency.
2. __Embedded Systems:__ In consumer electronics, such as smart TVs, smart home devices, and wearables, SoCs enable functionalities such as connectivity, processing, and multimedia processing.
3. __Internet of Things (IoT):__ SoCs are essential in IoT devices, providing the necessary processing power and connectivity for smart sensors, home automation, health monitoring, and industrial applications.
4. __Gaming Consoles:__ High-performance gaming consoles utilize SoCs to integrate graphics processing and gaming logic on a single chip for enhanced gaming experiences.
5. __Medical Devices:__ SoCs are utilized in medical imaging equipment, wearables for health monitoring, and diagnostic tools to provide accurate and efficient processing capabilities.
6. __Artificial Intelligence (AI):__ Certain SoCs are designed with AI acceleration capabilities for edge computing applications, enabling real-time data analysis and machine learning functionalities.

##### Well Known SoCs
1. Qualcomm Snapdragon
2. Apple A-Series
3. MediaTek Helio and Dimensity
4. Samsung Exynos
5. Google Tensor
6. Kirin
7. Rockchip and Allwinner
8. NVIDIA Tegra
9. Texas Instruments OMAP
10. Raspberry Pi SoCs

##### Typical structure of Snapdragon SoC and its Key features

* SoCs integrate a variety of components, including the CPU (central processing unit), GPU (graphics processing unit), modem for cellular connectivity, and various other multimedia and processing functions.

* Some key features and components associated with Snapdragon SoCs:

1. __CPU Architecture:__ Snapdragon SoCs often incorporate Qualcomm's custom CPU cores, such as the Kryo series, alongside standard ARM Cortex cores. The architecture is designed to optimize performance and energy efficiency.
2. __GPU:__ Snapdragon processors include Adreno GPUs for enhanced graphics performance, which is beneficial for gaming, video playback, and other graphically intensive tasks.
3. __Modem:__ Many Snapdragon chips come with integrated modems supporting various connectivity standards, including 4G LTE and 5G. They provide capabilities for high-speed mobile data and voice over LTE (VoLTE).
4. __AI Capabilities:__ Recent Snapdragon SoCs feature dedicated AI processing units (APUs), which enhance performance for AI-related tasks, including image recognition and voice processing.
5. __Camera Support:__ Snapdragon SoCs typically integrate advanced image signal processors (ISPs) that support high-resolution camera sensors, multiple camera setups, and features like HDR and video recording.
6. __Multimedia Features:__ Snapdragon chips support high-definition audio and video codecs, enabling high-quality media playback and recording capabilities.
7. __Power Efficiency:__ Qualcomm designs its SoCs to maximize performance while minimizing power consumption, which is crucial for extending battery life in mobile devices.
8. __Ecosystem:__ Snapdragon SoCs are commonly used across various devices and support a wide range of software, including Android and other operating systems.
<
  <div align="center">
    <![image](https://github.com/user-attachments/assets/ae10e112-4959-4e75-a6fb-ee40b544ebe7)>
</div>


__SoCs__ are a foundational technology driving the advancement of modern electronics, providing a compact, efficient, and powerful solution for a wide variety of applications. They play a crucial role in the ongoing evolution of devices we use daily, impacting everything from consumer gadgets to complex industrial and automotive systems.

</details>

<details>
<summary>Types of SoC</summary>

* SoCs built around a microcontroller
* SoCs built around a microprocessor, often found in cell phones.
* Specialized application-specific integrated circuit SoCs, designed for specific applications.
    Examples: Google’s Tensor Processing Units (TPUs) for machine learning, Bitcoin ASIC miners.
  
</details>

<details>
<summary>SoC Design Flow</summary>

* __System Specifications:__ Defining and creating the specifications of the design. For example in 4 * 4 array multiplier, the specifications are nothing but two 4-bit inputs and the result is 8-bit output.
* __Architecture Design:__ It inculdes deciding the blocks and hierarchy.
* __Basic Logic Design:__ This is basically a schematic design.
* __Logic Verification:__ Veriifcation of functionality. This is done using simulation tools.
* __Physical Design:__ Translation of schematic design into layout
* __Physical Verification:__ DRC will check for any design rule violations for example metal spacing etc
* __Chip Fabrication__
  
![image](https://github.com/user-attachments/assets/413967bd-5e00-4eb6-9481-146ad6a9a7eb)

  
</details>

<details>
<summary>Introduction to VSDBabySoC</summary>

* __VSDBabySOC__ is small yet powerfull RISC-V based SoC. The main purpose of this SoC is to test IP cores. The IP cores used here are __RVMYTH__, __PLL__ and __DAC__.
* __VSDBaby SoC Componets__
  * __RVMYTH :__ It is a simple RISC-V based CPU.
  * __PLL (Phase Locked Loop):__ It is a control system that generates an output signal whose phase is related to the phase of an input signal. PLLs are widely used for synchronization purposes, including clock generation and disribution.
  * __DAC (Digital to Analog Converter):__ It is a system that converts a digital signal into an analog signal. DACs are widely used in modern communication systems enabling the generation of digitally-defined transmission signals.
     
![image](https://github.com/user-attachments/assets/2434c5ce-52c8-47ac-bf72-2427ac9b5079)


  
</details>
