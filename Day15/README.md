<details>
  <summary> Good floorplan Vs bad floorplan and introduction to library cells: Theory</summary>
  <br>

  * First step in physical design is defining `width (W)` and `height (H)` of `Core` and `Die`

  ![image](https://github.com/user-attachments/assets/27eac35f-3fa5-4303-a4a1-553cdba608c3)

* Example to idwntify width and height
  * Let us consider the following netlist

![image](https://github.com/user-attachments/assets/c5b4ebf9-7e8b-44f3-9488-a9f24a7c9f50)

* Let us convert the highlighted symbols into physical dimension.

![image](https://github.com/user-attachments/assets/76b44ace-d8b7-492f-a3a5-d26e563a5570)

* Let us assume the rough dimensions

![image](https://github.com/user-attachments/assets/b2e27a71-8cdf-4565-bd99-6b5909c5983f)
![image](https://github.com/user-attachments/assets/597ca830-35b9-4eb7-b9f2-edbe2929b51f)

* What is `Core` and `Die` section of Chip?

  * `Core`: It is the section of the chip where the fundamental logic of the design is placed.
  * `Die`: It consists of a core, is small semiconductor material specimen on which the fundamental circuit is fabricated.

![image](https://github.com/user-attachments/assets/f3d47a2c-c9bb-4a10-b218-f4307b775eec)
![image](https://github.com/user-attachments/assets/b83ca9d2-7a81-4359-ad6e-9f8338ad9837)

* To arrive at dimensions place all the logic cells inside the core

![image](https://github.com/user-attachments/assets/d31349f4-1c91-4348-aab2-dac76482dd33)
![image](https://github.com/user-attachments/assets/64aa696a-e586-4cc6-8abf-2b3f3e875b09)
![image](https://github.com/user-attachments/assets/8f4e2711-79dd-46c5-98ed-aed3863427ee)

* In this case `utilization factor = 1`
  
* 100% utilization factor means core is completely occupied and there is no space to add any extra logic
  
* `Aspect Ratio = Height/Width`
  
* In the above example Aspect Ratio=1
  
* `Aspect Ratio = 1` signifies that chip is `square` shaped
  
* `Aspect Ratio` other than 1 signifies that chip is `rectangular` shaped

* ![image](https://github.com/user-attachments/assets/6efdf404-fa26-449c-be64-e95c8e1de63d)

* Example to understand `utilization factor` and `aspect ratio`

![image](https://github.com/user-attachments/assets/c70e43bc-48a0-457f-af36-908b8b4e5ef1)

</details>


<details>
  <summary>Good floorplan Vs bad floorplan and introduction to library cells: Lab </summary>
<br>
  
#### Just go to to the location given in the screenshot and try to open the readme file

![image](https://github.com/user-attachments/assets/09b4e8dc-9cc0-4e8b-b5ef-125929b1b426)

#### README.md file by giving the command less README.md: Here you can see the variables required for each stage, these variables are noting but switches

![image](https://github.com/user-attachments/assets/db8fc66e-ae66-4ad2-9c1b-1bb486683e45)

#### To see the default settings of the floorplan type the following command

#### less floorplan.tcl

#### In the screenshot FP_IO_MODE 1 indicates that the pins are positioned randomly around the core but at equi distant for zero they will not be at equi distant

![image](https://github.com/user-attachments/assets/12933317-3809-4277-afd3-566afcb27335)

#### less config.tcl: shows design name, clock period etc

![image](https://github.com/user-attachments/assets/3ce7b835-5017-4305-8006-f5009edb62ef)

#### To run the floor plan just give the command as run_floorplan

![aspectratioo](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/a8abead7-877d-4aca-825a-860c3f8dc6f3)

![floorplan](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/cf5c3f91-6a1b-4bcb-91d6-9f948a698f81)

![1dieaarea](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/429b50f4-6d1a-4833-8c19-b78b1481d945)

#### default parameters set for floorplan in openlane

![image](https://github.com/user-attachments/assets/cb6d9c56-2ff3-4701-b490-4b4d4be5d869)

#### logs/floorplan/

![image](https://github.com/user-attachments/assets/42725de1-0913-4281-98a9-5921d53eb1dd)

#### ioPlacer.log

![image](https://github.com/user-attachments/assets/aa1b3bc6-12d0-4b36-800f-c3435812c074)

![image](https://github.com/user-attachments/assets/3122ac0c-7435-4ae3-908a-4485af0d73d8)

#### def file: design exchange format

![image](https://github.com/user-attachments/assets/d454d048-4c93-4cfe-b56d-f37ff41edda5)

#### beginning of def file is diearea

![image](https://github.com/user-attachments/assets/a55c59ac-9ce0-4970-9826-3381e0069a15)

![image](https://github.com/user-attachments/assets/31d96e7c-b548-4ad2-9a5b-b02977cc4692)

#### Press s and v to fit it on screen properly

![image](https://github.com/user-attachments/assets/f5c6b1c7-e9e5-4c81-bd97-f91646c2d2f4)

![image](https://github.com/user-attachments/assets/1e31bcb4-ebb7-437f-9a99-366d76de6328)

#### move the cursor on particular object and then press s

#### go to tkcon main and type what it will show the details as in the screenshot

![image](https://github.com/user-attachments/assets/06538254-9343-49e2-bb8e-95cd7b83ea84)

#### `cd Desktop/work/tools/openlane_working_dir/openlane`

#### git clone `https://github.com/nickson-jose/vsdstdcelldesign`

![10](https://github.com/VijayalaxmiSKumbhar/VSD-SoC-Design-Program/assets/170864002/46645870-db68-4a72-8829-a900744dcd50)

#### Various files in vsdstdcelldesign

![image](https://github.com/user-attachments/assets/ec21011e-cd72-43af-857b-dc43fcf9f064)

#### tech file

![image](https://github.com/user-attachments/assets/1cfe424e-d118-44e5-9fdb-a6fff86b2de2)

#### copying the sky130A.tech file

![image](https://github.com/user-attachments/assets/135f44aa-d471-404c-8b14-70a3e4dadf94)

#### After copying the file will be seen as given in the screenshot

![image](https://github.com/user-attachments/assets/1145bf1c-8364-4f53-9e7c-bd71c0987487)

</details>

<details>
  <summary>Design Library Cell using Magic Layout and ngspice characterization: Lab</summary>
  <br>
  
## Inverter in magic

![image](https://github.com/user-attachments/assets/3fa8b21b-038d-4ec2-85bb-d548212d552f)

#### press s & V to fit on screen properly

![image](https://github.com/user-attachments/assets/10f9f197-ca75-4fe5-a9f8-bd6b81944874)

#### what in tkcon tells highlighted portion, so here NMOS is identified

![image](https://github.com/user-attachments/assets/b7b14fb4-70f1-4425-9a84-d30a008dd39b)

#### PMOS is identified

![image](https://github.com/user-attachments/assets/20943225-513a-4192-8028-17edf13ffe91)

#### In magic to see whether two different parts of the circuit are connected press s two times

#### first time press: the area where the cursor is highlighted

![image](https://github.com/user-attachments/assets/c88e01f1-7878-40bd-a841-9332c12ed11b)


#### second time press:the area where it is connected gets highlighted

![image](https://github.com/user-attachments/assets/c03bb8c0-566a-4e1f-bc60-fb4d1ee97fbc)

#### extract on spice

![image](https://github.com/user-attachments/assets/3b3808b4-d487-4d7a-8a4f-bbc74295f80d)

#### spice file has been created

![image](https://github.com/user-attachments/assets/dbe87655-b6df-4ca8-a65e-d33016a3090e)

#### Let us see what is inside this spice file by giving the command vim sky130_inv.spice

![image](https://github.com/user-attachments/assets/db164868-3b01-41f4-88ed-980b77650c3b)

#### edited spice file

![image](https://github.com/user-attachments/assets/71d34498-ef4b-4dd8-8254-223e999ddc1d)

#### To simulate the spice file give the command ngspice sky130_inv.spice

![image](https://github.com/user-attachments/assets/9bb9f34a-1b7e-4509-a9c6-3af0160ff43f)

#### To see the plot give the command as plot y vs time a

![image](https://github.com/user-attachments/assets/f8e17bb9-d30d-4d99-aefe-8ea98f87f2f7)

#### To remove the spikes in the output waveform we will change the load capactice value to 2fF

![image](https://github.com/user-attachments/assets/8e896688-1e6b-48ec-907b-6c0d127f5a61)

## 20% Screenshots

![image](https://github.com/user-attachments/assets/66b776dd-f78d-487b-a15d-8895199c6607)

![image](https://github.com/user-attachments/assets/874689f3-07fa-4d4a-a991-97168bab0198)

## 80% screenshots

![image](https://github.com/user-attachments/assets/3cf3d08e-989e-45b1-b72a-7cb9a47e16eb)

![image](https://github.com/user-attachments/assets/b6f9e2f3-65e6-464d-a394-d66d55c989d1)

#### Rise time= 2.24608e-09 - 2.18196e-09=0.06412 nS

## Now let us calculate the propogation delay

## 50% screenshots

![image](https://github.com/user-attachments/assets/82afc187-6152-436e-856f-cd1c43850e18)

![image](https://github.com/user-attachments/assets/eb6f65af-2cfc-47e4-a476-6ee78ba92e53)

#### cell rise delay = 2.21183e-09 - 2.15108e-09 = 0.06075 nS

#### Problems in DRC

![image](https://github.com/user-attachments/assets/80db1b8f-04e9-4647-822f-cb97841d16f7)

![drc2](https://github.com/user-attachments/assets/54bfd2b3-ebc1-46ab-8f4d-321b6aa3f614)

![drc2magicrc](https://github.com/user-attachments/assets/c15139d4-6d52-4f4c-94a7-76f03afa9433)

![drc3](https://github.com/user-attachments/assets/dcfe3628-efde-4099-afeb-b18c0d6d602e)

![drc4](https://github.com/user-attachments/assets/c98fd132-e9cb-46f5-8d83-c1ec1832c3c6)

![drc5](https://github.com/user-attachments/assets/01e69edb-1a0f-46b8-be42-74310cdf0a2c)

![drc6](https://github.com/user-attachments/assets/16c92828-94ce-4c28-866c-a0b57516f21e)

![drc7](https://github.com/user-attachments/assets/cd878889-528d-425a-bcf5-ed7814f58143)

![drc8](https://github.com/user-attachments/assets/7a8df255-4e2d-4709-bbd5-0c6fc27cbe2e)

![drc9](https://github.com/user-attachments/assets/62b27f17-829d-47a3-80da-a3f613fbe106)

![drc10](https://github.com/user-attachments/assets/b30ab77c-dbc0-424c-aa3f-0c655801955b)

![drc11](https://github.com/user-attachments/assets/6ffd74e5-d202-439e-8bfd-f547ce0d2894)

![drc12](https://github.com/user-attachments/assets/78fd13db-2dff-4edd-be0c-3c0d57719b88)

![drc13](https://github.com/user-attachments/assets/adb65618-e748-4191-964a-b9f39be0a8c3)

![drc14](https://github.com/user-attachments/assets/8306a760-47cc-4ffb-96c1-cf02bfeeba20)

![drc15](https://github.com/user-attachments/assets/84129c87-ad3e-430c-add6-725e9c130b95)

![drc16](https://github.com/user-attachments/assets/e45491f4-adcb-45b7-990a-2900b1757a28)


# extracting lef file out of .mag file

#### less tracks.info: tracks are basicaaly used during routing stage

![image](https://github.com/user-attachments/assets/13a0078d-6b01-4e26-869f-3729d7f22291)

</details>


<details>
  <summary>Pre-layout timing analysis and importance of good clock tree: Lab</summary>
  <br>
  
#### Each of the tracks are placed at 0.46 along horizontal direction. Similarly for y direction 0.34

#### for every layer there is x and y direction

![image](https://github.com/user-attachments/assets/3cb49fbe-5f97-4cb0-8ef2-b0d2d37f77c6)

#### grid dimensions

![image](https://github.com/user-attachments/assets/356dd412-37cc-4c73-aaf8-4816bbfa5d25)

#### width of the standard cell must be odd multiples of xpitch

#### creating a port

#### select a particular region and then go to edit click on text to make the changes

![image](https://github.com/user-attachments/assets/ede1d061-b743-4fcd-9cfe-96a201fea458)

#### port class and port use

#### what will tell you to which layer it is attached, port name, signal etc

![image](https://github.com/user-attachments/assets/0bc83188-34e4-45d2-87ec-b9c7deb93532)

#### once this is done we are ready to extract the lef file

#### save the file as sky130_vsdinv.mag

![image](https://github.com/user-attachments/assets/82bffb63-b5a0-4307-b802-5f8fcfe475d9)

#### lef write

![image](https://github.com/user-attachments/assets/0023a960-8391-42eb-af79-6f4c4d6c134f)

#### type the following commands to open the lef file

![image](https://github.com/user-attachments/assets/87a68d3f-aa81-46b5-a163-efaaf38d01ec)

![image](https://github.com/user-attachments/assets/283da182-302c-4a5a-8eef-6d11ce9e7cdf)

#### plug this lef file into our picorv32a

![image](https://github.com/user-attachments/assets/b542a447-3dd5-4a7f-911d-020fd1442194)

#### copying lef file into src

![image](https://github.com/user-attachments/assets/7efa90b8-7327-406d-b3da-b31fcbd28ecc)

#### The lef file has been included

![image](https://github.com/user-attachments/assets/751a16b0-376d-4f93-bace-2b7b60dd1793)

#### less sky130_fd_sc_hd__typical.lib

![image](https://github.com/user-attachments/assets/115aa230-cb68-4132-bdc6-c81f7527868b)


![image](https://github.com/user-attachments/assets/0e052742-44fe-49ea-88e4-24245c1a185f)

#### src will be having lef file as well as library

![image](https://github.com/user-attachments/assets/29f3947c-a431-453f-ac29-7c04b5c11a6d)

![image](https://github.com/user-attachments/assets/b9b7a038-2700-429c-a33b-ec85b7b70e90)

#### now modify config.tcl

![image](https://github.com/user-attachments/assets/ff25f623-fdcd-4875-8b11-d0c1e7854481)



#### overwrite will take the new values defined in config.tcl

![image](https://github.com/user-attachments/assets/85ef28c4-798d-452b-8656-e5847cbb9235)

![image](https://github.com/user-attachments/assets/fc899c11-24f8-4c4b-ac3e-154425d5392d)

#### Additional steps

![image](https://github.com/user-attachments/assets/4f5cb375-cc59-4444-af07-3d83cf08b0ef)


#### mapping our custom vsd inverter 

![image](https://github.com/user-attachments/assets/177a2f1c-572d-428d-ba91-bcf72b67143d)

![image](https://github.com/user-attachments/assets/92118c9c-ef43-412e-b22b-85d3fb476b20)

#### Synthesis is successful. In the screenshot wns is maximum slack and tns is total negative slack

![image](https://github.com/user-attachments/assets/1671895d-e040-4686-af75-40cd09d51f84)

#### Commands to reduce slack

![image](https://github.com/user-attachments/assets/45ec2679-59c5-4d79-bcc3-b28a015488b1)

#### Now slack has been reduced

![image](https://github.com/user-attachments/assets/1c4d9e6e-b553-495c-9176-7657418ed76b)

#### run_floorplan

![image](https://github.com/user-attachments/assets/dab08b19-824e-4486-8e1d-ececdf035e97)

#### Since the flow is failed as shown in the above screenshot, run the following commands

```
* init_floorplan
* place_io
* tap_decap_or

```

![image](https://github.com/user-attachments/assets/906a335d-6260-455f-9a10-8ee6ce0f8335)

#### run_placement

![image](https://github.com/user-attachments/assets/23348c6a-9884-4993-877e-81841925c3f7)

#### load placement def in magic

![image](https://github.com/user-attachments/assets/d400ab23-0ace-4f69-ad55-077bccfe9e57)

#### placement def in magic

![image](https://github.com/user-attachments/assets/ea2ea4a1-a677-4cfe-8c97-d3a411ee34a7)

![image](https://github.com/user-attachments/assets/9345aa08-80d7-4500-93c7-4f384e7e7be3)

#### sky130_vsdinv

![image](https://github.com/user-attachments/assets/49248642-cd11-49d0-aa37-9f63a6275659)

#### search for sky130_vsdinv and then expand

![image](https://github.com/user-attachments/assets/20c8f094-cd0d-4ff5-9270-2187a7cf9f45)

#### pre_sta.conf

#### pre_sta.conf file

![image](https://github.com/user-attachments/assets/abd5f1ca-7df1-48da-b2e1-44d72b73d429)

#### my_base.sdc file

![image](https://github.com/user-attachments/assets/79d56dbf-858a-4913-9caa-c60b3c4114af)

#### execution of sta pre_sta.conf

![image](https://github.com/user-attachments/assets/a8d9f2eb-d66e-4142-8cfe-a91db467347f)

![image](https://github.com/user-attachments/assets/7cb31fd3-f797-4128-b747-ad17ddf068a4)


![image](https://github.com/user-attachments/assets/b65e6819-0f33-4fd6-a63b-d42586bd5d70)

#### reduce fanout and do the synthesis again

#### follow the commands given in screenshot

![image](https://github.com/user-attachments/assets/8621a0a5-2612-4c0e-b469-88f0936ab673)

![image](https://github.com/user-attachments/assets/3a39a252-0c73-4ff7-8aa7-c583ff2f2c16)

#### run the sta pre_sta.conf

![image](https://github.com/user-attachments/assets/fec2902f-884e-4a1a-a2e6-cdc01f0b328b)

![image](https://github.com/user-attachments/assets/24102bf8-4939-46fd-86dc-c067e0816a70)

#### pre_sta.conf: Configuration file on which we will be doing Prelayout timing analysis

![image](https://github.com/user-attachments/assets/2dcca01c-0f20-49cd-9391-4212663ffcf6)

#### Let us see the contents of this file 

![image](https://github.com/user-attachments/assets/88a8e65a-e2a4-4004-b176-a76897e83d95)

![image](https://github.com/user-attachments/assets/f3181649-8827-4797-841b-53e91a39d5b3)

#### Do sta pre_sta.conf

![image](https://github.com/user-attachments/assets/37fb086f-4292-4181-8ab1-e86c1a86fe13)


## Hold analysis come into picture after CTS. Let us check set up analysis

#### Optimize the fanout value

#### Let us see the fanout value

![image](https://github.com/user-attachments/assets/8c29ce40-67b9-490e-9fc2-9ce63cbdd6bd)

![image](https://github.com/user-attachments/assets/c9ad7e63-a864-4047-9627-315200009448)

#### Choose the optimum value of fanout value
#### set the fanout value to 4 and run the synthesis again

 ![image](https://github.com/user-attachments/assets/26691fb4-3d2f-4b63-ad01-e82c8539a052)

![image](https://github.com/user-attachments/assets/169b303b-c45b-4934-bd3f-3bf7b05f45b1)

#### Net having huge delay

![image](https://github.com/user-attachments/assets/9893474c-df45-478f-b71c-4f2e9a91a5f9)

#### Now run the following commands

![image](https://github.com/user-attachments/assets/11207a05-8f5a-49a6-8253-933dd4e1e3b0)

#### upsizing the cell reduces the delay

#### help write_verilog

![image](https://github.com/user-attachments/assets/b1ea00a4-9419-4f0d-9b0d-825a7e7c4f9f)

#### Now objective is to replace the synthesis file with modified one

![image](https://github.com/user-attachments/assets/5801a876-19c6-4a56-ba43-7ef2ded528a9)

#### This will over write the current verilog file

![image](https://github.com/user-attachments/assets/1efef009-60d5-4e83-9c95-0961401b3683)

#### The file has been modofied with 15/Sept/2024 earlier it was created on 11/Sept/2024

![image](https://github.com/user-attachments/assets/cab9844e-f3f0-44ed-96a7-57ad4bfc017e)

![orgate](https://github.com/user-attachments/assets/1da6e515-c153-49de-8cce-5004bd312da4)

![orgate2](https://github.com/user-attachments/assets/5e0a8bcb-302f-4405-8827-1947e686ccfa)

![slack](https://github.com/user-attachments/assets/2ffde198-9ad9-48c9-bf60-6e5c0bf30a00)

![customtimingreport](https://github.com/user-attachments/assets/1f91fd93-5115-4abf-93b2-fe8cc3d912fa)

![updatevariablessynthesis](https://github.com/user-attachments/assets/d8870f37-74a1-46f4-a114-097d9dd9b9ad)

![runfloorplan](https://github.com/user-attachments/assets/f7779e78-b671-4f42-a067-6e3449d320d1)

![tapdecap](https://github.com/user-attachments/assets/7f98096a-1e11-4213-91b0-64cbea0c979e)

![runplacement](https://github.com/user-attachments/assets/79b9b74e-260a-46df-83ef-798dfddb1077)

![cts](https://github.com/user-attachments/assets/ba866a37-807d-45e2-a771-4a6a96e43c5f)

![cts2](https://github.com/user-attachments/assets/8cdd89ea-ca45-4b90-b91a-28ddfbc3cc0b)

## openroad

![openroad](https://github.com/user-attachments/assets/899238af-b4d6-4d66-902a-f673acf6c62a)

![reportchecks](https://github.com/user-attachments/assets/e9fca8f7-90a4-4b15-b4d3-0c435a29f02f)


![reportchecks1](https://github.com/user-attachments/assets/2376c6e7-512f-4c91-950c-97ea777da95a)

![clkbuff](https://github.com/user-attachments/assets/7dd93e1e-9755-4ffc-bfc9-d7675b52e0b2)

![insertingclkbuf1](https://github.com/user-attachments/assets/db78ad3e-7e2d-46c0-a63a-06bfa9d35489)

![setuphold](https://github.com/user-attachments/assets/2b67e96d-7431-45db-8eff-9d472eed8ff7)

</details>

<details>
  <summary>Final steps for RTL2GDS using triton Route and openSTA: Lab</summary>
  <br>

## Power Distribution Network

![pdngen](https://github.com/user-attachments/assets/22901949-2a5d-49dc-a18d-44abd5775dfa)

![pdnsuccessful](https://github.com/user-attachments/assets/ac0f0572-b938-432b-a301-1368e20d3b35)

![pdndef](https://github.com/user-attachments/assets/2976c237-f3a9-45ae-b414-e72ffa037a8f)

![pdndef1](https://github.com/user-attachments/assets/4936a6a3-c1cf-4a92-8fa4-533db12f6a60)

![pdndef2](https://github.com/user-attachments/assets/cb1b55f4-11d0-4e5d-9a0b-1e2a857e473e)

![pdndef3](https://github.com/user-attachments/assets/d1e16d8b-3c45-4ada-b97f-a8138a679532)

![routing](https://github.com/user-attachments/assets/04d45a71-5a91-4def-a94b-9620a4aa6774)

![routing1](https://github.com/user-attachments/assets/bd1bc0cb-192f-4fe6-a09a-4c414f82df3e)

![routing2](https://github.com/user-attachments/assets/8ebfe671-adc4-4d05-aaca-5dbd5e87b9f8)

![routing3](https://github.com/user-attachments/assets/67378d71-088f-4e7e-ae3d-5f506cd2836f)

![routeddef](https://github.com/user-attachments/assets/3f582104-e31a-41b9-ac52-978d0236bea8)

![routeddef1](https://github.com/user-attachments/assets/c5042468-311e-479a-963e-631086e98164)

![routeddef2](https://github.com/user-attachments/assets/a248f818-a92a-4285-8078-6558a4bca7d9)

![laststep1](https://github.com/user-attachments/assets/db025b85-d39c-4a52-99bb-580175991869)

![laststep2](https://github.com/user-attachments/assets/006c37e0-5f48-40fe-9c1f-373d06d75118)

![laststep3](https://github.com/user-attachments/assets/7700637f-3e87-460f-9d91-19fd3ca1e4b7)

![laststep4](https://github.com/user-attachments/assets/d18bd42b-2043-479c-b0d4-b5162dde0893)

![laststep5](https://github.com/user-attachments/assets/d5d3d6b7-c074-4f5b-8337-89402354027b)


## Certificate

![image](https://github.com/user-attachments/assets/bb73341a-b682-4dc1-9b42-49db67726836)












Acknowledgements

Kunal Ghosh, Co-founder VSD Coporation Private Limited.

Nickson P Jose, Physical Design Engineer, Intel Corporation.

R. Timothy Edwards, Senior Vice President of Analog and Design, efabless Corporation.
</details>



