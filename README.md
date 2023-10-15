# RISC-V
<p align="center">
<img width="550" alt="image" src="https://github.com/vandhana01/RISC-V/assets/142392052/da7f9740-ce99-4cae-88a1-3e8e1df4ef0d">
</p>

**RISC-V is a real and widely recognized open-standard instruction set architecture (ISA). RISC-V, pronounced "RISC-Five," stands for "Reduced Instruction Set Computing Five" and is designed to be a simple and modular ISA that is both open and free to use. It has gained significant traction in the technology industry and academia.**

- RISC-V has gained popularity for several reasons:
1. Open Standard and License-Free
2. Simplicity and Modularity
3. Academic and Industry Support
4. Innovation
5. Ecosystem
6. Community
   
## CONTENTS
# DAY 1
<details>
<summary> Digital Logic with TL-Verilog and Makerchip </summary>
<br>
	
[](https://github.com/RISC-V#links-for-easy-navigaton)
  
- [Combinational Logic in TL-Verilog using Makerchip](#combinational-logic-in-tl-verilog-using-makerchip)
- [Sequential Logic](#sequential-logic)
- [Pipelined Logic](#pipelined-logic)
- [Validity](#validity)

# Combinational Logic in TL-Verilog using Makerchip
- Combinational logic refers to a type of digital logic circuit in which the output is solely determined by the current input values, without considering any past states or inputs.
- There is no memory or feedback involved in combinational logic, which means that the output changes immediately in response to changes in the input.
## Logic Gates
- Logic gates are fundamental building blocks of digital circuits that perform logical operations on one or more binary inputs to produce a single binary output. They are used to process and manipulate binary data (0s and 1s) in various ways. 
- These logic gates can be combined in various ways to create more complex logic functions and circuits.
  
![image](https://github.com/vandhana01/RISC-V/assets/142392052/283589dc-f780-4f8e-8eae-f05dc2076008)

## Boolean Operation
- Boolean operations are fundamental operations in Boolean algebra
- Boolean operations, such as AND, OR, and NOT, are fundamental in binary logic. AND returns 1 when both inputs are 1, OR returns 1 if at least one input is 1, and NOT inverts the input. These operations underpin digital circuit design and computer logic.

![image](https://github.com/vandhana01/RISC-V/assets/142392052/91afdc68-ed2c-491a-973d-422b6715c071)

3. **Basic Mux Implementation**
- A digital logic circuit that selects one of several input data lines and forwards it to a single output line.
- The selection is based on a set of control signals.

![image](https://github.com/vandhana01/RISC-V/assets/142392052/2a2ca5db-5fa4-4020-92ed-830f8cd79e7e)

## Chaining Ternary Operator
- Chaining ternary operators in programming is a way to create more complex conditional expressions by nesting multiple ternary (conditional) operators within each other. 

![image](https://github.com/vandhana01/RISC-V/assets/142392052/076c3497-4dbe-4a0f-aac9-e2399c44f21a)


## Makerchip Platform 
- Makerchip is an online platform that provides a user-friendly interface for designing and simulating digital circuits using TL-Verilog.
  + Go to http://makerchip.com/
  + Click `IDE`
  + Open `Tutorials` then `Validity Tutorial`
  + Click `Load Pythogorean Example`
  + Split planes and move tabs.
  + Zoom/pan in Diagram with mouse wheel and drag.
  + Zoom waveform with `Zoom In` button.
  + Click `$bb_sq` in waveform to highlight in the diagram.

![image](https://github.com/vandhana01/RISC-V/assets/142392052/0a295d46-5945-4bcf-b16c-de0418ddae8f)


1. **Inverter**
+ Open `Examples`(under `Tutorials`).
+ Load `Makerchip Default Template`.
+ Make an inverter.
+ On line 16, in place of `//..` , type `$out = ! $in1;` (preserve 3-space indentation, no tabs).
+ Compile (`E` menu).

![image](https://github.com/vandhana01/RISC-V/assets/142392052/068ee05b-0cb0-46ac-b6ab-88b4354cb5af)

 - There was no need to declare $out and $in1 unlike verilog, and no need to assign $in1.
 - Random stimulus is generated and a warning is produced.

2. **OR**
+  On line 16, in place of `//..` , type
  ```v
  $out = $in1 | $in2;
  ```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/159e4176-34b2-4217-a771-c35ef42e80fa)

3. **Vectors**
+ Arithmetic operations operate on vectors as binary numbers.
+  On line 16, in place of `//..` , type

 ```v
  $out[4:0] = $in1[3:0] + $in2[3:0];
```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/96107845-b4b8-4a6a-b9ad-5ebcdd59561f)


4. **MUX**
+ ```v
  $out = $sel ? $in1 : $in2;
  ```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/338445d9-0c35-4a1b-8f24-91e143c7e046)

+ Modified the mux to operate on vectors.
   - ```v
     $out[7:0] = $sel ? $in1[7:0] : $in2[7:0];
     ```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/7eb4aa97-6171-4099-b933-ca5a574c7d40)


5. **Combinational Calculator**

<p align="center">
  <img width="308" alt="image" src="https://github.com/vandhana01/RISC-V/assets/142392052/1a8fc0c9-352c-42a4-b5ca-d6861fbc1adc">
</p>
<p align="center">
</p>


```v
$reset = *reset;
$val1[31:0] = $rand1[3:0];
$val2[31:0] = $rand2[3:0];
$sum[31:0] = $val1[31:0] + $val2[31:0];
$diff[31:0] = $val1[31:0] - $val2[31:0];
$prod[31:0] = $val1[31:0] * $val2[31:0];
$quot[31:0] = $val1[31:0] / $val2[31:0];
$out[31:0] = $op[1] ? ($op[0] ? $quot : $prod)
                    : ($op[0] ? $diff : $sum);
```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/9a675c81-13dd-45cc-84b7-2069081030ce)

# Sequential Logic
- Sequential logic, also known as clocked or state-based logic, is a fundamental concept in digital electronics and digital design.
- It refers to the type of digital logic in which the output depends not only on the current input but also on the past behavior of the system.

![image](https://github.com/vandhana01/RISC-V/assets/142392052/8e4e6028-d942-4613-b3c6-db29d24479cb)

- Combinational logic performs immediate data processing and decision-making, while sequential logic elements introduce memory and sequencing capabilities, making it possible to control the flow of data and manage system states.

<p align="center">
  <img width="300" alt="image" src="https://github.com/vandhana01/RISC-V/assets/142392052/48f4c6eb-0ca9-4a21-a80a-73938c89e992">
</p>
<p align="center">
</p>    

## Labs 
1. **Fibonacci Series-Reset**


<p align="center">
<img width="300" alt="image" src="https://github.com/vandhana01/RISC-V/assets/142392052/dac0b3e8-41b6-41d5-bda1-5c821270ec43">
</p>
<p align="center">
</p>

- ```v
  $num[31:0] = $reset ? 1 : (>>1$num + >>2$num);
  ```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/ca8d08e8-ff67-4686-bc20-1ce0922c284c)


2. **Counter**

<p align="center">
<img width="300" alt="image" src="https://github.com/vandhana01/RISC-V/assets/142392052/1558abb4-8d69-4d2f-8242-1dec30b02913">
</p>
<p align="center">
</p>

- ```v
     $cnt[31:0] = $reset ? 0 : (1 + >>1$cnt);
  ```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/0fad340b-865e-41fd-894a-79a492777ea4)


3. **Sequential Calculator**

<p align="center">
<img width="300" alt="image" src="https://github.com/vandhana01/RISC-V/assets/142392052/27efedaa-669a-47f2-8e3d-1eda8cb671ad">
</p>
<p align="center">
</p>

- ```v
   $reset = *reset;
   $val2[31:0] = $rand2[3:0]; 
   $val1[31:0] = >>1$out[31:0];
   $sum[31:0] = $val1[31:0] + $val2[31:0];
   $diff[31:0] = $val1[31:0] - $val2[31:0];
   $prod[31:0] = $val1[31:0] * $val2[31:0];
   $quot[31:0] = $val1[31:0] / $val2[31:0];
   $out[31:0] = $reset ? 32'b0 :
                ($op[1] ? ($op[0] ? $quot : $prod)
                        : ($op[0]? $diff : $sum));
  ```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/e75c3b06-a5c6-4a7e-bbde-dd7eaaa23145)

# Pipelined Logic


# Validity

</details>

# DAY 2
<details>
<summary> Basic RISC-V CPU Microarchitecture </summary>
<br>
	
[](https://github.com/RISC-V#links-for-easy-navigaton)

+ [Introduction](#introduction)
+ [Fetch and Decode](#fetch-and-decode)
+ [RISC-V Control Logic](#risc-v-control-logic)

</details>

# DAY 3
<details>
<summary> Complete Pipelined RISC-V CPU Micro-architecture </summary>
<br>
	
[](https://github.com/RISC-V#links-for-easy-navigaton)

+ [Pipelining the CPU](#pipelining-the-cpu)
+ [Solutions to Pipeline Hazards](#solutions-to-pipeline-hazards)
+ [Load/Store Instructions and Completing RISC-V CPU](#load/store-instructions-and-completing-risc-v-cpu)

</details>


