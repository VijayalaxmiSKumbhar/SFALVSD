## Inception of open-source EDA, OpenLANE and Sky130 PDK

<details>
  <summary> How to talk to computers</summary>
  <br>

##### Introduction to QFN 48 Package, chip, pads, core, die and IPs.

* Block diagram of typical board

![image](https://github.com/user-attachments/assets/d8b45192-3c9a-4857-b0c8-2dae3ad448bc)

* Example of QFN-48 Package

![image](https://github.com/user-attachments/assets/85490fab-021d-47db-9529-27754bae2c25)

* This is how the chip is connected in package to communicate with outside world

![image](https://github.com/user-attachments/assets/82f5d98e-818b-497e-818c-5e13724fc5d5)

* There are various components of Chip
  * `Pads`: Pads are something through which we can send the signals inside the chip.
  * `Core`: It is a place where all the digital logic is present.
  * `Die`: Size of the entire chip

![image](https://github.com/user-attachments/assets/11544b08-bff4-40e1-ba22-6b98589b1312)

* `Foundary IP's` and `Macros`

  ![image](https://github.com/user-attachments/assets/e9b1b95e-8665-4f0c-a914-9ae80435cff4)

* RISC-V Instruction Set Architecture (ISA)

![image](https://github.com/user-attachments/assets/fc01fb96-c642-4141-a7b2-007c5b0518d1)

![image](https://github.com/user-attachments/assets/8abc92d5-4567-412f-a181-e7bb5ad20aa3)

* Abstract Interface

  ![image](https://github.com/user-attachments/assets/6922ddb3-8a7d-497b-a3b1-b2db4f07148a)

  
</details>

<details>
  <summary> SoC Design using OpenLANE</summary>
  <br>

* Open Source Digital ASIC Design

 * There are three important components of open source Digital ASIC Design:
   * `Open Source RTL Designs`
   * `Open Source EDA tools`
   * `Open Source PDK data`

![image](https://github.com/user-attachments/assets/2c800da3-e73f-400d-a90a-eb7d008cb285)


* What is PDK (Process Design Kit)?
    * `It is the interface between FAB and designers`
    * `Collection of files used to model a fabrication process for the EDA tools used to design an IC
       * Process Design Rules: DRC, LVS, PEX
       * Device Models
       * Digital Standard cell libraries
       * I/O libraries
       * .....`
    * On June 30, 2020 Google released first ever open PDK

      ![image](https://github.com/user-attachments/assets/15f1bb85-80aa-485b-b936-b1e8fbcf179f)

* Is 130nm old and not in use?
  130nm is old, but it is still used in some applications.

* Is 130nm Fast?
  * `YES`
  * Exmple

   ![image](https://github.com/user-attachments/assets/e5e847cc-29c3-451f-befc-e39ac0212cb7)

* Simplified RTL to GDSII Flow

![image](https://github.com/user-attachments/assets/db2af022-98f0-4ca3-b266-2f40c099193c)

* Step-1: Synthesis : `It converts RTL to a circuit out of components fro the standard cell library (SCL)`

  ![image](https://github.com/user-attachments/assets/3bd7885e-51fc-49e1-b04d-27856abe2114)
  ![image](https://github.com/user-attachments/assets/838c723b-dabc-4ec8-a969-ec72756e5a00)

* Step-2: Floor and Power Planning:
  
         * Chip Floor Planning: `Partition the chip die between different system building blocks and place the I/O pads`

          ![image](https://github.com/user-attachments/assets/0dc22710-72ff-4335-a726-e57952da9f2c)

         * Macro Floor Planning:  `Dimensions, pin locations, rows definition`

           ![image](https://github.com/user-attachments/assets/f0946865-f204-42a4-ad69-251b15e1e60e)

         * Power Planning:

           ![image](https://github.com/user-attachments/assets/2057b9b9-446d-468e-a5a1-51e0d07718ec)

  * Step-3: Placement: `Place the cells on floorplan rows, aligned with sites.
 
    ![image](https://github.com/user-attachments/assets/a807d6cd-9d90-4482-9c2f-b99d81a9b26f)

    * Placement is done in 2 steps, Global placement followed by Detailed.

     ![image](https://github.com/user-attachments/assets/366c5aa1-a222-4d0b-a773-cbf2c05b640a)

  * Step-4: Clock Tree Synthesis (CTS): `To create clock distribution network`
 
    ![image](https://github.com/user-attachments/assets/53beda13-7b9d-43a4-93ed-14268b7da579)

* Step-5: Routing: `Implement the interconnect using available metal layers`

  ![image](https://github.com/user-attachments/assets/3dc6af6e-cb4f-4d6f-a36b-7d81c9162025)
  ![image](https://github.com/user-attachments/assets/9ed17b92-a15b-44b8-be6c-1e4873bd9afe)

* Step-6: Sign off: It consists

  * Physical Verifications
    * Design Rules Checking (DRC)
    * Layout Vs Schematic (LVS)

  * Timing verification
    * Static Timing Analysis (STA) : To verify that all the timing constraints are met.



  
</details>
