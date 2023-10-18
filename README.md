# RISC-V Based Myth
## DISCLAIMER : This repo mainly focus on DAY 3,4 and 5

<img width="1100" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/2e4c7a2d-b188-403d-9482-a8efac7ceada">

# Introduction
**VLSI physical design for ASIC** is the process of converting a conceptual chip design into a physical layout suitable for manufacturing. It encompasses tasks such as arranging components, optimizing connections, managing power and clock distribution, addressing manufacturing challenges, and ensuring design compliance. This meticulous process guarantees a functional and manufacturable integrated circuit tailored to specific applications.

# System requirments
- Ubuntu 20+
- RAM : 6Gb (minimum)
- Disk space : 100Gb (minimum)
  
# Installation
https://github.com/kunalg123/riscv_workshop_collaterals/blob/master/run.sh
- Download the run.sh
- Open terminal
- cd Downloads
- ./run.sh

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
     
# CONTENTS
# Day 1
<details>
<summary> Introduction to RISCV ISA and GNU Compiler Toolchain </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

**Introduction to RISCV ISA and GNU Compiler Toolchain**
+ Introduction to RISC-V Basic Keywords
  - [Introduction](#introduction)
  - [From Apps to Hardware](#from-apps-to-hardware)
  - [Detail Description of Course Content](#detail-description-of-course-content)

+ Labwork for RISC-V Toolchain
  - [C Program](#c-program)
  - [RISCV GCC Compiler and Dissemble](#riscv-gcc-compiler-and-dissemble)
  - [Spike Simulation and Debug](#spike-simulation-and-debug)

+ Integer Number Representation  
  - [64-bit Unsigned Numbers](#64-bit-unsigned-numbers)
  - [64-bit Signed Numbers](#64-bit-signed-numbers)
  - [Lab For Signed and Unsigned Numbers](#lab-for-signed-and-unsigned-numbers)


# DAY 1
 
# Introduction to RISc-V Basic Keywords
## Introduction
RISC-V Architecture -> RTL -> Layout

## From Apps to Hardware
## Flow
+ Application Software 
+ System Software
  - Operating System
  - Complier
  - Assembler
+ Hardware
<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/eb287951-3c15-4b47-b5fe-1f471c84fe14">

## Detail Description of Course Content
- Pseudo Instructions
- Base integer Instructions RV641
- Multiply extension RV64M
- Single and double precision floating point extension RV64F & RV64D
- Application binary interface (ABI)
- Memory allocation and stack pointer

# Labwork for RISC-V Toolchain
## C Program
- Text editor used : leafpad
- To install leafpad in ubuntu : `sudo snap install leafpad`

## C program for sum from 1 to N
`leafpad sum1ton.c` : creates a text file called sum1ton.c
``` c
#include<stdio.h>

int main(){
	int i, sum=0, n=10;
	for (i=1;i<=n; ++i) {
	sum +=i;
	}
	printf("Sum of numbers from 1 to %d is %d \n",n,sum);
	return 0;
}
```
Compile using gcc complier
`gcc sum1ton.c`
`./a.out`

<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/bcec2cbb-9a78-441d-84d6-f341d2645825">

## RISCV GCC Compiler and Dissemble
Compile using RISC-V gcc complier
- using -O1 optimisation
```
riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
riscv64-unknown-elf-objdump -d sum1ton.o
```
Number of instructions = 15
<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/242d83e5-c7c4-47cf-aa04-2c3db3373bd2">
- using -Ofast optimisation
```
riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o sum1ton.o sum1ton.c
riscv64-unknown-elf-objdump -d sum1ton.o
```
Number of instructions = 12
<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/b772a095-3460-4396-aba4-5c86296b4c34">

`riscv64-unknown-elf-objdump -d sum1ton.o` : gives the disassembled (Assembly Language Programming )ALP code

## Spike Simulation and Debug
`spike pk sum1ton.o` : To Verify the simulations using RISC-V complier

<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/cdf11383-ad59-47e8-8007-abc80cd560ce">

`spike -d pk sum1ton.c ` :To debug

<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/99241fdb-3988-4a42-b9f5-853648bd595d">

# Integer Number Representation 
+ 8-bits -> byte, 4-bytes -> word, 2-words or 8-bytes -> doubleword
## 64-bit Unsigned Numbers
- A 64-bit unsigned number can represent non-negative integer values using 64 bits, with no sign bit to indicate whether the number is positive or negative.
- Range: [0, (2^n)-1 ]

## 64-bit Signed Numbers
- A 64-bit signed number can represent both positive and negative integer values using 64 bits. The first bit, often referred to as the "sign bit," indicates whether the number is positive or negative.
- Range : Positive : [0 , 2^(n-1)-1] Negative : [-1 to 2^(n-1)]

## Lab For Signed and Unsigned Numbers
+ C program that shows the maximum and minimum values of 64bit unsigned numbers
```c
#include <stdio.h>
#include <math.h>

int main(){
	unsigned long long int max = (unsigned long long int) (pow(2,64) -1);
	unsigned long long int min = (unsigned long long int) (pow(2,64) *(-1));
	printf("lowest number represented by unsigned 64-bit integer is %llu\n",min);
	printf("highest number represented by unsigned 64-bit integer is %llu\n",max);
	return 0;
}
```

<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f0c93d75-c326-42ec-b3de-e1290c23b192">

+ C program that shows the maximum and minimum values of 64bit signed numbers
  
```c
#include <stdio.h>
#include <math.h>

int main(){
	long long int max = (long long int) (pow(2,63) -1);
	long long int min = (long long int) (pow(2,63) *(-1));
	printf("lowest number represented by signed 64-bit integer is %lld\n",min);
	printf("highest number represented by signed 64-bit integer is %lld\n",max);
	return 0;
}
```

<img width="502" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7fef9481-74ef-4fcb-8462-eb0a7dc40cd9">


- To acess DAY 1 CODEs : https://github.com/vandhana01/pes_asic_class/tree/main/DAY1

</details>

# DAY 2
<details>
<summary> Introduction to ABI and Basic Verification Flow </summary>
<br>

[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigation)


## DAY 2 
**Introduction to ABI and Basic Verification Flow**
+ Application Binary Interface
  - [Introduction to ABI](#introduction-to-abi)
  - [Memory Allocation for Double Words](#memory-allocation-for-double-words)
  - [Load, add and store instructions](#load-add-and-store-instructions)
  - [32-Registers and their ABI Names](#32-registers-and-their-abi-names)

+ Labwork using ABI Function Calls
  - [Algorithm for C Program using ASM](#algorithm-for-c-program-using-asm)
  - [Review ASM Function Calls](#review-asm-function-calls)
  - [Simulate C Program using Function Call](#simulate-c-program-using-function-call)

# Application Binary Interface

## Introduction to ABI
+ Base Binary Instructions
  - Base integer instructions refer to the fundamental set of instructions that operate on integer data in a computer's instruction set architecture (ISA)
  - These are arithmetic, logical, Comparison, Data Movement, Control Flow performing operations
+ Application Binary Interface (ABI)
  - An Application Binary Interface (ABI) serves as a crucial bridge between the software and hardware components of a computer system.
  - ABIs enable software components to seamlessly communicate and collaborate, even across diverse programming languages, compilers, and hardware architectures.
<img width="600" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/e25eba01-5478-4113-b402-e96d3da1ba9d"> 

## Memory Allocation for Double Words
- RISC-V has **32** registers
  - 32 bits for RV32
  - 64 bits for RV64

- Memory addressing system
  - **Little-Endian** (Risc-V belongs to little-endian)
  - **Big-Endian**
  
<img width="650" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/76ab920b-3abd-4085-b1b7-96e40af4945b"> 

## Load, add and store instructions
Load, Add, and Store instructions are often used to manipulate data within a computer's memory and registers.
1. **Load Instructions:**
Load instructions are used to transfer data from memory to registers. They allow you to fetch data from a specified memory address and place it into a register for further processing.

Example `ld x6, 8(x5)`

In this Example
- `ld` is the load double-word instruction.
- `x6` is the destination register.
- `8(x5)` is the memory address pointed to by register `x5` (base address + offset).
2. **Store Instructions:**
Store instructions are used to write data from registers into memory.They store values from registers into memory addresses

Example `sd x8, 8(x9)`

In this Example
- `sd` is the store double-word instruction.
- `x8` is the source register.
- `8(x9)` is the memory address pointed to by register `x9` (base address + offset).
3. Add Instructions:
  Add instructions are used to perform addition operations on registers. They add the values of two source registers and store the result in a destination register.

Example `add x9, x10, x11`

In this Example
- `add` is the add instruction.
- `x9` is the destination register.
- `x10` and `x11` are the source registers.

<img width="750" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/9df00634-f508-4c5f-9e55-86d4bf03be9f"> 

## 32-Registers and their ABI Names
The ABI names provide meaningful and consistent labels to the registers, which simplifies understanding their roles in function calls, data manipulation, and other operations.

<img width="350" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/320a926d-6867-4803-bb13-4abcecbe1467"> 

# Labwork using ABI Function Calls
## Algorithm for C Program using ASM
- This allows you to take advantage of assembly language's low-level control and optimizations while still benefiting from C's higher-level constructs.
- When you call an assembly function from your C code, the C calling convention is followed, including pushing arguments onto the stack or passing them in registers as required.
- The program executes the assembly function, following the assembly instructions you've provided.

## Review ASM Function Calls
- C code and assembly code are written in separate files
- Declaring assembly functions with appropriate signatures that match the calling conventions of your platform in assembly file
 
**C Program**
  
  `1to9custom.c`
  
  ``` c
  #include <stdio.h>
  
  extern int load(int x, int y);
  
  int main()
  {
    int result = 0;
    int count = 9;
    result = load(0x0, count+1);
    printf("Sum of numbers from 1 to 9 is %d\n", result);
  }
  ```
**Asseembly File**

`load.s`

``` s
.section .text
.global load
.type load, @function

load:

add a4, a0, zero
add a2, a0, a1
add a3, a0, zero

loop:

add a4, a3, a4
addi a3, a3, 1
blt a3, a2, loop
add a0, a4, zero
ret
```
## Simulate C Program using Function Call

Compile and execute the files 

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/87bb8d8a-1ce6-4631-8fcf-65116d2e32f7"> 

Disassemble the code 

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/038da5c5-6402-4e90-825c-9c8548353a95">


## Lab to Run C-Program on RISCV-CPU

```
git clone https://github.com/kunalg123/riscv_workshop_collaterals.git
```

```
cd riscv_workshop_collaterals
```

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/2904e4cc-c126-4e06-9b12-4a04ca31ab88">


```
ls -ltr
```

```
cd labs
```

```
ls -ltr
```

```
chmod 777 rv32im.sh
```

```
./rv32im.sh
```

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/3c9bb5d2-0247-436e-a666-c45148e03752">

- To access DAY 2 CODEs : https://github.com/vandhana01/pes_asic_class/tree/main/DAY2

# RTL Design using verilog with SKY130 technology 
<details>
<summary> Introduction to Verilog RTL design and Synthesis</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)



<details>
<summary> Introduction to open-source simulator iverilog </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## Introduction to open-source simulator iverilog
**Introduction to iverilog design test bench**

- **Simulator**
  + Simulators create virtual models of systems, enabling analysis and testing of behaviors without real-world implementation
  + Simulators is the tool used for simulating the design
  + The simulator runs the model using the provided inputs. It calculates the system's behavior over time and produces output data upon change in input (if no change to the input, no change to the output)
  + **iverilog** is the tool used here
     + Icarus Verilog (iverilog) is an open-source simulator for hardware description languages like Verilog, enabling design, simulation, and testing of digital circuits
     + It's used to model and validate digital systems before physical implementation

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/a1fe7cb8-41e6-423c-a986-b4f2fd1308f6">

- **Design**
  + Design is the actual verilog code or set of verilog codes which has the intended functionality to meet with the required specifications
  
- **TestBench**
  + It involves creating a set of test cases and stimuli to apply to the design and then comparing the design's outputs with expected results.
  + Test benches are written using hardware description languages like Verilog or VHDL
  + This verification process is crucial for building reliable and bug-free digital systems
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/3c3fd20b-e3bb-4c9f-b3b7-41593c3356ea">  

</details>


<details>
<summary> Labs using iverilog and gtkwave </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)


## Labs using iverilog and gtkwave

**Icarus Verilog** simulates the design and generates simulation output files, and **GTKWave** then allows you to visually inspect and analyze the simulation results in waveform format

- [Introduction to lab (Lab1)](#introduction-to-lab-lab1)
- [iverilog GTKwave Part-1 (Lab2)](#iverilog-gtkwave-part-1-lab2)
- [iverilog GTKwave Part-2 (Lab2)](#iverilog-gtkwave-part-2-lab2)

## Introduction to lab (Lab1)
- Environment setup !!!
+ create a directory ` mkdir vsd `
+ change directory ` cd vsd `
+ Git clonning ` git clone https://github.com/kunalg123/sky130RTLDesignAndSynthesisWorkshop.git`
   + `sky130RTLDesignAndSynthesisWorkshop` folder will be created

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/5eeabad8-63c7-4a6a-aaa9-5b1bd4b10139"> 

## iverilog GTKwave Part-1 (Lab2)
+ ` cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files
    + loads verilog source files and associated testbench files into iverilog simulator
    + verilog_files : this folder contains all design files
+ `iverilog good_mux.v tb_good_mux.v` loads mux into the simulator
+ output file `a.out` will be created
+ Execute a.out `./a.out` to dump the vcd file (output of simulator)
+ To load vcd file into simulator ` gtkwave tb_good_mux.vcd`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/c6d25681-de8d-449c-a270-bfd454f15e4a"> 

## iverilog GTKwave Part-2 (Lab2)
`gvim tb_good_mux.v -o good_mux.v` to view the files


**good_mux.v**

``` v
module good_mux (input i0 , input i1 , input sel , output reg y);
always @ (*)
begin
	if(sel)
		y <= i1;
	else 
		y <= i0;
end
endmodule
```
**tb_good_mux.v**

``` v
timescale 1ns / 1ps
module tb_good_mux;
	// Inputs
	reg i0,i1,sel;
	// Outputs
	wire y;

        // Instantiate the Unit Under Test (UUT)
	good_mux uut (
		.sel(sel),
		.i0(i0),
		.i1(i1),
		.y(y)
	);

	initial begin
	$dumpfile("tb_good_mux.vcd");
	$dumpvars(0,tb_good_mux);
	// Initialize Inputs
	sel = 0;
	i0 = 0;
	i1 = 0;
	#300 $finish;
	end

always #75 sel = ~sel;
always #10 i0 = ~i0;
always #55 i1 = ~i1;
endmodule
```

    

</details>


<details>
<summary> Introduction to Yosys and Logic synthesis </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)


## Introduction to Yosys and Logic synthesis

- [Introduction to Yosys](#introduction-to-yosys)
- [Introduction to Logic synthesis)](#introduction-to-logic-synthesis)


## Introduction to Yosys
- **Synthesizer**
   + Synthesizeris a tool used for converting the RTL to netlist
   + **Yosys** is the synthesizer used in the course
      + Yosys is an open-source synthesis tool that translates hardware description language (HDL) code into gate-level netlists, optimizing designs for efficient hardware implementation.
- **Netlist**
  + Netlist is the representation of the design in the form of standard cells in the .lib
  + Design and .lib files are fed to the synthesizer to get a netlist file
 
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/56f8289c-4737-481e-9bb3-2b86f38a6902"> 

+ Commands used to perform synthesis:
  - To read the design :  `read_verilog` 
  - To read the .lib file : `read_liberty` 
  - To write out the netlist file : `write_verilog` 
 
- Verify the synthesis
 
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/63bd1f15-ec42-47e3-b2d6-e76ee3ebe6d9"> 

   - The output on the simulator must be same as the output observed during RTL simulation.
   - Same RTL testbench can be used because the primary inputs and primary outputs remain same between the RTL design and synthesised netlist.

## Introduction to Logic synthesis

- **RTL design**
  + Behavioral representation of the required specification
  + RTL (Register-Transfer Level) forms a bridge between behavioral descriptions and gate-level implementation.

- **Synthesis**
  + RTL to gate level translation
  + The design is coverted into dates and the connections are made between the gates
  + This is given out as a file called netlist
    
<img width="350" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/dd91792a-9e4b-4c6e-ac62-55cd19486580)"> 

- **.lib**
   + Collection of logical modules
   + Includes basic logic gates like AND, OR, NOT, etc
   + Different flavors of same gate , **WHY ??**
       + These variations are designed to accommodate specific design requirements, process technologies, and performance goals
       + Clock frquency should be high, Hence time period of the clock should be  as low as possible
         
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/5030de94-2f5a-4ea4-952d-2d3ffb04c9f5"> 

- What is maximum clock rate ? tclk ?
	+ Propogation delay of Flop A
	+ Propogational delay of combinational circuit
	+ Time before clock edge, setup time
- So we need cells that work fast to make Tcombi samall
- Are faster cells sufficient ??
   + NO
- Why do we need slow cells ?
  
<img width="150" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/2c4cf856-de06-4d1d-96e3-c7f072b448f2"> 

   + To ensure that there are no "HOLD" issues at DFF_B, we need slow cells
   + Hence we need cells that work fast to meet the required performance and we need cells that work slow to meet HOLD
   **Hence the collection forms the .lib!!!**
     
**Faster cells vs Slower cells**
- Load in degital circuit -> Capacitance
- Faster the charging/discharging of capacitance -> Lesser the cell delay
    + To charge/discharge the capacitance fast, we need transistors capable of sourcing more current ( Wide Transistors)
    + Wider transistors -> Low Delay -> More area and power as well
    + Narrow transistors -> More Delay -> Less area and power
-Faster cells come at the penalty of area and power

**Selction of cells**
Synthesizer should be guided to select the flavour of cells that is optimum for the implementation of logic circuit. Guidance offered -> "Constaints"


<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/b4119c84-db5f-4751-acfd-72c81fe4b3d6">

 </details>

 
<details>
<summary> Labs using Yosys and Sky130 PDKs</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
## Labs using Yosys and Sky130 PDKs 
-[Yosys good mux (Lab3)](#yosys-good-mux-lab3)

 The SkyWater Technology Foundry's **SKY130 Process Design Kit (PDK)** is a collection of files, data, and models that enable the design and layout of integrated circuits using the SkyWater 130 nm technology node. PDKs provide designers with the necessary tools and information to create, simulate, and verify custom and digital designs that can be manufactured using the specific technology offered by the foundry. 
 
## Yosys good mux (Lab3)
- To invoke the Yosys : `yosys`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/eaa3287e-b5b6-4597-b29a-d8651c4839f6">

- To read the library : ` read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
- To read the design : `read_verilog good_mux.v`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/3953ff06-69ed-48b0-a966-39ff5fa2b560">

- To synthesis the mosule : `synth -top good_mux`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/6309e60b-1c8c-467b-ad52-e550bc305daf">

- To generate the netlist : `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/c948cd72-9e64-4bd9-a102-4f98112eab3b">

- To see the logic it has realised `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/30e2335a-7f17-4eef-b203-804640eb62d5">

- To write the netlist : 'write_verilog good_mux_netlist.v`
- ` !gvim good_mux_netlist.v`
-  To view a simplified code : ` write_verilog -noattr good_mux_netlist.v`
-  `!gvim good_mux_netlist.v`
  
</details>
</details>  

## part 4
<details>
<summary> Timing libs, hierarchical vs flat synthesis and efficient flop coding styles</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

<details>
<summary> Introduction to timing.libs </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## Introduction to timing.libs (Lab4)
**Introduction to dot Lib**
+ To view the contents in the .lib
`gvim ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`


<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/bcdd2944-4944-499b-99c8-9400c084a9b2">


- To have a pleasant color : `:syn off` (syntax off)
    - NOTE: Don't edit this file
- **sky130** : Name of the library
- **tt**     : Typical process
- **025C**   : Temperature variation
- **P V T**  : Operating conditions (Process Voltage Temperature)
    - Together determines how the silicon works
- **1v80**   : Voltage levels variation

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f49ac9c0-7677-40e3-9456-46bd9c75c756">

- Displays the units of parameters
- Contains area and power consumpution
- .lib is a Bucket of all the standard cells
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/267ed2ae-d9e9-49dc-9039-7c02215dfb99">


- To enable line number `:se nu`
- To view all the cells `:g//`
- To view any instance `:/instance`
- Can compare and analyse the parameters

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/47cabe0a-eee7-40e9-9357-b1871e47fa46">


 </details>     


<details>
<summary> Hierarchical vs Flat synthesis </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
## Hierarchical vs Flat synthesis (Lab5)

## Hierarchical Synthesis
**Hierarchical synthesis involves breaking down a complex design into smaller modules for separate synthesis and integration. This approach enhances modularity, enables parallel development, and simplifies verification, making it ideal for large designs.**

- File used : 'multiple_modules.v`
- To view : `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- and `gvim multiple_modules.v`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/d6816017-c0f4-48e9-8c92-1bf8c99ddeb6">


- It contains 2 submodules : `sub_module1` -> AND gate and `sub_module2`->OR gate
- `mutiple_module` instantiates them as `u1` and `u2` respectively
  
+  Frist Launch Yosys     : `yosys`
+  Read the library file  : `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+  Read the verilog file  : `read_verilog multiple_modules.v`
+  To set it as top module: `synth -top multiple_modules`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/cc297050-dc6e-4469-90d8-3ac600194370">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/a9495611-658d-489f-bf39-b9e6546a524e">


+  `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ To view the netlist    :`show multiple_modules`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/8740c0be-8439-4b75-9c4f-a81cc0a8a26c">

+ `sub_module1` and `sub_module2` are shown instead of AND gate and OR gate.
+ To view : `write_verilog -noattr multiple_modules_hier.v`
+ `!gvim multiple_modules_hier.v`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/fd066807-4c8b-4bc6-95fb-6b8976185214">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/e1c470a9-0747-4c7d-a4ca-47f405231908">



## Flat Synthesis
**Flat synthesis treats the entire design as a single unit, synthesizing it as one entity. While simpler for smaller designs, it can become unwieldy for larger projects, leading to longer synthesis times and reduced reusability of modules.**

+  Launch  : `yosys`
+  Read the library file :   `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+  Read the verilog file : ` read_verilog multiple_modules.v`
+  To set it as top module: `synth -top multiple_modules` 
+  `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
+ `flatten` to write out a flattened netlist
+ `show` to view the netlist

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7dffcc47-5ed6-40d6-b48e-08d156f95f34">

+ `write_verilog -noattr multiple_modules_flat.v`
+ `!gvim multiple_modules_flat.v`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/1e708f33-455c-40bf-a7d0-710e6ac6b174">

**Why sub module level synthesis**
- U seful when we have multiple instances of same module
- Divide and Conquer
- Helpful when circuits are massive
-`synth -top module_name` controls which module to synthesis
 </details>     


<details>
<summary>Various Flop Coding Styles and optimization</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
   
## Various Flop Coding Styles and optimization
- [Why flops and Flop coding styles](#why-flops-and-flop-coding-styles)
- [Lab flop synthesis simulations](#lab-flop-synthesis-simulations)
- [Interesting Optimisations](#interesting-optimisations)
  
## Why flops and Flop coding styles
**What are flops??**
- Flip-flops, often referred to as "flops," are fundamental building blocks in digital circuits
- Flip-flops are fundamental to sequential logic circuits and play a vital role in memory storage and synchronization of signals with clock edges.
-  Flip-flops are used to store state information in sequential circuits, enabling the creation of memory elements, registers, and other essential components in digital designs.
 
**Why flops??**
- In a combinational circuit, when a input is given to a flop, output changes after the propagation delay
- Output glitches occur due to this propagation delay
- **Glitch** occurs when the intermediate signals reach the next set of gates while they are still transitioning. This can lead to temporary, unwanted changes in the output until all paths stabilize and reach a consistent logic state
- More the number of combinational circuit, more the glitches (output will never settle down)
- To avoid this we want a element to store that value, that is **flop**
- Basically Flops are like storage elements present between the combinational circuits
- output of the flop will change only at the edge of the clock ,therefore even if the input is changing output will be stable
- Hence aviods the transfer of gitch to the subsequent combinational circuits
- Controls pin called **Reset** and **set** are used to initialize the flop
- They can be synchronous or asynchronous

## D Flip-Flop with Asynchronous and synchronous Reset

- asynchronous->irrespective of clock
- synchronous->with respecte to clock
- when both asynchronous and synchronous reset is present, should take care of race
  
  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `gvim dff_asyncres_syncres.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/b61d78a3-36c0-44d5-83ce-1fc0460c0259">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_asyncres_syncres.v tb_dff_asyncres_syncres.v`
   - `./a.out`
   - `gtkwave tb_dff_asyncres_syncres.vcd`
     
- OUTPUT

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/9af4f145-6e3c-41c1-be66-91236c6726c7">


## Lab flop synthesis simulations

## D Flip-Flop with Asynchronous Reset
- When the asynchronous reset input is asserted (set to 1), the flip-flop's output is immediately forced to 0, regardless of the clock signal's state.
- When the clock rises from 0 to 1, the flip-flop samples the value at its Data (D) input and updates its stored state accordingly.

  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `gvim dff_asyncres.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/8040e97b-d2f0-4074-b749-b7ccb41b1e96">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_asyncres.v tb_dff_asyncres.v`
   - `./a.out`
   - `gtkwave tb_dff_asyncres.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7f27ad28-faf1-4cee-8e52-0c969dc71aa6">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_asyncres.v`
   - `synth -top dff_asyncres`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/febe071c-9064-4fa9-8b30-791b20d73ab8">


## D Flip_Flop with Asynchronous Set
- When the clock rises from 0 to 1, the flip-flop samples the value at its Data (D) input and updates its stored state accordingly.
- When the asynchronous set input (S) is asserted (set to 1), the flip-flop's output (Q) is immediately forced to 1, regardless of the clock signal's state.

  - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
  - `gvim dff_async_set.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/46903c4d-d823-4728-addd-b529b8e5d204">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_async_set.v tb_dff_async_set.v`
   - `./a.out`
   - `gtkwave tb_dff_async_set.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/a6b5ce19-5000-4ba3-9417-2daffcb40554">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_async_set.v`
   - `synth -top dff_async_set`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/ceb182bc-e9b3-4117-a70f-79d3473b0edc">

## D Flip-Flop with Synchronous Reset 
- When the clock rises from 0 to 1, the flip-flop samples the value at its Data (D) input and updates its stored state accordingly.
- The synchronous reset input (R) allows you to reset the flip-flop's stored state when the clock rises. If the reset input (R) is asserted (set to 1) simultaneously with a rising clock edge, the flip-flop's output (Q) is forced to the reset state (typically 0).

- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim dff_syncres.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/81efabae-3eff-4e71-b1ca-c4e11f69d096">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_syncres.v tb_dff_syncres.v`
   - `./a.out`
   - `gtkwave tb_dff_syncres.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/eb72d454-0ed6-44de-aa3b-afb742966611">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_syncres.v`
   - `synth -top dff_syncres`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7f07809f-825b-4185-864d-75c9ed1de71e">


## Interesting Optimisations
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim mult_2.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/b5417497-2bdc-4727-a27d-a7e4f45fc286">

- Here input **a** is 3-bit , output **y** is 4-bit and relation is **y=2*a**
- observation
	- A Number **a** multiplied by 2 is a number appended by 0 **{a,0}**
 	- No extra hardware is required for multiplying a number with 2 or powers of 2
    	- ground the LSB , interconnect other bits in order

- Lets see what we get when we synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog mult_2.v`
   - `synth -top mul2`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/fbd7454f-fee3-462d-9c73-5c21df1a9aa1">

- **netlist**
    - `write_verilog -noattr mul2_netlist.v`
    - `!gvim mul2_netlist.v`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/bbcc5f98-1592-467e-b251-8748a8386b04">

- Another special case
   - Here input **a** is 3-bit , output **y** is 6-bit and relation is **y=9*a**
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim mult_8.v`
   
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/a595cde8-95c0-4563-ba6e-07559c2120ba">

- Lets see what we get when we synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog mult_8.v`
   - `synth -top mult8`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/218caf9a-2e48-4039-9ad3-524cae3f1efd">

- **netlist**
    - `write_verilog -noattr mul8_netlist.v`
    - `!gvim mult8_netlist.v`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/fd91fb9e-3da0-4fb4-987d-af40b1ccda6f">
   
</details> 
</details>   

## Part 5
<details>
<summary> Combinational and sequential optmizations </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)


<details>
<summary> Introduction to optimisations</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
## Introduction to Logic optimisations

**Combinational Logic optimisations**
- **Combinational logic??** refers to a type of digital logic design where the output is solely determined by the current input values, and there are no memory elements involved. Examples of combinational circuits include adders, multiplexers, demultiplexers, comparators, and more.
- Squeezing the logic to get the most optimised design (Area and power savings)

**Optimisation techniques**
- **Constant Propogation** (Direct Optimisation)
	- dentify signals that are derived from constant inputs or other signals with constant values.
	- Replace these signals with their constant values throughout the logic.
	- Update downstream logic accordingly, simplifying the circuit.
	- This optimization eliminates unnecessary logic and reduces gate count, improving circuit efficiency and performance.
- **Boolean logic optimization** (using K-map or Quine McKluskey)
	- Apply Boolean algebra rules to simplify logic expressions, using techniques like factorization, distribution, and absorption.
   	-  Use Karnaugh Maps (K-Maps) to identify patterns and group terms for simplification.
        - Eliminate redundant terms and simplify expressions further.
	- This optimization reduces the number of gates, improves circuit performance, and enhances overall efficiency.

**Sequential Logic Optimizations**
- **Sequential Logic??** is a fundamental concept in digital circuit design that involves elements capable of storing information (memory elements like flip-flops and latches) and producing outputs based not only on current inputs but also on past inputs and internal states.It forms the basis for many digital devices, including microcontrollers, processors, and communication systems.
- Designers must carefully evaluate the trade-offs between speed, power, and complexity to create effective and optimized sequential logic designs.

**Optimisation techniques**
- Basic
   - **Sequential constant propagation**
	- Sequential constant propagation is an optimization technique that involves identifying and replacing intermediate signals within a sequential circuit with their constant values. This technique aims to eliminate unnecessary calculations and logic, reducing the complexity of the circuit.
- Advanced
   - **State optimization**
     	- State optimization focuses on reducing the number of states in a finite state machine (FSM) or reducing the complexity of state transitions. By eliminating redundant or unreachable states and simplifying the transition logic, designers can create more efficient and streamlined state machines.
   - **Retiming**
     	- Retiming is a technique used to balance the delay of a sequential circuit by moving flip-flops within the design. By strategically relocating flip-flops along the critical path, designers can minimize propagation delays and improve the overall performance of the circuit.
   - **Sequential logic cloning** (Floor Plan Aware Synthesis)
	- Sequential logic cloning involves duplicating a portion of a sequential circuit to optimize its performance. This technique is particularly useful for critical paths where excessive delays are present. By replicating a section of the circuit and introducing additional registers, designers can reduce the delay along the path.
   
</details> 
<details>
<summary> Combinational logic optimizations </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)
## Combinational logic optimizations (Lab6)
- [opt_check](#opt_check)
- [opt_check2](#opt_check2)
- [opt_check3](#opt_check3)
- [opt_check4](#opt_check4)
- [multiple_module_opt](#multiple_module_opt)
  
## opt_check
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim opt_check.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/43a315f8-0d96-4b05-adb1-a1e5c980fed8">

- synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog opt_check.v`
   - `synth -top opt_check`
   - `opt_clean -purge` : For constant Propogation optimisation
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/0e1358d8-9657-4de5-b107-4db795b9a916">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/6b2571dc-e221-4981-b0ae-5770489b55e5">

## opt_check2
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim opt_check2.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/b2592f4e-ef1a-4568-8303-5e7e5aa62700">

- synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog opt_check2.v`
   - `synth -top opt_check2`
   - `opt_clean -purge` 
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/5f309b47-7665-4508-b927-4080c6190296">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f5c93b1d-3003-4516-a4f6-6ccf9f841d26">


## opt_check3
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim opt_check3.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f62eeed3-3728-4307-9219-06ff4e7ad148">

- synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog opt_check3.v`
   - `synth -top opt_check3`
   - `opt_clean -purge`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/af41291a-96e0-41a7-ac5b-a9f9957af8a2">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/b0fc25c4-ad70-4f55-a896-9bc94c20423b">


## opt_check4
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim opt_check4.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/4b08507e-1687-42a8-9b30-7e47c5860378">

- synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog opt_check4.v`
   - `synth -top opt_check4`
   - `opt_clean -purge`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/310a5ca1-f592-44a5-a150-e8b078bdf693">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/9c7a8966-12b6-49e0-86d5-8201bfc09d5e">



## multiple_module_opt
- To look at the RTL code
	- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
	- `gvim multiple_module_opt.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/db948604-3af1-4ad8-a6e0-c80574baf752">

- synthesis
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog multiple_module_opt.v`
   - `synth -top multiple_module_opt`
   - `opt_clean -purge`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show multiple_module_opt `
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/e4ace4b9-44a4-437f-8734-6df63eeb2b4f">

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7b4426ed-6f89-4f51-a9b5-f746866829d4">


</details> 
<details>
<summary> Sequential logic optimizations </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## Sequential logic optimizations (Lab7)
- [dff_const1](#dff_const1)
- [dff_const2](#dff_const2)
- [dff_const3](#dff_const3)
- [dff_const4](#dff_const4)
- [dff_const5](#dff_const5)

## dff_const1
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim dff_const1.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/d280b206-0bd3-407e-8398-fe74eceeba76">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_const1.v tb_dff_const1.v`
   - `./a.out`
   - `gtkwave tb_dff_const1.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/a599e34b-db12-4228-ba8f-2c5f155a0e8d">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_const1.v`
   - `synth -top dff_const1`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/410e4642-01a4-4dd3-8f19-c0c8a8b46ba0">

## dff_const2
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim dff_const2.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/2484b140-e115-4a04-994f-484ab86072b8">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_const2.v tb_dff_const2.v`
   - `./a.out`
   - `gtkwave tb_dff_const2.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/4c5f73bc-d98b-4126-8997-10fee42fcc2c">


- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_const2.v`
   - `synth -top dff_const2`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/3cf456ac-56f4-4462-8c64-495df3147e80">


## dff_const3
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim dff_const3.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/aa085a87-d270-407c-995b-abee10ff93a0">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_const3.v tb_dff_const3.v`
   - `./a.out`
   - `gtkwave tb_dff_const3.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/7ddc0cd0-fdfb-4b24-a1f6-d684f66eac7f">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_const3.v`
   - `synth -top dff_const3`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/499f4930-bf45-4930-b81e-6471172cdbef">

## dff_const4
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim dff_const4.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f93252e5-5f97-46ae-b9fb-0291ecb463b2">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_const4.v tb_dff_const4.v`
   - `./a.out`
   - `gtkwave tb_dff_const4.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/953f2daf-4a80-4dcd-974d-6da7183106ba">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_const4.v`
   - `synth -top dff_const4`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/71d67c55-a813-45c5-b2a9-a0ba32aeba91">

## dff_const5
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim dff_const5.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/74c6a764-2115-4bd8-8cb9-6bbe0cfe5063">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog dff_const5.v tb_dff_const5.v`
   - `./a.out`
   - `gtkwave tb_dff_const5.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f21e94a6-72eb-4cb7-b893-59fa99829cfb">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog dff_const5.v`
   - `synth -top dff_const5`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/cdadc96a-5a53-4b12-946d-51a40634c924">

</details> 
<details>
<summary>  Sequential optimizations for unused outputs  </summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## Sequential optimizations for unused outputs 
- [counter_opt](#counter_opt)
- [counter_opt2](#counter_opt2)

## counter_opt
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim counter_opt.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/304f06b8-ebff-4ef8-8cc4-042c2430a350">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog counter_opt.v`
   - `synth -top counter_opt`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="750" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/ef4f0f85-9e00-4e25-a43c-5dc609c8a5cb">

## counter_opt2
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim counter_opt2.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/d788dc1d-8c0c-4c86-878c-009c870022f7">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog counter_opt2.v`
   - `synth -top counter_opt`
   - `dfflibmap -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib `
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="750" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/3562b15a-b362-4977-ae86-71d293ab2684">


</details> 
</details>  

## Part 6
<details>
<summary> GLS, blocking vs non-blocking and Synthesis-Simulation mismatch</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

<details>
<summary>GLS, synthesis-Simulation mismatch and Blocking/Non-blocking statements</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

- [GLS concepts and flow using iverilog](#GLS-concepts-and-flow-using-iverilog)
- [Synthesis-Simulation mismatch](#Synthesis-Simulation-mismatch)
- [Blocking and Non-blocking statements in verilog](#Blocking-and-Non-blocking-statements-in-verilog)
- [Caveats with blocking statements](#Caveats-with-blocking-statements)
  
## GLS concepts and flow using iverilog
**Gate level simulation (GLS)**
- **What is GLS??**
	- It is a verification process in digital design where the gate-level netlist of a design is simulated to ensure that it behaves as expected after the synthesis process. In gate-level simulation, the design is represented using actual gate-level components (AND gates, OR gates, flip-flops, etc.) and their interconnections.
	- Run the testbench with netlist as the design under test
	- Netlist is logically same as RTL code (same TB will allign with the design)
- **Why GLS??**
	- To verify the logical correctness of design under synthesis
	- Ensuring the timing of the design is met
	- It helps designers catch post-synthesis errors, timing issues, and other potential design flaws.
- **GLS using iverilog**

<img width="750" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/cbeb0cf9-fb14-454b-ae9d-83b7c03a9e36">

## Synthesis-Simulation mismatch

Discrepancies or inconsistencies that can arise between the behavior of a digital design as simulated and its behavior after synthesis.
- **Reasons**
	- Missing sensitivity List
	- Blocking vs Non-blocking assignments
	- Non standard Verilog coding
   
Addressing and minimizing synthesis-simulation mismatch is crucial for ensuring the correctness and reliability of digital designs. Careful validation, consistency in constraints, and understanding the intricacies of the synthesis process are key steps in mitigating this type of issue.
     
## Blocking and Non-blocking statements in verilog
Blocking and non-blocking statements are two types of assignment statements used in Verilog, a hardware description language. They serve different purposes in describing how assignments are executed within a procedural block of code, such as an 'always' or 'initial' block.

- **Blocking Assignment**

    - Blocking assignments in Verilog use the `=` operator for assignment.
    - A blocking assignment is executed sequentially, meaning the next statement will not be executed until the current assignment is complete.
    - The value on the right side of the assignment is immediately assigned to the left-hand side, and the process waits for the assignment to complete before moving on.
    - It represents a procedural programming-style behavior.

```v
a = 1;    // Assign the value 1 to 'a'
b = a;    // Use the current value of 'a' to assign to 'b'
c = b;    // Use the current value of 'b' to assign to 'c'
```

- **Non-blocking Assignment**

    - Non-blocking assignments in Verilog use the <= operator for assignment.
    - A non-blocking assignment schedules the assignment to take place at the end of the current time step without affecting the order of execution of subsequent statements.
    - It is commonly used to model concurrent behavior, particularly in sequential logic circuits, by allowing multiple assignments to occur simultaneously within the same time step.
    - It represents hardware modeling and concurrent behavior more accurately.

```v
always @(posedge clk) begin
  a <= b;  // Schedule the assignment of 'b' to 'a'
  b <= c;  // Schedule the assignment of 'c' to 'b'
  c <= d;  // Schedule the assignment of 'd' to 'c'
end
```

## Caveats with blocking statements

Using blocking statements (`=`) in Verilog can introduce certain caveats and potential issues in your designs. Here are some important considerations to keep in mind:

1. **Sequential Execution:** Blocking assignments are executed sequentially, meaning that each assignment must complete before the next one starts. This can lead to unintended delays and might not accurately capture concurrent behavior.

2. **Race Conditions:** When multiple blocking assignments are used to update the same variable within a procedural block, the final value of the variable is determined by the order of execution. This can lead to race conditions where simulation results might not match hardware behavior.

3. **Combinational Logic:** In combinational logic circuits, using only blocking assignments might not accurately model concurrent behavior. Combinational logic should ideally use non-blocking assignments (`<=`) to capture concurrent signal updates within the same time step.

4. **Sensitivity Lists:** Procedural blocks using blocking assignments should have accurate sensitivity lists to ensure that the code executes when the appropriate events occur. Incorrect sensitivity lists can lead to unexpected simulation behavior.

5. **Simulation vs. Hardware Behavior:** The sequential execution of blocking assignments in simulation might not accurately represent the concurrent behavior of hardware circuits.

6. **Nested Blocking Blocks:** Nesting blocking assignment blocks within each other can lead to unintended delays and can complicate the design.

7. **Timing Analysis:** If used improperly, blocking assignments in synchronous logic (such as setting flip-flop inputs) can lead to incorrect timing analysis results.

8. **State Machines:** When describing state machines, using only blocking assignments might lead to incorrect state transitions if transitions are not carefully managed.

**Best Practices to Mitigate Caveats:**

1. **Use Non-Blocking Assignments:** For modeling concurrent behavior in sequential logic circuits, use non-blocking assignments (`<=`) to avoid race conditions and capture the expected hardware behavior.

2. **Reserve Blocking for Sequential Logic:** Use blocking assignments (`=`) for simple sequential operations where one operation must complete before the next one starts.

3. **Minimize Multiple Blocking Assignments:** Avoid multiple blocking assignments to the same variable within a single procedural block to prevent race conditions.

4. **Sensitivity List Integrity:** Ensure that sensitivity lists in your procedural blocks are accurate and capture the necessary triggers for execution.

5. **Separate Logic Types:** Clearly separate sequential logic (clocked processes) from combinational logic (non-blocking assignments) to maintain accurate modeling.

6. **Avoid Nesting Blocks:** Minimize nesting of blocking assignment blocks to avoid unintended timing effects.

7. **Consult Simulation Warnings:** Pay attention to simulation tool warnings or messages related to the usage of blocking assignments. They can offer insights into potential issues.

By understanding these caveats and applying best practices, you can use blocking assignments effectively while mitigating potential pitfalls and ensuring accurate modeling of your Verilog designs.

</details>     

<details>
<summary>Labs on GLS and Synthesis-Simulation Mismatch</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

- [Ternary operator mux](#Ternary-operator-mux)
- [Bad_mux](#Bad-mux)

## Ternary operator mux
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim ternary_operator_mux.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/1778a50e-e9bd-4ba0-a62c-f6529f501149">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog ternary_operator_mux.v tb_ternary_operator_mux.v`
   - `./a.out`
   - `gtkwave tb_ternary_operator_mux.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/75ddfb8c-c2ec-4f47-916b-6fca39a57df6">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog ternary_operator_mux.v`
   - `synth -top ternary_operator_mux`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/d788d4e2-217e-45a0-999c-2508e8e2f529">

- **GLS to Gate-Level Simulation**

    - `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v ternary_operator_mux_net.v tb_ternary_operator_mux.v`
    - `./a.out`
    - `gtkwave tb_ternary_operator_mux.vcd`
      
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/5bc21f41-7d4b-4328-9a6d-addaf16c5225">
      
## Bad_mux
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim bad_mux.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/ba70bbba-4674-40db-841a-f49f0a0f59cf">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog bad_mux.v tb_bad_mux.v`
   - `./a.out`
   - `gtkwave tb_bad_mux.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/55334f40-31fe-477d-9837-750f4ac90426">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog bad_mux.v`
   - `synth -top bad_mux`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/0148e431-ffbf-4950-a7a5-18c31b770119">

- **GLS to Gate-Level Simulation**

    - `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v bad_mux.v tb_bad_mux.v`
    - `./a.out`
    - `gtkwave tb_bad_mux.vcd`
      
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/218556de-de81-4927-82aa-bfa449e393e7">

</details> 

<details>
<summary>Labs on synth-sim mismatch for blocking statement</summary>
<br>
	
[](https://github.com/vandhana01/pes_asic_class#links-for-easy-navigaton)

## blocking_caveat
- `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
- `gvim blocking_caveat.v`
  
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/59c74996-fdac-4908-8cde-9d8e19c50dfa">

- **Simulation**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `iverilog blocking_caveat.v tb_blocking_caveat.v`
   - `./a.out`
   - `gtkwave tb_blocking_caveat.vcd`
     
- OUTPUT
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/9b4484ae-49ae-400c-bc2a-ab7d20efff33">

- **Synthesis**
- CODE
   - `cd vsd/sky130RTLDesignAndSynthesisWorkshop/verilog_files`
   - `yosys`
   - `read_liberty -lib ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `read_verilog blocking_caveat.v`
   - `synth -top blocking_caveat`
   - `abc -liberty ../lib/sky130_fd_sc_hd__tt_025C_1v80.lib`
   - `show`

<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/8881c6be-5275-4922-b2e6-1a0ee64e93b0">

- **GLS to Gate-Level Simulation**

    - `iverilog ../my_lib/verilog_model/primitives.v ../my_lib/verilog_model/sky130_fd_sc_hd.v blocking_caveat.v tb_blocking_caveat.v`
    - `./a.out`
    - `gtkwave tb_blocking_caveat.vcd`
      
<img width="550" alt="image" src="https://github.com/vandhana01/pes_asic_class/assets/142392052/f3c28fca-c64b-4ced-96e3-f9d081789505">


</details>   
</details>   
  
</details>                    


# DAY 3
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
- It involves breaking down a complex operation into a series of stages, with each stage executed in parallel. The result is improved throughput, as new data can enter the pipeline before the previous data exits.
  
![image](https://github.com/vandhana01/RISC-V/assets/142392052/0c7d9eac-37a3-4da8-bdbf-1a8caa0bc5cd)

- TL Verilog gives us the ability to model this in what we called as timing abstract representation.
  
![image](https://github.com/vandhana01/RISC-V/assets/142392052/24f5d2e1-2165-465e-a910-cdb9e27b05a9)

- **system verilog vs TL-verilog**
- SystemVerilog is a comprehensive and mature language used for both design and verification in the semiconductor industry.
- TL-Verilog, on the other hand, is a more recent language that simplifies digital design by providing a high-level abstraction and is well-suited for designing high-performance accelerators and dataflow-style designs.

![image](https://github.com/vandhana01/RISC-V/assets/142392052/898f9d69-f613-4eef-b456-228532d7d329)

- **Retiming**

![image](https://github.com/vandhana01/RISC-V/assets/142392052/a96eb72b-20eb-4971-947e-46cffe2dc37b)

- Retiming in SystemVerilog is very bug-prone!!!
1. Without Pipeline
   
![image](https://github.com/vandhana01/RISC-V/assets/142392052/6d265660-d568-417f-84b0-7b309f47d4d4)

2. With Pipeline

![image](https://github.com/vandhana01/RISC-V/assets/142392052/a3655aca-182c-488b-8d3f-ba99a660ca05)

_ **Identifiers and Types**

![image](https://github.com/vandhana01/RISC-V/assets/142392052/f40d9b84-6297-458b-89ee-2f413d46eb7e)

## Labs
- Example
![image](https://github.com/vandhana01/RISC-V/assets/142392052/16f1f346-9571-4889-a600-0959a6083f2a)

- **Counter and Calculator in pipeline**
- Put Counter and Calculator in stage @1 in pipeline

![image](https://github.com/vandhana01/RISC-V/assets/142392052/48964ff9-bd31-4192-a65b-8cdd99a0586b)

- The $reset = *reset expression should be moved under the pipeline and pipestage as well

```v
|calc
      @0
         $reset = *reset;
      @1
         $val2[31:0] = $rand2[3:0];
         $val1[31:0] = (>>1$out[31:0]);
         $sum[31:0] = $val1[31:0] + $val2[31:0];
         $diff[31:0] = $val1[31:0] - $val2[31:0];
         $prod[31:0] = $val1[31:0] * $val2[31:0];
         $quot[31:0] = $val1[31:0] / $val2[31:0];
         $out[31:0] = $reset ? 32'b0 :
                      ($op[1] ? ($op[0] ? $quot : $prod)
                              : ($op[0]? $diff : $sum));
         $cnt[31:0] = $reset ? 0 : (1 + >>1$cnt);
```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/0a9ff7be-def7-46dc-825a-53b0d6b69276)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/bce00593-28e8-41ae-9e88-0fe53a8bc762)

- **2-Cycle Calculator**
- At high frequency, we might need to calculate every other cycle.
1. Change alignment of $out (to calculate every other cycle).
2. Change counter to single-bit (to indicate every other cycle).
3. Connect $valid (to clear alternate outputs).
4. Retime mux to @2 (to ease timing; no functional change).
5. Verify behavior in waveform. 

![image](https://github.com/vandhana01/RISC-V/assets/142392052/dd3e26ca-94a4-4c01-827d-65baa2b1ca37)

```v
   |calc 
      @0
         $reset = *reset;
      @1  
         $val1[31:0] = (>>2$out[31:0]);
         $val2[31:0] = $rand2[3:0];
         $sum[31:0] = $val1[31:0] + $val2[31:0];
         $diff[31:0] = $val1[31:0] - $val2[31:0];
         $prod[31:0] = $val1[31:0] * $val2[31:0];
         $quot[31:0] = $val1[31:0] / $val2[31:0];
         $cnt[0] = $reset ? 0 : (1 + >>1$cnt);
      @2
         $valid[0] = $cnt;
         $rst = ~$valid[0] || $reset;
         $out[31:0] = $rst ? 32'b0 :
                      ($op[1] ? ($op[0] ? $quot : $prod)
                              : ($op[0]? $diff : $sum));
   
```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/0e186445-4f86-4163-b789-45e74b608780)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/fcfd3bbe-0fa0-4cb7-bd08-4680ebc22d74)

# Validity
- Validity provides:
  - Easier debug
  - Cleaner design
  - Better error checking
  - Automated clock gating
- **CLOCK GATING**
- Motivation:
  - Clock signals are distributed to EVERY flip-flop.
  - Clocks toggle twice per cycle.
  - This consumes power.
- Clock gating avoids toggling clock signals.
- TL-Verilog can produce fine-grained gating (or enables).

![image](https://github.com/vandhana01/RISC-V/assets/142392052/534d1f0e-6194-425f-9559-52de4c345d17)

## Labs
1. **Distance accumulator**

```v
|calc
      @1
         $reset = *reset;
      ?$valid
         @1
            $aa_sq[31:0] = $aa[3:0] ** 2;
            $bb_sq[31:0] = $bb[3:0] ** 2;
         @2
            $cc_sq[31:0] = $aa_sq + $bb_sq;
         @3
            $cc[31:0] = sqrt($cc_sq);
      @4
         $tot_dist[63:0] = 
                   $reset ? '0 :
                   $valid ? >>1$tot_dist + $cc :
                            >>1$tot_dist;
```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/e430b637-57c9-4a7d-b3f7-8f51571aa585)

2. **2-Cycle Calculator with Validity** 

```v
  |calc
      @0
         $reset = *reset;
      @1
         $valid = $reset ? 1'b0 : >>1$valid + 1'b1;
         $val2[31:0] = $rand2[3:0];
         $val1[31:0] = >>2$out;
         $reset_or_valid = $valid || $reset;
      ?$reset_or_valid
         @1
            $sum[31:0] = $val1[31:0] + $val2[31:0];
            $diff[31:0] = $val1[31:0] - $val2[31:0];
            $prod[31:0] = $val1[31:0] * $val2[31:0];
            $quot[31:0] = $val1[31:0] / $val2[31:0];
         @2 
            $out[31:0] = $reset ? 32'b0 : 
                        ($op[1:0] == 2'b00) ? $sum :
                        ($op[1:0] == 2'b01) ? $diff :
                        ($op[1:0] == 2'b10) ? $prod : $quot;
```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/b743f93d-d1fa-4657-9fc3-5dac49407f27)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/898c7c6a-9023-4c8a-ac0d-4628f545113c)

3. **Calculator with Single-Value Memory**
- Calculators support “mem” and “recall”, to remember and recall a value

```v
   |calc
      @0
         $reset = *reset;
      @1
         $valid = $reset ? 1'b0 : >>1$valid + 1'b1;
         $val2[31:0] = $rand2[3:0];
         $val1[31:0] = >>2$out;
         $reset_or_valid = $valid || $reset;
      ?$reset_or_valid
         @1
            $sum[31:0] = $val1[31:0] + $val2[31:0];
            $diff[31:0] = $val1[31:0] - $val2[31:0];
            $prod[31:0] = $val1[31:0] * $val2[31:0];
            $quot[31:0] = $val1[31:0] / $val2[31:0];
         @2 
            $mem[31:0] = $reset ? 32'b0 : 
                         ($op[2:0] == 3'b101) ? $val1 :
                                              >>2$mem;
            $out[31:0] = $reset ? 32'b0 : 
                        ($op[2:0] == 3'b000) ? $sum :
                        ($op[2:0] == 3'b001) ? $diff :
                        ($op[2:0] == 3'b010) ? $prod : 
                        ($op[2:0] == 3'b011) ? $quot : 
                        ($op[2:0] == 3'b100) ? >>2$mem : >>2$out;

```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/c4f367ec-3742-40c4-8431-c49e05779222)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/b6ae65e8-adc7-4604-b2c7-939b8f2e8223)


</details>

# DAY 4
<details>
<summary> Basic RISC-V CPU Microarchitecture </summary>
<br>
	
[](https://github.com/RISC-V#links-for-easy-navigaton)

+ [Introduction to simple RISC-V micro-architecture](#introduction-to-simple-RISC-V-micro-architecture)
+ [Fetch and Decode](#fetch-and-decode)
+ [RISC-V Control Logic](#risc-v-control-logic)

# Introduction to simple RISC-V micro-architecture

![image](https://github.com/vandhana01/RISC-V/assets/142392052/f9764b63-7970-4814-aa14-e282988bb63f)

- A single-cycle RISC-V CPU is a simplified implementation of a RISC-V (Reduced Instruction Set Computing) processor where each instruction is executed in a single clock cycle.
1. **Instruction Fetch (IF)**: In the first stage, the CPU fetches the instruction from memory using the program counter (PC) and increments the PC to point to the next instruction. The instruction is loaded into the instruction register (IR).

2. **Instruction Decode (ID)**: During this stage, the CPU decodes the instruction in the IR. It identifies the operation to be performed, the source registers, and the destination register. It also performs register file reads.

3. **Execute (EX)**: In this stage, the actual execution of the instruction occurs. For ALU (Arithmetic Logic Unit) operations, this is where the ALU performs the calculations. For memory operations, such as loads and stores, the memory access is performed.

4. **Memory Access (MEM)**: In this stage, the CPU interacts with memory. If the instruction is a load or store, data is read from or written to memory. If the instruction does not involve memory access, this stage becomes a pass-through stage.

5. **Write-Back (WB)**: The final stage is where the results of the instruction are written back to the register file. The result of an ALU operation or data loaded from memory is written to the destination register.

# Fetch and Decode

- **Implementation Plan**
  
![image](https://github.com/vandhana01/RISC-V/assets/142392052/93ffbce4-57e7-4114-a0ac-9c67cd63c8b1)
   
## Labs

![image](https://github.com/vandhana01/RISC-V/assets/142392052/f4798145-fdb6-446d-99b9-942a67f5669e)



- Sample test program to check in viz

```v
  |cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
  ```
  
![image](https://github.com/vandhana01/RISC-V/assets/142392052/9dcdff7e-0848-4536-9e1b-47619011ec9f)

- Lab for Insstruction Fetch Logic
```v
  |cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
```
  
![image](https://github.com/vandhana01/RISC-V/assets/142392052/d4c6a8c5-3208-438a-95f6-adde859655ba)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/9c650957-4eb3-49f0-8a0e-62dd2eef8432)

- Lab for Instruction Decode
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1[4:0] = $instr[19:15];
         $rs2[4:0] = $instr[24:20];
         $rd[4:0] = $instr[11:7];
         $opcode[6:0] = $instr[6:0];
         $funct7[6:0] = $instr[31:25];
         $funct3[2:0] = $instr[14:12];
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
```
  
![image](https://github.com/vandhana01/RISC-V/assets/142392052/8f1e6c5f-0178-47c6-b6e8-52ac5a5df4f2)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/99c7baf4-4dd4-41eb-a883-6a697a1363a6)


- Lab for Instruction Decode with Validity
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required

```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/39a47dcc-ad6d-46e6-a16f-b644f6fc975d)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/29775ef3-c724-4689-8b6d-2edf248ab21d)

- Lab to Decode Individual Instruction
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];         
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/7d782627-ecd6-4870-bace-8a234efb8e0c)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/de5180b0-fe87-48d7-89a8-9a121ca51727)


# RISC-V Control Logic
- Lab for Register File
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = 1'b0;
         $rf_wr_index[4:0] = 5'b0;
         $rf_wr_data[31:0] = 32'b0;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/95525f66-650c-4ee2-a3b4-65e03a9f6acf)

- Lab for ALU Operations (add/addi)

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = 1'b0;
         $rf_wr_index[4:0] = 5'b0;
         $rf_wr_data[31:0] = 32'b0;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation

```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/b1f2cfe1-210a-4196-8820-78bb3457955e)

- Lab for Register File Write

```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = $rd_valid && $rd != 5'b0;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/7264d77f-3b8f-4f37-89d8-f6385c1a86f6)

- Lab for Branch Instructions
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>1$taken_br ? >>1$br_tgt_pc :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = $rd_valid && $rd != 5'b0;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $br_tgt_pc[31:0] = $pc + $imm;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/c5fed7fe-a677-4a76-8810-2f0940594f5d)


- **Lab for Testbench**
- Add `*passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9);`
- check log for passed message.

![image](https://github.com/vandhana01/RISC-V/assets/142392052/2cbfcbd3-bd42-4d4a-a459-bf8c3ff2dd5d)





</details>

# DAY 5
<details>
<summary> Complete Pipelined RISC-V CPU Micro-architecture </summary>
<br>
	
[](https://github.com/RISC-V#links-for-easy-navigaton)

+ [Pipelining the CPU](#pipelining-the-cpu)
+ [Solutions to Pipeline Hazards](#solutions-to-pipeline-hazards)
+ [Load/Store Instructions and Completing RISC-V CPU](#load/store-instructions-and-completing-risc-v-cpu)

# Pipelining the CPU
- Pipelining a RISC-V processor involves breaking down the instruction execution into multiple stages, allowing for the concurrent processing of multiple instructions and improving overall performance.
  
## Introduction to hazards
-  **Hazard** refers to a situation or condition that can potentially disrupt the normal and efficient execution of instructions in a processor's pipeline.
-  There are three main types of hazards:
   1. **Structural Hazards**
   - This can happen when multiple instructions need access to the same resource, such as the memory, ALU (Arithmetic Logic Unit), or a register file, during the same clock cycle.
   2. **Data Hazards**
   - Data hazards arise when an instruction depends on the result of a previous instruction that is still in progress within the pipeline.
   - There are three types of data hazards:
	1. **Read-After-Write (RAW) Hazard**: An instruction attempts to read a register or memory location that a previous instruction is still in the process of writing to.
	2. **Write-After-Read (WAR) Hazard**: An instruction attempts to write to a register or memory location that a subsequent instruction is reading from.
	3. **Write-After-Write (WAW) Hazard**: Two instructions attempt to write to the same register or memory location in close succession.
   3. **Control Hazards**
   - Control hazards, also known as control dependencies, occur when the pipeline encounters branches or jumps. The branch instruction may alter the program flow, leading to uncertainty about the path of execution.

## Labs
- Lab to create 3-Cycle Valid Signal
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>1$taken_br ? >>1$br_tgt_pc :
                                 >>1$pc + 32'd4;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
         $start = >>1$reset && !$reset;
         $valid = $reset ? 1'b0 : $start ? 1'b1 :
                                          >>3$valid;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1   
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $rf_wr_en = $rd_valid && $rd != 5'b0;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @1
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @1
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>1$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>1$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $br_tgt_pc[31:0] = $pc + $imm;
         *passed = |cpu/xreg[10]>>5$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@1, @1)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/ee59804a-b926-4ab7-afc6-22f61b03ff25)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/36a8769f-edb3-4494-92b9-60a200dcbbcc)

- Taking care of Invalid Cycles
  
![image](https://github.com/vandhana01/RISC-V/assets/142392052/c223baed-4763-48bc-846f-cd7716c64649)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/fcc2d865-c8db-41d4-bd4b-0a46b2db1196)

- To modify 3-cycle RISC-V to Distribute Logic
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                                 >>3$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
         $start = >>1$reset && !$reset;
         $valid = $reset ? 1'b0 : $start ? 1'b1 :
                                          >>3$valid;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = $rf_rd_data1;
         $src2_value[31:0] = $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $rf_wr_en = $rd_valid && $rd != 5'b0 && $valid;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/3f236314-ef99-4f14-bdfc-1ed8617c19c2)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/adfc1cdc-b269-49be-bb2f-03505404dd44)

# Solutions to Pipeline Hazards
## Labs
- Register File Bypass
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                                 >>3$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
         $start = >>1$reset && !$reset;
         $valid = $reset ? 1'b0 : $start ? 1'b1 :
                                          >>3$valid;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $rf_wr_en = $rd_valid && $rd != 5'b0 && $valid;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/6a1b9435-032e-477e-93c9-6daf2af2cfc1)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/e49cc08e-0ccf-4610-8603-819b34529d7b)

- To correct Branch Target Path
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $rf_wr_en = $rd_valid && $rd != 5'b0 && $valid;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/dd27f878-e003-4b36-be7a-bfb29d2a5aa5)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/6b4d0120-6143-4d78-b973-24102d9f59d9)

- Complete Instruction Decode
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_load = $opcode == 7'b0000011;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltui = $dec_bits ==? 11'bx_011_0010011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                                    32'bx;
         $rf_wr_en = $rd_valid && $rd != 5'b0 && $valid;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/d2f57766-d68a-42d4-a999-16f85b1268e4)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/2c34c205-46e5-4d3a-a7b2-01d3d514e6cf)

- Complete ALU
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_load = $opcode == 7'b0000011;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltui = $dec_bits ==? 11'bx_011_0010011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                          $is_andi ? $src1_value & $imm :
                          $is_ori ? $src1_value | $imm :
                          $is_xori ? $src1_value ^ $src2_value :
                          $is_slli ? $src1_value << $imm[5:0] :
                          $is_srli ? $src1_value >> $imm[5:0] :
                          $is_and ? $src1_value & $src2_value :
                          $is_or ? $src1_value | $src2_value : 
                          $is_xor ? $src1_value ^ $src2_value :
                          $is_sub ? $src1_value - $src2_value :
                          $is_sll ? $src1_value << $src2_value[4:0] :
                          $is_srl ? $src1_value >> $src2_value[4:0] :
                          $is_srai ? {{32{$src1_value[31]}}, $src1_value} >> $imm[4:0] :
                          $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]} :
                          $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]} :
                          $is_sra ? {{31{$src1_value[31]}}, $src1_value} >> $src2_value[4:0] :
                          $is_lui ? {$imm[31:12], 12'b0} :
                          $is_auipc ? $pc + $imm :
                          $is_jal ? $pc + 4 :
                          $is_jalr ? $pc + 4 :
                          32'bx;
         $rf_wr_en = $rd_valid && $rd != 5'b0 && $valid;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```

![image](https://github.com/vandhana01/RISC-V/assets/142392052/e9800c5b-e451-43fc-bff7-b7064c01aa41)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/34a5a4b1-9be4-49f4-973e-5b69afccfd5a)

# Load/Store Instructions and Completing RISC-V CPU
## Labs
- Lab to Redirect Loads
```v
 |cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                         >>3$valid_load ? >>3$inc_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_load = $opcode == 7'b0000011;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltui = $dec_bits ==? 11'bx_011_0010011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                          $is_andi ? $src1_value & $imm :
                          $is_ori ? $src1_value | $imm :
                          $is_xori ? $src1_value ^ $src2_value :
                          $is_slli ? $src1_value << $imm[5:0] :
                          $is_srli ? $src1_value >> $imm[5:0] :
                          $is_and ? $src1_value & $src2_value :
                          $is_or ? $src1_value | $src2_value : 
                          $is_xor ? $src1_value ^ $src2_value :
                          $is_sub ? $src1_value - $src2_value :
                          $is_sll ? $src1_value << $src2_value[4:0] :
                          $is_srl ? $src1_value >> $src2_value[4:0] :
                          $is_srai ? {{32{$src1_value[31]}}, $src1_value} >> $imm[4:0] :
                          $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]} :
                          $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]} :
                          $is_sra ? {{31{$src1_value[31]}}, $src1_value} >> $src2_value[4:0] :
                          $is_lui ? {$imm[31:12], 12'b0} :
                          $is_auipc ? $pc + $imm :
                          $is_jal ? $pc + 4 :
                          $is_jalr ? $pc + 4 :
                          32'bx;
         $rf_wr_en = $rd_valid && $rd != 5'b0 && $valid;
         $rf_wr_index[4:0] = $rd;
         $rf_wr_data[31:0] = $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $valid_load = $valid && $is_load;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br || >>1$valid_load || >>2$valid_load);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/99fd9970-b08d-4ba6-a3ce-e3a103b82e00)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/04f37810-03ea-4a2d-be94-e8e08a41f060)

- Lab to Load Data From Memory to Register File
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                         >>3$valid_load ? >>3$inc_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_load = $opcode == 7'b0000011;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltui = $dec_bits ==? 11'bx_011_0010011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                          $is_andi ? $src1_value & $imm :
                          $is_ori ? $src1_value | $imm :
                          $is_xori ? $src1_value ^ $src2_value :
                          $is_slli ? $src1_value << $imm[5:0] :
                          $is_srli ? $src1_value >> $imm[5:0] :
                          $is_and ? $src1_value & $src2_value :
                          $is_or ? $src1_value | $src2_value : 
                          $is_xor ? $src1_value ^ $src2_value :
                          $is_sub ? $src1_value - $src2_value :
                          $is_sll ? $src1_value << $src2_value[4:0] :
                          $is_srl ? $src1_value >> $src2_value[4:0] :
                          $is_srai ? {{32{$src1_value[31]}}, $src1_value} >> $imm[4:0] :
                          $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]} :
                          $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]} :
                          $is_sra ? {{31{$src1_value[31]}}, $src1_value} >> $src2_value[4:0] :
                          $is_lui ? {$imm[31:12], 12'b0} :
                          $is_auipc ? $pc + $imm :
                          $is_jal ? $pc + 4 :
                          $is_jalr ? $pc + 4 :
                          32'bx;
         $rf_wr_en = ($rd_valid && $rd != 5'b0 && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = >>2$valid_load ? >>2$rd : $rd;
         $rf_wr_data[31:0] = >>2$valid_load ? >>2$ld_data : $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $valid_load = $valid && $is_load;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br || >>1$valid_load || >>2$valid_load);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
      @5
         $ld_data = 'x;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+cpu_viz(@4)    // For visualisation
```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/1e42be23-97d9-4222-b4c3-03a6c17e98c2)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/62dac2a8-d10f-441f-a374-95ea4fff9e10)

- Lab to Instantiate Data Memory to CPU
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                         >>3$valid_load ? >>3$inc_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_load = $opcode == 7'b0000011;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltui = $dec_bits ==? 11'bx_011_0010011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                          $is_andi ? $src1_value & $imm :
                          $is_ori ? $src1_value | $imm :
                          $is_xori ? $src1_value ^ $src2_value :
                          $is_slli ? $src1_value << $imm[5:0] :
                          $is_srli ? $src1_value >> $imm[5:0] :
                          $is_and ? $src1_value & $src2_value :
                          $is_or ? $src1_value | $src2_value : 
                          $is_xor ? $src1_value ^ $src2_value :
                          $is_sub ? $src1_value - $src2_value :
                          $is_sll ? $src1_value << $src2_value[4:0] :
                          $is_srl ? $src1_value >> $src2_value[4:0] :
                          $is_srai ? {{32{$src1_value[31]}}, $src1_value} >> $imm[4:0] :
                          $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]} :
                          $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]} :
                          $is_sra ? {{31{$src1_value[31]}}, $src1_value} >> $src2_value[4:0] :
                          $is_lui ? {$imm[31:12], 12'b0} :
                          $is_auipc ? $pc + $imm :
                          $is_jal ? $pc + 4 :
                          $is_jalr ? $pc + 4 :
                          32'bx;
         $rf_wr_en = ($rd_valid && $rd != 5'b0 && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = >>2$valid_load ? >>2$rd : $rd;
         $rf_wr_data[31:0] = >>2$valid_load ? >>2$ld_data : $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $valid_load = $valid && $is_load;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br || >>1$valid_load || >>2$valid_load);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
      /dmem[15:0]
         @4
            $wr = |cpu$dmem_wr_en && (|cpu$dmem_addr == #dmem);
            $value[31:0] = |cpu$reset ? #dmem : $wr ? |cpu$dmem_wr_data :
                                                      $RETAIN;
      @4
         $dmem_wr_data[31:0] = $src2_value;
         $dmem_wr_en = $is_s_instr && $valid;
         $dmem_rd_en = $is_load;
         $dmem_addr[3:0] = $result[5:2];
         ?$dmem_rd_en
            $dmem_rd_data[31:0] = /dmem[$dmem_addr]>>1$value;
      @5
         $ld_data[31:0] = $dmem_rd_data;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
      m4+cpu_viz(@4)    // For visualisation  
```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/eb8c829b-bc5f-4211-9094-e7cdd6e80224)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/05563f47-ef7a-40a5-a5a5-b6af1d94ef67)

- Add stores and loads to Test program
```v
// External to function:
   m4_asm(ADD, r10, r0, r0)             // Initialize r10 (a0) to 0.
   // Function:
   m4_asm(ADD, r14, r10, r0)            // Initialize sum register a4 with 0x0
   m4_asm(ADDI, r12, r10, 1010)         // Store count of 10 in register a2.
   m4_asm(ADD, r13, r10, r0)            // Initialize intermediate sum register a3 with 0
   // Loop:
   m4_asm(ADD, r14, r13, r14)           // Incremental addition
   m4_asm(ADDI, r13, r13, 1)            // Increment intermediate register by 1
   m4_asm(BLT, r13, r12, 1111111111000) // If a3 is less than a2, branch to label named <loop>
   m4_asm(ADD, r10, r14, r0)            // Store final result to register a0 so that it can be read by main program
   m4_asm(SW, r0, r10, 10000)           // Store the final result value to byte address 16
   m4_asm(LW, r17, r0, 10000)           // Load the final result value from adress 16 to x17  
```
- Lab for Jump Instructions
```v
|cpu
      @0
         $reset = *reset;
         $pc[31:0] = >>1$reset ? 32'b0 :
                         >>3$valid_taken_br ? >>3$br_tgt_pc :
                         >>3$valid_load ? >>3$inc_pc :
                         >>3$valid_jump && >>3$is_jal ? >>3$br_tgt_pc :
                         >>3$valid_jump && >>3$is_jalr ? >>3$jalr_tgt_pc :
                                 >>1$inc_pc;
         $imem_rd_addr[M4_IMEM_INDEX_CNT-1:0] = $pc[M4_IMEM_INDEX_CNT+1:2];
         $imem_rd_en = !$reset;
      /imem[7:0]
         @1
            $instr[31:0] = *instrs\[#imem\];
      ?$imem_rd_en
         @1
            $imem_rd_data[31:0] = /imem[$imem_rd_addr]$instr;
      @1 
         $inc_pc[31:0] = $pc + 32'd4;
         $instr[31:0] = $imem_rd_data[31:0];
         $is_b_instr = $instr[6:2] ==? 5'b11000;
         $is_r_instr = $instr[6:2] ==? 5'b01011 ||
                          $instr[6:2] ==? 5'b011x0 ||
                          $instr[6:2] ==? 5'b10100;
         $is_j_instr = $instr[6:2] ==? 5'b11011;
         $is_i_instr = $instr[6:2] ==? 5'b0000x ||
                            $instr[6:2] ==? 5'b001x0 ||
                            $instr[6:2] ==? 5'b11001;
         $is_u_instr = $instr[6:2] ==? 5'b0x101;
         $is_s_instr = $instr[6:2] ==? 5'b0100x;
         $is_load = $opcode == 7'b0000011;
         $rs1_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $rs2_valid = $is_r_instr || $is_s_instr || $is_b_instr;
         $rd_valid = $is_r_instr || $is_i_instr || $is_u_instr || $is_j_instr;
         $funct3_valid = $is_r_instr || $is_i_instr || $is_s_instr || $is_b_instr;
         $funct7_valid = $is_r_instr;
         $imm[31:0] = $is_i_instr ? {{21{$instr[31]}}, $instr[30:20]} :
                         $is_s_instr ? {{21{$instr[31]}}, $instr[30:25], $instr[11:7]} :
                         $is_b_instr ? {{20{$instr[31]}}, $instr[7], $instr[30:25], $instr[11:8], 1'b0} :
                         $is_u_instr ? {$instr[31:12], 12'b0} :
                         $is_j_instr ? {{12{$instr[31]}}, $instr[19:12], $instr[20], $instr[30:21], 1'b0} :
                                     32'b0;
         ?$rs1_valid
            $rs1[4:0] = $instr[19:15];
         ?$rs2_valid
            $rs2[4:0] = $instr[24:20];
         ?$rd_valid
            $rd[4:0] = $instr[11:7];
         ?$funct3_valid
            $funct3[2:0] = $instr[14:12];
         ?$funct7_valid
            $funct7[6:0] = $instr[31:25];
         $opcode[6:0] = $instr[6:0];
         $dec_bits[10:0] = {$funct7[5], $funct3, $opcode};
         $is_slti = $dec_bits ==? 11'bx_010_0010011;
         $is_slt = $dec_bits ==? 11'b0_010_0110011;
         $is_slli = $dec_bits ==? 11'b0_001_0010011;
         $is_sll = $dec_bits ==? 11'b0_001_0110011;
         $is_sh = $dec_bits ==? 11'bx_001_0100011;
         $is_sb = $dec_bits ==? 11'bx_000_0100011;
         $is_ori = $dec_bits ==? 11'bx_110_0010011;
         $is_or = $dec_bits ==? 11'b0_110_0110011;
         $is_lui = $dec_bits ==? 11'bx_xxx_0110111;
         $is_jalr = $dec_bits ==? 11'bx_000_1100111;
         $is_jal = $dec_bits ==? 11'bx_xxx_1101111;
         $is_auipc = $dec_bits ==? 11'bx_xxx_0010111;
         $is_andi = $dec_bits ==? 11'bx_111_0010011;
         $is_and = $dec_bits ==? 11'b0_111_0110011;
         $is_xori = $dec_bits ==? 11'bx_100_0010011;
         $is_xor = $dec_bits ==? 11'b0_100_0110011;
         $is_sw = $dec_bits ==? 11'bx_010_0100011;
         $is_sub = $dec_bits ==? 11'b1_000_0110011;
         $is_srli = $dec_bits ==? 11'b0_101_0010011;
         $is_srl = $dec_bits ==? 11'b0_101_0110011;
         $is_srai = $dec_bits ==? 11'b1_101_0010011;
         $is_sra = $dec_bits ==? 11'b1_101_0110011;
         $is_sltu = $dec_bits ==? 11'b0_011_0110011;
         $is_sltui = $dec_bits ==? 11'bx_011_0010011;
         $is_bne = $dec_bits ==? 11'bx_001_1100011;
         $is_bltu = $dec_bits ==? 11'bx_110_1100011;
         $is_blt = $dec_bits ==? 11'bx_100_1100011;
         $is_bgeu = $dec_bits ==? 11'bx_111_1100011;
         $is_bge = $dec_bits ==? 11'bx_101_1100011;
         $is_beq = $dec_bits ==? 11'bx_000_1100011;
         $is_addi = $dec_bits ==? 11'bx_000_0010011;
         $is_add = $dec_bits ==? 11'b0_000_0110011;
      /xreg[31:0]
         @3
            $wr = |cpu$rf_wr_en && (|cpu$rf_wr_index != 5'b0) && (|cpu$rf_wr_index == #xreg);
            $value[31:0] = |cpu$reset ? #xreg : 
                                  $wr ? |cpu$rf_wr_data : $RETAIN;
      @2
         $rf_rd_index1[4:0] = $rs1;
         $rf_rd_en1 = $rs1_valid;
         $rf_rd_en2 = $rs2_valid;
         $rf_rd_index2[4:0] = $rs2;
         ?$rf_rd_en1
            $rf_rd_data1[31:0] = /xreg[$rf_rd_index1]>>2$value;
         ?$rf_rd_en2
            $rf_rd_data2[31:0] = /xreg[$rf_rd_index2]>>2$value;
         $src1_value[31:0] = (>>1$rf_wr_index == $rf_rd_index1) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data1;
         $src2_value[31:0] = (>>1$rf_wr_index == $rf_rd_index2) && >>1$rf_wr_en ? >>1$result :
                                                                                  $rf_rd_data2;
         $jalr_tgt_pc[31:0] = $src1_value + $imm;
         $br_tgt_pc[31:0] = $pc + $imm;
      @3
         $sltiu_rslt[31:0] = $src1_value < $imm;
         $sltu_rslt[31:0] = $src1_value < $src2_value;
         $result[31:0] = $is_addi ? $src1_value + $imm :
                          $is_add ? $src1_value + $src2_value :
                          $is_andi ? $src1_value & $imm :
                          $is_ori ? $src1_value | $imm :
                          $is_xori ? $src1_value ^ $src2_value :
                          $is_slli ? $src1_value << $imm[5:0] :
                          $is_srli ? $src1_value >> $imm[5:0] :
                          $is_and ? $src1_value & $src2_value :
                          $is_or ? $src1_value | $src2_value : 
                          $is_xor ? $src1_value ^ $src2_value :
                          $is_sub ? $src1_value - $src2_value :
                          $is_sll ? $src1_value << $src2_value[4:0] :
                          $is_srl ? $src1_value >> $src2_value[4:0] :
                          $is_srai ? {{32{$src1_value[31]}}, $src1_value} >> $imm[4:0] :
                          $is_slt ? ($src1_value[31] == $src2_value[31]) ? $sltu_rslt : {31'b0, $src1_value[31]} :
                          $is_slti ? ($src1_value[31] == $imm[31]) ? $sltiu_rslt : {31'b0, $src1_value[31]} :
                          $is_sra ? {{31{$src1_value[31]}}, $src1_value} >> $src2_value[4:0] :
                          $is_lui ? {$imm[31:12], 12'b0} :
                          $is_auipc ? $pc + $imm :
                          $is_jal ? $pc + 4 :
                          $is_jalr ? $pc + 4 :
                          32'bx;
         $rf_wr_en = ($rd_valid && $rd != 5'b0 && $valid) || >>2$valid_load;
         $rf_wr_index[4:0] = >>2$valid_load ? >>2$rd : $rd;
         $rf_wr_data[31:0] = >>2$valid_load ? >>2$ld_data : $result;
         $taken_br = $is_beq ? ($src1_value == $src2_value) :
                          $is_bne ? ($src1_value != $src2_value) :
                          $is_blt ? (($src1_value < $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bge ? (($src1_value >= $src2_value) ^ ($src1_value[31] != $src2_value[31])) :
                          $is_bltu ? ($src1_value < $src2_value) :
                          $is_bgeu ? ($src1_value >= $src2_value) :
                                          1'b0;
         $valid_taken_br = $valid && $taken_br;
         $is_jump = $is_jal || $is_jalr;
         $valid_load = $valid && $is_load;
         $valid_jump = $is_jump && $valid;
         $valid = !(>>1$valid_taken_br || >>2$valid_taken_br || >>1$valid_load || >>2$valid_load || >>1$valid_jump || >>2$valid_jump);
         *passed = |cpu/xreg[10]>>3$value == (1+2+3+4+5+6+7+8+9);
      /dmem[15:0]
         @4
            $wr = |cpu$dmem_wr_en && (|cpu$dmem_addr == #dmem);
            $value[31:0] = |cpu$reset ? #dmem : $wr ? |cpu$dmem_wr_data :
                                                      $RETAIN;
      @4
         $dmem_wr_data[31:0] = $src2_value;
         $dmem_wr_en = $is_s_instr && $valid;
         $dmem_rd_en = $is_load;
         $dmem_addr[3:0] = $result[5:2];
         ?$dmem_rd_en
            $dmem_rd_data[31:0] = /dmem[$dmem_addr]>>1$value;
      @5
         $ld_data[31:0] = $dmem_rd_data;
|cpu
      m4+imem(@1)    // Args: (read stage)
      m4+rf(@2, @3)  // Args: (read stage, write stage) - if equal, no register bypass is required
      m4+dmem(@4)    // Args: (read/write stage)
      m4+cpu_viz(@4)    // For visualisation
```
![image](https://github.com/vandhana01/RISC-V/assets/142392052/1e11f704-5e4f-4f8c-8f0b-2767ffe5e761)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/d45be8a3-beb0-4df2-b90b-495bb070b5cf)


</details>

# Wrap UP 

<details>
<summary> Final RISC-V CPU Core implementation </summary>
<br>
	
[](https://github.com/vandhana01/RISc-V#links-for-easy-navigaton)

## Final RISC-V CPU Core implementation
- Makerchip allows you to see the code generated for a RISC-V core in both TL-Verilog and SystemVerilog and visually compare the differences in code size and complexity.
- TL-Verilog is designed to make hardware design more concise and readable, which often results in a reduction in the amount of code needed to describe a complex hardware design compared to traditional hardware description languages like SystemVerilog.

- CODE: https://github.com/vandhana01/RISC-V/blob/main/final_riscv_core.tlv
    
![image](https://github.com/vandhana01/RISC-V/assets/142392052/86d231f3-4f06-4ee2-97e5-227bc08c0fcd)

![image](https://github.com/vandhana01/RISC-V/assets/142392052/cac2c257-8701-4f17-bae9-e5e56effd9ac)


- Comparing the code for a RISC-V core written in TL-Verilog and SystemVerilog using a tool like Makerchip can indeed show significant code reduction in favor of TL-Verilog.   

![image](https://github.com/vandhana01/RISC-V/assets/142392052/8d6a5bca-889c-4bbe-beca-c66feb06f65f)

## CONCLUSION
- When comparing the code for a RISC-V CPU core in TL-Verilog and SystemVerilog using Makerchip platform, you can visually see the significant code reduction achieved with TL-Verilog, making it an attractive option for projects where code simplicity and conciseness are valued. However, the ultimate choice should align with your project's goals and constraints.
</details>
