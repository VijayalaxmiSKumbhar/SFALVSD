# PVT (Process Voltage Temperature) Analysis

#### Integrated circuits are designed in such a way that they can function in a wide variety of vltages and temperatures, rather than a single voltage and temperature. These must function in variety of contexts including various conditions, electrical setup, user environments etc.

<details>
<summary>What is PVT?</summary>
<br>

* `Process (P)` : There are millions of transistors on a singke chip as we are going to lower nodes and all the transistors in a chip cannot have same properties. Process variation is the deviation in parameters of the transistors during fabrication.

* `Voltage (V)`: As we are going to lower nodes the supply voltage for a chip is also going to less. Let's say the chip is operating at 1.2 V. So, there are chances that at certain instances of time this voltage may vary.

* `Temperature (T)`: When a chip is operating, the temperature can vary throught the chip. This is due to power dissipation in MOS- transistors.
  
</details>

<details>
<summary>Corners of PVT?</summary>
<br>

* In order to make our chip to work after fabrication in all the possible conditions, we simulate it at different corners of process, voltage and temperature.

* These conditions are called corners. All these three parameters directly affect the delay of the cell.
  
</details>
