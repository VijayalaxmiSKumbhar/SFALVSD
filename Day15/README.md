# Good floorplan Vs bad floorplan and introduction to library cells

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







