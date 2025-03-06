## Table for Worst Negative/Setup Slack (WNS) & Worst Hold Slack (WHS) for different available PVT corners from Prime Time Analysis, for our BabySoC Design :

![image](https://github.com/user-attachments/assets/644fc41f-7059-47ac-b8f2-8b129848b9f2)

| PVT_Corner   | WNS         | WHS       |
| ------------ | ----------- | --------- |
| ff_100C_1v65 | 3.163197    | \-0.21487 |
| ff_100C_1v95 | 4.52766     | \-0.2685  |
| ff_n40C_1v56 | 1.71135     | \-0.2122  |
| ff_n40C_1v65 | 2.693945    | \-0.23178 |
| ff_n40C_1v76 | 3.579041    | \-0.25714 |
| ff_n40C_1v95 | 4.593926    | \-0.28598 |
| ss_100C_1v40 | \-16.511486 | 0.711383  |
| ss_100C_1v60 | \-7.945134  | 0.342825  |
| ss_n40C_1v28 | \-56.932819 | 1.613348  |
| ss_n40C_1v35 | \-36.237518 | 1.081402  |
| ss_n40C_1v40 | \-27.168804 | 0.823482  |
| ss_n40C_1v44 | \-21.881821 | 0.652679  |
| ss_n40C_1v60 | \-9.959112  | 0.278781  |
| ss_n40C_1v76 | \-4.31766   | 0.039611  |
| tt_025C_1v80 | 1.226283    | \-0.14216 |
| tt_100C_1v80 | 1.321706    | \-0.12361 |

![image](https://github.com/user-attachments/assets/91989dfa-3e6e-46da-bc52-e8488d0d6f90)

![image](https://github.com/user-attachments/assets/66f05421-d5d4-4a60-b026-1cd6d7db2660)

![image](https://github.com/user-attachments/assets/f3caa7b6-1d99-4cde-a94e-160467d9ec62)

## Script to setup prime time ECO:

![image](https://github.com/user-attachments/assets/e2ac9e12-fe1b-4022-aae9-3d891556afb9)

![image](https://github.com/user-attachments/assets/9b4044fb-0bf9-48b7-adc0-3b20afb80be7)

## To fix setup violations: fix_eco_timing -type setup

![image](https://github.com/user-attachments/assets/de314d97-e4f8-42b8-8d4f-78024476bfc7)

## To fix hold violations: fix_eco_timing -type hold -methods insert_buffer -buffer_list {sky130_fd_sc_hd__buf_1 sky130_fd_sc_hd__buf_2 sky130_fd_sc_hd__buf_4 sky130_fd_sc_hd__buf_8}

![image](https://github.com/user-attachments/assets/cb371f1d-8ba2-4f8d-a6cf-f59a168a64c9)
![image](https://github.com/user-attachments/assets/ae6fbe9d-80d7-48c7-b6af-b573da87ffc9)

![image](https://github.com/user-attachments/assets/87630d17-21a4-495f-b825-52e2c5582bf4)

## Table for Worst Negative/Setup Slack (WNS) & Worst Hold Slack (WHS) for different available PVT corners from Prime Time Analysis, for our BabySoC Design :

| PVT_Corner   | WNS         | WHS        |
| ------------ | ----------- | ---------- |
| ff_100C_1v65 | 3.124938    | \-0.235642 |
| ff_100C_1v95 | 4.522051    | \-0.291165 |
| ff_n40C_1v56 | 1.436169    | \-0.193214 |
| ff_n40C_1v65 | 2.510405    | \-0.230101 |
| ff_n40C_1v76 | 3.476581    | \-0.261722 |
| ff_n40C_1v95 | 4.582528    | \-0.300085 |
| ss_100C_1v40 | \-12.455952 | 0.59104    |
| ss_100C_1v60 | \-5.715736  | 0.236287   |
| ss_n40C_1v28 | \-48.670876 | 1.840496   |
| ss_n40C_1v35 | \-31.053354 | 1.181901   |
| ss_n40C_1v40 | \-23.332808 | 0.867832   |
| ss_n40C_1v44 | \-18.90251  | 0.674178   |
| ss_n40C_1v60 | \-8.493254  | 0.244431   |
| ss_n40C_1v76 | \-3.560485  | 0.040591   |
| tt_025C_1v80 | 1.610215    | \-0.166896 |
| tt_100C_1v80 | 1.694567    | \-0.156524 |


![image](https://github.com/user-attachments/assets/614545e6-d5fe-4f27-948c-604d6ca14e97)


![image](https://github.com/user-attachments/assets/30034718-1662-43df-86b4-38f4b3706d1a)

