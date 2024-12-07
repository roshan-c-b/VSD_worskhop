# VSDSquadron Mini Internship November_2024
 The goal of the VSDSquadron Mini-Internship program is to use open-source tools to introduce participants to RISC-V architecture and VLSI chip design. Using the VSDSquadron Mini RISC-V Development Board, the program's central component, it offers a practical learning experience.

This development board has a 32-bit RISC-V CPU with a clock speed of 24MHz, 16KB of flash memory, and 2KB of SRAM. With its 15 GPIO pins for hardware interface and support for SPI, USART, and I2C, it may be used for a wide range of projects. Participants in the program develop and test hardware applications to use their understanding of the RISC-V ecosystem.<br />



***

<details>
<summary><b>Task 1:</b> Execute C program with GNU GCC and RISC-V GCC compiler and understand the assembly code. </summary><br />
  

  **1.Command for Installing Leafpad**<br />
  ```
  $ sudo apt install leafpad
  ```
  
  **2.Command for Opening Leafpad**<br />
  ```
  $ cd
  $ leafpad filename.c &
  ```
  Enter the C Code in the leafpad.
  
  ![git-1](https://github.com/user-attachments/assets/882a740c-66b9-4aa8-9a4b-b54c03f15fb2)

  
  **3.Commands to Compile and View the Output**<br />
  ```
  $ gcc filename.c
  $ cat filename.c
  $ ./a.out
  ```
  ![git-2](https://github.com/user-attachments/assets/8fc91ce4-b25e-411c-bc89-cb6063bc6f75)

  
  **4.Command for Compiling the Code using RISC-V Compiler**<br />
  ```
  $ riscv64-unknown-elf-gcc -O1 -mabi=lp64 -march=rv64i -o filename.o filename.c
  $ ls -ltr filename.o
  ```
  ![install risc-compiler](https://github.com/user-attachments/assets/51ba5cb7-bf72-4d54-a8a4-c232be45d780)
  

  **5.Command to View the Assembly Code**<br />
  ```
  $ riscv64-unknown-elf-objdump -d filename.o //Gives bunch of Code
  $ riscv64-unknown-elf-objdump -d filename.o | less // Gives Reduced Code
  /main //to view the main function of the code
  ```
  ![git-3](https://github.com/user-attachments/assets/98404d4b-6282-405d-9760-b2b09ec97016)

  ```
  To calculate the number of instructions:-
  101b0 - 10184 = 2c     //Hex format
  2c/4 = b = 11          //address are incremented by 4
  ```


  **6. Command to View the Assembly Code**<br />
  Same command as step-4 but replacing O1 with Ofast.
  ```
  $ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o filename.o filename.c
  $ riscv64-unknown-elf-objdump -d filename.o | less 
  /main 
  ```
  ![git-4](https://github.com/user-attachments/assets/d2b861aa-956a-46c4-a0c9-11246659428e)

  ```
  Calculating number of instructions:-
  100dc - 100b0 = 2c      // Hex format
  2c/4 = b = 11           // address are incremented by 4
  ```
  Same number of instructions as the command in step-4 (with O1).
  
</details>


<details>
<summary><b>Task 2:</b> SPIKE simulation and Debugging of C code Using Spike</summary>   
<br>

SPIKE SIMULATION
--------

SPIKE is a RISC-V simulator. In this task, we will check the output of the previous program (from task1 - ```sum1ton.o```) using the RISC-V Compiler with the spike command.

1. Debugging using the command:
    ```bash
    $ spike -d pk sum1ton.o
    ```
    ![Task-2-1](https://github.com/user-attachments/assets/9fa16c2f-6699-4426-bc1a-f68c3153afd5)

2. Assembly Language Program:
   
   ![Task-2-2](https://github.com/user-attachments/assets/cdf273bd-d94d-4b1f-92af-af6bbfb16c7d)

3. Debugger:

   ![Task-2-3](https://github.com/user-attachments/assets/663ef5cf-651f-44a8-b6e5-33ecd90bb569)

   ![Task-2-4](https://github.com/user-attachments/assets/e864276a-1242-49ab-bfc0-9db3db0755ce)

At address `100b4` the value of stack point before and after completion of the instruction is:
   - `sp` = `0x0000003ffffffb50`
   - `sp, sp, -16` = `0x0000003ffffffb40`

![Task-2-4(calc)](https://github.com/user-attachments/assets/2056bdb2-7875-4978-aeb6-441cf3594ab9)

Difference between stack point values = `10 (Hexadecimal)`, `16 (Decimal)`.

---

At address `100d8`, the program returns the sum = `55`.

<hr>

## About Instructions Used:

LUI (LOAD UPPER IMMEDIATE):
-
* This instruction is a key feature in RISC-V architecture. It is used to load a 20-bit immediate value into the upper 20 bits of a register, while setting the lower 12 bits to zero.
* Format - LUI rd, immediate [ rd- destination register, immediate- 20-bit immediate value to be loaded]
* The 20- bit immediate value is shifted left by 12 bits(appended with 12 zeros). The lower 12 bits of the destination register are set to zero. 

ADDI (ADD IMMEDIATE)
-
* This instruction is a common operation in RISC-V architecture.
* It performs an addition between a register and a sign-extended immediate value, storing the result in a destination register.
* Format- ADDI rd, rs1, immediate (rd- destination register, rs- source register, immediate- the immediate value to be added).


Application CODE:
--
Arithmetic Logic Unit (ALU):
--
An Arithmetic Logic Unit (ALU) is a fundamental building block of any processor, responsible for performing arithmetic and logic operations. This code simulates a simple ALU in C, which can execute basic operations like addition, subtraction, multiplication, and division. The operations are selected programmatically, and the results are displayed to demonstrate the functionality of the ALU. This program is designed to work across various compilers, including GCC and RISC-V GCC, ensuring platform compatibility and enabling easy testing on different hardware architectures.

The generated assembly code showcases how instructions are executed at a low level, highlighting the efficiency and simplicity of the RISC-V instruction set.

1.C-program :
-
```
Open leafpad in the terminal and write the C code.
Compile with C gcc compiler and check the output.
```
![Task-2-1(new code)](https://github.com/user-attachments/assets/dcf15d52-d269-49af-8876-ef47ed2b168b)

Now, compile with RISC-V GCC command. (Both -O1 and -Ofast).

![Task-2-2(new code)](https://github.com/user-attachments/assets/85246589-1255-4958-b7a3-17524b18d32e)

2.Assembly Program for the C code:
-
![Task-2-3(new code- assembly)](https://github.com/user-attachments/assets/2a1d928f-f2b2-45e8-a325-b4772ad98eba)

# Assembly Instruction Breakdown:

### **1. `lui a0,0x21`**
- Load the upper immediate value `0x21` into the `a0` register.  
- This sets up the upper 20 bits of a memory address.

### **2. `addi sp,sp,-16`**
- Adjust the stack pointer (`sp`) by decreasing it by 16 bytes.  
- This reserves space on the stack for local variables or saved registers.

### **3. `li a1,15`**
- Load the immediate value `15` into register `a1`.  
- This prepares one of the operands for the ALU operation.

### **4. `addi a0,a0,560 # 21230 <__clzdi2+0x40>`**
- Add `560` to `a0`.  
- This completes the calculation of a memory address (`21230`) where data or a function resides.

### **5. `sd ra,8(sp)`**
- Store the return address (`ra`) at the memory location `sp + 8`.  
- This ensures the return address is preserved before a function call.

### **6. `jal ra,105e4 <printf>`**
- Jump to the `printf` function and save the next instruction's address into `ra`.  
- This outputs the ALU operation result.

### **7. `lui a0,0x21`**
- Reload the upper part of a new memory address into `a0`.

### **8. `li a1,5`**
- Load the immediate value `5` into register `a1`.  
- This is another operand for the ALU.

### **9. `addi a0,a0,576 # 21240 <__clzdi2+0x50>`**
- Add an offset of `576` to `a0`.  
- This calculates the next memory address.

### **10. `jal ra,105e4 <printf>`**
- Call `printf` to display the result of another ALU operation.

### **11. `lui a0,0x21`**
- Load the upper immediate value for another address.

### **12. `li a1,50`**
- Load the immediate value `50` into register `a1`.  
- This is used for the next ALU operation.

### **13. `addi a0,a0,600 # 21258 <__clzdi2+0x68>`**
- Add an offset of `600` to `a0`.  
- This prepares the memory address for another operation.

### **14. `jal ra,105e4 <printf>`**
- Call `printf` again to print the result.

### **15. `lui a0,0x21`**
- Reload the upper immediate value into `a0`.

### **16. `li a1,2`**
- Load the value `2` into `a1`.  
- This is another operand.

### **17. `addi a0,a0,624 # 21270 <__clzdi2+0x80>`**
- Add an offset of `624` to `a0`.  
- This sets up the memory address for the final operation.

### **18. `jal ra,105e4 <printf>`**
- Call `printf` to display the result of the final ALU operation.

### **19. `ld ra,8(sp)`**
- Load the return address (`ra`) from the stack.  
- This restores the return address for proper function exit.

### **20. `li a0,0`**
- Set the value in `a0` to `0`.  
- This is the return value of the `main` function (success).

### **21. `addi sp,sp,16`**
- Adjust the stack pointer back up by 16 bytes to deallocate local memory.

### **22. `ret`**
- Return from the function using the address in `ra`.
---

3.Debugging the Code
-
Command:
```
$ spike -d pk alu.o
```
![Task-2-4(new code-debugging)](https://github.com/user-attachments/assets/1fa5192b-f23e-4e4f-b535-7482199ed3ba)

Finally, the address ```10104``` returns the final output.

</details>


<details>
<summary><b>Task 3:Types of RISC-V Instructions and the 32-bit representation of the instructions from application code. </b>  </summary><br />
  

**1.Various RISC-V instruction type are as follows:**<br />

## RISC-V Instruction Formats
 ```
   The RISC-V ISA defines the following instruction types:
   
   R-Type: Register-register operations
   I-Type: Immediate operations
   S-Type: Store instructions
   B-Type: Branch instructions
   U-Type: Upper immediate instructions
   J-Type: Jump instructions

 ```
### R-Type Instructions
<details>
<summary>R-Type Format</summary>
<ul>
  <li><strong>Bit Range:</strong></li>
  <ul>
    <li><strong>opcode:</strong> [0:6] - Specifies the operation type (e.g., arithmetic, logical).</li>
    <li><strong>rd:</strong> [7:11] - Destination register.</li>
    <li><strong>funct3:</strong> [12:14] - Specifies the operation (e.g., ADD, SUB).</li>
    <li><strong>rs1:</strong> [15:19] - First source register.</li>
    <li><strong>rs2:</strong> [20:24] - Second source register.</li>
    <li><strong>funct7:</strong> [25:31] - Additional operation specifier (e.g., ADD vs. SUB).</li>
  </ul>
  <br>
  <strong>Example:</strong> ADD rd, rs1, rs2 <br>
  <strong>Operation:</strong> Adds the values in rs1 and rs2 and stores the result in rd. <br>
  <strong>Opcode:</strong> 0110011
</ul>
</details>

---

### I-Type Instructions
<details>
<summary>I-Type Format</summary>
<ul>
  <li><strong>Bit Range:</strong></li>
  <ul>
    <li><strong>opcode:</strong> [0:6] - Specifies the operation type.</li>
    <li><strong>rd:</strong> [7:11] - Destination register.</li>
    <li><strong>funct3:</strong> [12:14] - Specifies the operation.</li>
    <li><strong>rs1:</strong> [15:19] - Source register.</li>
    <li><strong>imm[11:0]:</strong> [20:31] - 12-bit signed immediate value.</li>
  </ul>
  <br>
  <strong>Example:</strong> ADDI rd, rs1, imm <br>
  <strong>Operation:</strong> Adds an immediate value (imm) to rs1 and stores the result in rd. <br>
  <strong>Opcode:</strong> 0010011
</ul>
</details>

---

### S-Type Instructions
<details>
<summary>S-Type Format</summary>
<ul>
  <li><strong>Bit Range:</strong></li>
  <ul>
    <li><strong>opcode:</strong> [0:6] - Specifies the store operation.</li>
    <li><strong>imm[4:0]:</strong> [7:11] - Lower 5 bits of the immediate value.</li>
    <li><strong>funct3:</strong> [12:14] - Specifies the store operation (e.g., SW, SH).</li>
    <li><strong>rs1:</strong> [15:19] - Base address register.</li>
    <li><strong>rs2:</strong> [20:24] - Register whose value will be stored.</li>
    <li><strong>imm[11:5]:</strong> [25:31] - Upper 7 bits of the immediate value.</li>
  </ul>
  <br>
  <strong>Example:</strong> SW rs2, imm(rs1) <br>
  <strong>Operation:</strong> Stores the value in rs2 at the memory address calculated as rs1 + imm. <br>
  <strong>Opcode:</strong> 0100011
</ul>
</details>

---

### U-Type Instructions
<details>
<summary>U-Type Format</summary>
<ul>
  <li><strong>Bit Range:</strong></li>
  <ul>
    <li><strong>opcode:</strong> [0:6] - Specifies the type of instruction.</li>
    <li><strong>rd:</strong> [7:11] - Destination register.</li>
    <li><strong>imm[31:12]:</strong> [12:31] - 20-bit immediate value.</li>
  </ul>
  <br>
  <strong>Example:</strong> LUI rd, imm <br>
  <strong>Operation:</strong> Loads the upper 20 bits of imm into rd. <br>
  <strong>Opcode:</strong> 0110111
</ul>
</details>

---

### B-Type Instructions
<details>
<summary>B-Type Format</summary>
<ul>
  <li><strong>Bit Range:</strong></li>
  <ul>
    <li><strong>opcode:</strong> [0:6] - Specifies the branch operation.</li>
    <li><strong>imm[11]:</strong> [7] - Bit 11 of the branch offset.</li>
    <li><strong>imm[4:1]:</strong> [8:11] - Lower 4 bits of the branch offset.</li>
    <li><strong>funct3:</strong> [12:14] - Specifies the branch condition (e.g., BEQ, BNE).</li>
    <li><strong>rs1:</strong> [15:19] - First source register.</li>
    <li><strong>rs2:</strong> [20:24] - Second source register.</li>
    <li><strong>imm[10:5]:</strong> [25:30] - Bits 5–10 of the branch offset.</li>
    <li><strong>imm[12]:</strong> [31] - Bit 12 of the branch offset.</li>
  </ul>
  <br>
  <strong>Example:</strong> BEQ rs1, rs2, imm <br>
  <strong>Operation:</strong> Branches to PC + imm if rs1 == rs2. <br>
  <strong>Opcode:</strong> 1100011
</ul>
</details>

---

### J-Type Instructions
<details>
<summary>J-Type Format</summary>
<ul>
  <li><strong>Bit Range:</strong></li>
  <ul>
    <li><strong>opcode:</strong> [0:6] - Specifies the jump operation.</li>
    <li><strong>rd:</strong> [7:11] - Destination register to store the return address.</li>
    <li><strong>imm[19:12]:</strong> [12:19] - Bits 12–19 of the jump offset.</li>
    <li><strong>imm[11]:</strong> [20] - Bit 11 of the jump offset.</li>
    <li><strong>imm[10:1]:</strong> [21:30] - Bits 1–10 of the jump offset.</li>
    <li><strong>imm[20]:</strong> [31] - Bit 20 of the jump offset.</li>
  </ul>
  <br>
  <strong>Example:</strong> JAL rd, imm <br>
  <strong>Operation:</strong> Jumps to PC + imm and stores the return address in rd. <br>
  <strong>Opcode:</strong> 1101111
</ul>
</details>

---
  
**2. 15 unique RISC-V instrictions from the application code**<br />
      * To view the instructions , we should use the following commands to compile and view the assembly code.
  ```
  $ $ riscv64-unknown-elf-gcc -Ofast -mabi=lp64 -march=rv64i -o alu.o alu.c
  $ riscv64-unknown-elf-objdump -d alu.o | less 
  ```
  Following are the 15 instructions used in the application code: <br />
  
  
   |**Instruction**             |**Purpose**                                                                   |
   |----------------------------|------------------------------------------------------------------------------|
   | `lui a0,0x21`              | Load the upper immediate value `0x21` into the `a0` register.                |
   | `addi sp,sp,-16`           | Reserve 16 bytes on the stack by decrementing the stack pointer.             |
   | `li a1,15`                 | Load the immediate value `15` into the `a1` register (operand setup).        |
   | `sd ra,8(sp)`              | Store the return address (`ra`) to the stack for preserving state.           |
   | `jal ra,105e4 <printf>`    | Jump to the `printf` function to print the result and save the return addr.  |
   | `ld ra,8(sp)`              | Load the return address (`ra`) from the stack to restore state.              |
   | `addi a0,a0,560`           | Add an offset (`560`) to the address in `a0` for address calculation.        |
   | `li a1,5`                  | Load the immediate value `5` into the `a1` register.                         | 
   | `addi a0,a0,576`           | Add an offset (`576`) to the address in `a0`.                                |
   | `li a1,50`                 | Load the immediate value `50` into the `a1` register.                        |
   | `addi a0,a0,600`           | Add an offset (`600`) to the address in `a0`.                                |
   | `li a1,2`                  | Load the immediate value `2` into the `a1` register.                         |
   | `addi a0,a0,624`           | Add an offset (`624`) to the address in `a0`.                                |
   | `addi sp,sp,16`            | Deallocate 16 bytes from the stack by incrementing the stack pointer.        |
   | `ret`                      | Return from the function using the address in the `ra` register.             |

  

**3. The following table shows the 32-bit instructions code for the above 15 instructions**<br />

### Detailed RISC-V Instruction Table


| **Instruction**         | **Type** | **32-bit Binary Representation**                | **Breakdown**                                                                                                          |
|--------------------------|----------|------------------------------------------------|------------------------------------------------------------------------------------------------------------------------|
| `lui a0,0x21`           | U        | `000000000001 00001 01000 0110111`             | opcode: `0110111` <br> rd: `01010` (a0) <br> imm[31:12]: `000000000001`                                               |
| `addi sp,sp,-16`        | I        | `111111111110 01000 000 01000 0010011`         | opcode: `0010011` <br> funct3: `000` <br> imm[11:0]: `111111111110` (-16) <br> rs1: `01000` (sp) <br> rd: `01000` (sp) |
| `li a1,15`              | I        | `000000000111 01000 000 01001 0010011`         | opcode: `0010011` <br> funct3: `000` <br> imm[11:0]: `000000000111` (15) <br> rs1: `01000` (sp) <br> rd: `01001` (a1) |
| `sd ra,8(sp)`           | S        | `000000001000 01000 011 00001 0100011`         | opcode: `0100011` <br> funct3: `011` <br> imm[4:0]: `01000` (8) <br> rs1: `01000` (sp) <br> rs2: `00001` (ra) <br> imm[11:5]: `0000000` |
| `jal ra,105e4 <printf>` | J        | `000001000001 01110 1000 00001 1101111`        | opcode: `1101111` <br> imm[20]: `0` <br> imm[10:1]: `0001011101` <br> imm[11]: `0` <br> imm[19:12]: `00010000` <br> rd: `00001` (ra) |
| `ld ra,8(sp)`           | I        | `000000001000 01000 011 00001 0000011`         | opcode: `0000011` <br> funct3: `011` <br> imm[11:0]: `000000001000` (8) <br> rs1: `01000` (sp) <br> rd: `00001` (ra) |
| `addi a0,a0,560`        | I        | `000000100100 01010 000 01010 0010011`         | opcode: `0010011` <br> funct3: `000` <br> imm[11:0]: `000000100100` (560) <br> rs1: `01010` (a0) <br> rd: `01010` (a0) |
| `li a1,5`               | I        | `000000000101 01000 000 01001 0010011`         | opcode: `0010011` <br> funct3: `000` <br> imm[11:0]: `000000000101` (5) <br> rs1: `01000` (sp) <br> rd: `01001` (a1) |
| `addi a0,a0,576`        | I        | `000000100100 01010 000 01010 0010011`         | opcode: `0010011` <br> funct3: `000` <br> imm[11:0]: `000000100100` (576) <br> rs1: `01010` (a0) <br> rd: `01010` (a0) |
| `li a1,50`              | I        | `000000110010 01000 000 01001 0010011`         | opcode: `0010011` <br> funct3: `000` <br> imm[11:0]: `000000110010` (50) <br> rs1: `01000` (sp) <br> rd: `01001` (a1) |
| `addi a0,a0,600`        | I        | `000000100100 01010 000 01010 0010011`         | opcode: `0010011` <br> funct3: `000` <br> imm[11:0]: `000000100100` (600) <br> rs1: `01010` (a0) <br> rd: `01010` (a0) |
| `li a1,2`               | I        | `000000000010 01000 000 01001 0010011`         | opcode: `0010011` <br> funct3: `000` <br> imm[11:0]: `000000000010` (2) <br> rs1: `01000` (sp) <br> rd: `01001` (a1) |
| `addi a0,a0,624`        | I        | `000000100110 01010 000 01010 0010011`         | opcode: `0010011` <br> funct3: `000` <br> imm[11:0]: `000000100110` (624) <br> rs1: `01010` (a0) <br> rd: `01010` (a0) |
| `addi sp,sp,16`         | I        | `000000001000 01000 000 01000 0010011`         | opcode: `0010011` <br> funct3: `000` <br> imm[11:0]: `000000001000` (16) <br> rs1: `01000` (sp) <br> rd: `01000` (sp) |
| `ret`                   | I        | `000000000000 00000 000 00000 1100011`         | opcode: `1100011` <br> funct3: `000` <br> imm[11:0]: `000000000000` <br> rs1: `00000` <br> rd: `00000`                 |


</details>

<details>
<summary><b>Task 4:</b> Simulation of RISC-V Code Verilog netlist and Testbench </summary>   
<br>

Command to install iverliog and GTKWave:-
```
$ sudo apt install iverilog gtkwave

```
Step-1. Create a directory with the command:-
```
mkdir <name>
```
Step-2. create 2 files with the ```touch``` command as ```name_rv32i.v``` and ```name_rv32i_tb.v``` for verilog netlist and testbench code respectively.

We will not be writing the verilog codes, we shall take it from the following reference github repository.


Step-3. After getting the verilog codes and saving them, we can now simulate and verify.
Use the following code:-
```
$ iverilog -o name_rv32i name_rv32i.v name_rv32i_tb.v
```
After the above command is run, it will create ```iiitb_rv32i.vcd``` file.

Step-4. Now we shall open GTKWave with the above generated file, and view the output waveforms 

Command for opening GTKWave:
```
$ gtkwave iiitb_rv32i.vcd
```
The instructions in the verilog code are hard-coded.

**Hard-coded ISA** - That means the instructions do not follow the RISC-V 32-bit pattern, they have been encoded by designer with custom pattern.


Viewing the Output waveforms of the instructions in GTKWave :
--

1. ADD R6,R2,R1

![inst-1](https://github.com/user-attachments/assets/b620b73f-b2fd-450a-8be4-47c30f9bbb09)

2. SUB R7,R1,R2

![inst2-sub](https://github.com/user-attachments/assets/e4053e9c-6f78-4180-b15e-c699f6e81b2a)

3. AND R8,R1,R3

![inst3-AND](https://github.com/user-attachments/assets/0d277649-7941-4f31-bf0a-6693fff7472c)

4. OR R9,R2,R5

![inst4-OR](https://github.com/user-attachments/assets/50a69faf-d96e-4241-8290-39f239262ffe)

5. XOR R10,R1,R4

![inst5-XOR](https://github.com/user-attachments/assets/05c49a20-b0de-4097-ba4d-1c7aa1552c17)

6. SLT R1,R2,R4

![inst6-SLT](https://github.com/user-attachments/assets/428bd51d-478f-4cf4-a712-80878ad2f8dc)

7. ADDI R12,R4,5

![inst7-ADDI](https://github.com/user-attachments/assets/2c1f3a63-e42a-4f80-8f49-e66f7801a0a8)

8. 







 
