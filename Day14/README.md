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


#### Introduction to OpenLANE and Strive Chipsets

* Started as Open-Source Flow for a True Open-Source Tape-out Experiment
* striVe is a family of `open everything` SoC's
  * Open PDK, Open EDA, Open RTL
 
![image](https://github.com/user-attachments/assets/d10342b2-6e41-452b-b021-bb0e7a6c7469)

* Members of striVe SoC family

  ![image](https://github.com/user-attachments/assets/1120ad0b-0fc7-43fb-aa8b-0258478534b5)

* Features of OpenLANE
  * Tuned for SkyWater 130nm Open PDK
  * Containerized
    * Functional out of the box
    * Instructions to build and run natively will follow
  * Can be used harden Macros and chips.
  * It has two modes of operation
    * Autonomous or Interactive
  * It has Design Space Exploration
    * Find the best set of flow configurations
  * OpenLANE comes with large number of design examples
    * 43 designs with their best configurations
    * More will be added soon
   
#### OpenLANE ASIC flow

![image](https://github.com/user-attachments/assets/50a8029a-f548-4c38-a3c9-ae956d5186b3)

* OpenLANE is based on several opensource projects

![image](https://github.com/user-attachments/assets/400a4025-1f81-4bd7-b46b-63b2ce0a3719)

* `Synthesis Exploration`: It generates the reports that shows how the delay and area are affected by synthesis strategy.

  ![image](https://github.com/user-attachments/assets/3d548d7e-7bc7-4181-a611-55d6185576d5)

* `Design Exploration`: Used to sweep design configurations. It generates the reports as given here. This report shows different design metrics.
* `Design Exploraion` is also used for regression testing (CI)
* We run OpenLANE on ~70 designs and compare the results to best known ones.

![image](https://github.com/user-attachments/assets/8f27244a-f446-4ad2-acb5-6b4279d45499)
![image](https://github.com/user-attachments/assets/307b3bb9-0b2d-42d9-88e3-76000d83fd8c)

* `Design for Test (DFT)`:
  * Scan Insertion
  * Automatic Test Pattern Generation (ATPG)
  * Test Patterns Compaction
  * Fault Coverage
  * Fault Simulation

![image](https://github.com/user-attachments/assets/3f66061a-1efd-4991-a579-8b552fab96c0)

* `Physical Implementation (also called automated PnR Place and Route)`
  * Floor/Power Planning
  * End Decoupling capacitors and tap cells insertion
  * Placement: Global and Detailed
  * Post placement optimization
  * Clock Tree Synthesis (CTS)
  * Routing: Global and Detailed.
 
* Dealing with Antenna Rule Violations

  * When a metal wire segment is fabricated, it can act as antenna.
    * Reactive ion etching causes charge to accumulate on the wire
    * Transistor gates can be damaged during fabrication
   
  ![image](https://github.com/user-attachments/assets/adb2349b-976c-4572-9c18-0beb51b6d327)

* There are two solutions to overcome this
  * Bridging attaches higher layer intermediary
  * Add antenna diode cell to leak away charges (Antenna diodes are provided by SCL)

![image](https://github.com/user-attachments/assets/d2d4e746-379c-4d77-ba5d-bdc5ed38ac41)

* A preventive approach
  * Add a `Fake antenna diode` next to every cell input after placement
  * Run the antenna checker `(Magic)` o the routed layout.
  * If the checker reports a violation on the cell input pin, replace the `Fake diode cell` by real one.

![image](https://github.com/user-attachments/assets/52dffdd4-a2bc-4975-9625-2bcff8237a34)
 
* Static Timing Analysis
 
![image](https://github.com/user-attachments/assets/05e1b56d-0432-4cf6-a990-199e9e4aef61)

* Physical Verification involves `DRC` and `LVS`
  * Magic is used for Design Rules Checking and SPICE extraction from Layout.
  * Magic and Netgen are used for LVS
    * Extractec SPICE by Magic Vs. Verilog Netlist.
   
  ![image](https://github.com/user-attachments/assets/2b758f1d-b0b8-4bf7-8f75-70200d5ea3e9)

</details>

<details>
  <summary>Get Familiar to Open Source EDA Tools</summary>
  <br>

  ## OpenLANE Working Directory Structure
  cd/Desktop/work/tools/openlane_working_dir

  ![linuxcommands](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/63a389c8-6025-4b6a-b103-423c875d2234)

* Note: Some useful Linux Commands

  `cd` : Change directory

  `ls` : list files 

  `ls -ltr` : List the files in chronological order

   `ls --help` : Gives the detailed information about commands
   
#### Process Design Kit (pdks)
* `skywater-pdk` : It has all the pdk related files means timing libraries, tech file etc.
* `open_pdk` : It provides the necessary technology files (LEF/DEF) and libraries required for designing integrated circuits, specifically tailored for use with the OpenLane flow.
* `sky130A` : It contains libs.ref and libs.tech. 

![image](https://github.com/user-attachments/assets/ae30cb39-ac12-4577-9616-f0ed076f6f09)

* `libs.ref` (Specific to technology), `libs.tech` (Specific to tools)

![libs](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/e0d718bf-fb9a-4c3c-adf4-b39538f1029e)

* sky130_fd_sc_hd
  * `sky130': Process
  *  `fd`: Abbreviated foundary name. It is skywater foundary
  *  `sc`: standard cell library
  *  `hd`: high density

![sc](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/371b3f31-fc41-466e-a0f1-13aa1b433bfb)

* To invoke the tool
  * `docker` 
    `./flow.tcl -interactive`

![openlane](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/ff642715-c5eb-4d00-ba6d-6e265974a857)

## Design Preparation Steps

* `package require openlane 0.9`
* `prep -design picorv32a`

![image](https://github.com/user-attachments/assets/81ac7fd4-eab3-466a-b63c-c21972e30519)

* Various designs in openlane: It has around 40 designs

![image](https://github.com/user-attachments/assets/5247ca15-3106-41f6-9d2e-ac08518d29a3)

* picorv32a contains 3 files

 * `src`: stands for source 

 * `sky130A_sky130_fc_sc_hd_config.tcl`: pdk specific configuration file
 
 * `config.tcl` file


![picorv32a](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/d2a79fd2-80bd-48c0-a2ce-f5774ba23fa5)

less config.tcl contains all the information

* `design environment`

* `verilog file`

* `sdc file`

* `clock period`

* `setting of the file`

![config](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/b96eec9a-2f3b-4fb3-b0f3-841cc905029a)

* `prep -design picorv32a`
  * step 1: `mergeLef.py` -----> It combines two files into one

![designprep](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/0afd49ae-0dce-45e3-bd30-abf0a46f76c3)

* `runs directory is created`

![image](https://github.com/user-attachments/assets/4f42fd2f-da7f-4ceb-9204-0797654ef11e)

* `folder structure required for openLane`

![image](https://github.com/user-attachments/assets/ec9d0422-17ba-4f23-9f23-ee25b37a75d9)


* `cd tmp`

![image](https://github.com/user-attachments/assets/aa92a1a7-376c-4bb7-902b-6705fef9ed3c)


* `less merged.lef`

![merged](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/9695e7dc-e993-42b7-9800-28e9de3539ef)

* `cd runs`

* `cd results`

* `cd synthesis`

![image](https://github.com/user-attachments/assets/1d0d297c-0f0a-4cbd-93a8-0c32ff13a2d3)


* `cd reports`

![image](https://github.com/user-attachments/assets/a08e67c5-d40f-4d3e-8525-ad173780451d)

* `less config.tcl`: it shows the default parameters taken by run

![configtcl](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/2f878d07-9a84-4b6f-99f7-cf421c88303d)

* `run_synthesis`

![synthesis](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/45f0224d-1e11-428e-a314-e597a21e876e)

* `cd results/synthesis` : shows the verilog file of design

![image](https://github.com/user-attachments/assets/301ecbdb-dc2e-455c-bcfa-ff04fc01e920)


* `cd reports/synthesis`

![image](https://github.com/user-attachments/assets/fecc4c51-56cd-47db-9868-2bea9ae4e28c)

* Actual synthesis statics report from this we calculate the flop ratio

* command to get the synthesis reports

![image](https://github.com/user-attachments/assets/3e5d2653-f380-4c3c-8145-b6f345dddb2d)


![image](https://github.com/user-attachments/assets/11931170-4ca0-446a-81e7-1ad6169b035c)

* Flop ratio

![flopratio](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/8bb0301f-90e1-4417-93ae-c62e774f75ee)

* sta timing report

![image](https://github.com/user-attachments/assets/e1d15e6c-8c47-4905-908c-f912011c604b)


</details>
