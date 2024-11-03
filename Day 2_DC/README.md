# Basics of STA (Static Timing Analysis)

<details>
<summary>Introduction to STA </summary>
<br>

##### Max Delay Constraint
![image](https://github.com/user-attachments/assets/8aa430b2-ce66-4d64-9ed0-eb3a897e0372)

##### Min Delay Constraint

![image](https://github.com/user-attachments/assets/a15699c2-a3b9-420d-8195-69c3aa66cfc5)
![image](https://github.com/user-attachments/assets/1d050675-25e9-42d5-8bb3-ef61b85962dd)

##### Why Delay: Water Bucket Analogy
###### Example 1
![image](https://github.com/user-attachments/assets/f037b92f-3b0f-427e-b35e-8eafe105b42f)

+ Delay is a function of Inflow
+ Inflow of water ----> Inflow of current
+ Therefore Faster current source is having less delay

###### Example 2
Delay = function (load capacitance)

![image](https://github.com/user-attachments/assets/b7844bee-5d1f-4e62-af7d-5270da7296b9)

#### Is delay of cell is constatnt?

###### Delay of gate = function (input transition, output load)

![image](https://github.com/user-attachments/assets/f7db544a-5136-42b7-a651-195aff60e360)

### Timing Arcs

#### Combinational Cell

+ Delay information from every input pin to every output pin which it can control is present in timing arcs
+ Example
![image](https://github.com/user-attachments/assets/0918f0f6-9d08-4c3a-b5b0-e71a6b485a74)

#### Sequential Cell [D flip-flop, D latch]

![image](https://github.com/user-attachments/assets/2476ba4f-85bb-45bf-9a55-b4fa435cbed5)

![image](https://github.com/user-attachments/assets/9780917c-2140-4326-ae93-3ebc5e54675b)

![image](https://github.com/user-attachments/assets/2951cb01-67ca-49c6-8e0d-9b24cd9e20f3)

</details>

<details>
<summary>What are Constraints </summary>
<br>

#### What are timing paths and how it affects design?

###### Example
![image](https://github.com/user-attachments/assets/562cc8c4-3298-408c-9b63-7433c5b74097)

###### Start and End points of timing paths

![image](https://github.com/user-attachments/assets/b78223ce-93cb-44ae-a385-79c638b52fef)

##### Timing Paths Summary

![image](https://github.com/user-attachments/assets/e4d68547-4f3e-4d92-8ea3-8735dc7582af)


#### Constrainig the Design- Why Constraints?

##### Example 1
![image](https://github.com/user-attachments/assets/2308f304-3aa5-45f3-82e7-ff566530c558)

###### Example 2

![image](https://github.com/user-attachments/assets/d42e3127-eece-41f8-a625-e3aa6d1eaa52)


</details>

<details>
<summary>IO Constraints </summary>
<br>

##### Is IO Delay Modelling Sufficient?

![image](https://github.com/user-attachments/assets/d6399d90-606d-41f3-a195-fc4f21ba9b49)

![image](https://github.com/user-attachments/assets/38425de3-8995-4315-96ab-78a8a089e121)

+ Note: 70:30 rule that is 70% (External Delay) and 30% (Internal Delay)

### Summary
![image](https://github.com/user-attachments/assets/8dfd992f-f574-406f-9dcc-478ce064b410)


</details>

<details>
<summary>Lab 5: Timing dot libs </summary>
<br>


</details>


<details>
<summary>Lab 6: Exploring dot libs part 1 </summary>
<br>


</details>


<details>
<summary>Lab 7: Exploring dot libs part 2 </summary>
<br>


</details>

