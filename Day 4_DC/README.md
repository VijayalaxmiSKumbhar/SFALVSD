# Optimizations

<details>
<summary>Optimizations Combinational Opt </summary>
<br>

## Optimization Goals

![image](https://github.com/user-attachments/assets/a8135796-1f45-4329-bc6d-37f2554d8085)

## Combinational Logic Optimisation

![image](https://github.com/user-attachments/assets/28991cd8-3449-4930-aed5-4969281bdfd5)


#### Constant Propagation Example

![image](https://github.com/user-attachments/assets/6da28658-835c-439c-8978-1183678a96e6)

#### Boolean Logic Optimisation

![image](https://github.com/user-attachments/assets/bdd5c08a-1f42-469a-9f12-d081c6bcdcd6)

#### Resource Sharing (Very Important)

![image](https://github.com/user-attachments/assets/bafde63c-5c60-41c0-87d6-a49f8ca1a979)

#### Logic Sharing: Look for common logic across multiple expressions and does logic sharing (Very Important)

![image](https://github.com/user-attachments/assets/6ff72061-aee8-4f19-a05f-d7147bbfcfa7)

#### Balanced Vs Preferential Implementation

![image](https://github.com/user-attachments/assets/5c818d0a-a33a-4fa8-ab92-fe1db0c69edc)

</details>

<details>
<summary>Sequential Optimizations </summary>
<br>

## Sequential Logic Optimisations

![image](https://github.com/user-attachments/assets/74069174-b6ce-4640-af78-935cd3e3a5af)

#### Case-I (Sequential constant)

![image](https://github.com/user-attachments/assets/8ebdaca2-f613-4150-9990-26b568ebe76c)

#### Case-II (Sequential constant)

![image](https://github.com/user-attachments/assets/74ee4723-aa13-4432-b2fb-d7db5ba1da32)

#### case-III (Not a Sequential constant)

* As the circuit is retained as it is, it will not be optimized.

![image](https://github.com/user-attachments/assets/efe3d221-8f84-4361-a81b-5bb2f1278d6e)

#### Case-IV (Not a sequential constant)

![image](https://github.com/user-attachments/assets/444c9df8-e8fb-4b44-a691-8150eec73718)

#### Example of sequential optimization with sequential constant and constant propogation

![image](https://github.com/user-attachments/assets/61ecad4f-bbda-48ba-bbce-2250525abbf6)

#### Optimization of Unloaded Outputs

![image](https://github.com/user-attachments/assets/68ff42ec-28d0-44b6-9357-46a24948adf4)

#### Controlling Sequential Optimizations in DC

![image](https://github.com/user-attachments/assets/f2da94c2-689a-426e-9486-b0aa34bea781)


</details>

<details>
<summary>Lab 16: Part 1 Combinational_optimizations </summary>
<br>


</details>

<details>
<summary>Lab 16: Part 2 resource sharing optimizations </summary>
<br>


</details>

<details>
<summary>Lab 17: Sequential optimizations </summary>
<br>


</details>

<details>
<summary> Special optimizations </summary>
<br>

#### Example for illustration

![image](https://github.com/user-attachments/assets/76a8a5c7-d584-41f2-8d00-246d239e1d95)

#### Let us see how to improve the frequency of above circuit

* The solution to improvise the frequency is retiming.
* By reducing the critical path delay frequency can be improved.

![image](https://github.com/user-attachments/assets/1d1de245-e699-4ed0-b4fc-1bb30331f31b)

* The total criticalpath delay of 48 ns is divided into 3 parts and frequency is improved. Earlier it was 20 MHz, after register retiming frequency is increased to 50 MHz.

![image](https://github.com/user-attachments/assets/06f9f8db-e965-4f57-9164-0da8f6334545)

#### Boundary Optimization

![image](https://github.com/user-attachments/assets/219d5346-188b-4b07-90a3-879b606aaed5)

* Switch to control the boundary oprimization is
![image](https://github.com/user-attachments/assets/cdea923b-d34a-4b69-b32c-44fb31d72f1c)

#### Multi-cycle Paths

![image](https://github.com/user-attachments/assets/93645bc3-99a7-41ea-b73f-3de29878282d)



</details>

<details>
<summary>How Paths are timed MCP?</summary>
<br>


</details>

<details>
<summary>Lab 18: Boundary optimizations </summary>
<br>


</details>

<details>
<summary>Lab 19: Register Retiming </summary>
<br>


</details>

<details>
<summary>Lab 20: Isolating output ports </summary>
<br>


</details>

<details>
<summary>Lab 21: MultiCycle Path </summary>
<br>


</details>

