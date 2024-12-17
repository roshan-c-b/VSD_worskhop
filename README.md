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
<summary><b>Task 4:</b> Simulating and Viewing the RISC-V core instructions using Verilog netlist and testbench </summary>   
<br>
In this task, we will be observing output waveforms of RISC-V instructions by performing functional simulations using a verilog netlist .
 
**Software** : iverilog, GTKWave

Command to install iverliog and GTKWave:-
```
$ sudo apt install iverilog gtkwave

```
Follow the following steps to perform the simulation:
-
1. Create a directory with the command:-
```
mkdir <name>
```
2. create 2 files with the ```touch``` command as ```name_rv32i.v``` and ```name_rv32i_tb.v``` for verilog netlist and testbench code respectively.

We will not be writing the verilog codes, we shall take it from the following reference github repository.
Github repository: [iiitb_rv32i](https://github.com/vinayrayapati/rv32i/)* 


3. After getting the verilog codes and saving them, we can now simulate and verify.
Use the following code:-
```
$ iverilog -o name_rv32i name_rv32i.v name_rv32i_tb.v
```
After the above command is run, it will create ```iiitb_rv32i.vcd``` file.

4. Now we shall open GTKWave with the above generated file, and view the output waveforms 

Command for opening GTKWave:
```
$ gtkwave iiitb_rv32i.vcd
```
The instructions in the verilog code are hard-coded.

**Hard-coded ISA** - That means the instructions do not follow the RISC-V 32-bit pattern, they have been encoded by designer with custom pattern.

The following table explains the instructions in detail and the shows difference between RISC-V and custom encoding of instructions:

| **Instruction**      | **Explanation**                                                                          | **RISC-V Encoding**  | **Custom Encoding**  |
|-----------------------|-----------------------------------------------------------------------------------------|----------------------|----------------------|
| **ADD R4, R3, R2**    | Computes the sum of the values in R3 and R2, placing the result in R4                   | `32'h00210333`       | `32'h02308400`       |
| **SUB R5, R2, R3**    | Subtracts the value stored in R3 from R2 and stores the result in R5                    | `32'h403103b3`       | `32'h02309480`       |
| **AND R6, R2, R4**    | Executes a bitwise AND operation between R2 and R4, saving the result in R6             | `32'h0040e433`       | `32'h0240a400`       |
| **OR R7, R3, R5**     | Combines the bits of R3 and R5 using the OR operation, writing the output to R7         | `32'h005174b3`       | `32'h02513480`       |
| **XOR R8, R2, R4**    | Performs an XOR operation on the values in R2 and R4, storing the result in R8          | `32'h0040c633`       | `32'h0240c500`       |
| **SLT R2, R3, R5**    | Sets R2 to 1 if the value in R3 is smaller than R5, otherwise stores 0                  | `32'h00516133`       | `32'h02516580`       |
| **ADDI R10, R5, 8**   | Adds the immediate value 8 to the contents of R5 and stores the result in R10           | `32'h00512033`       | `32'h00820500`       |
| **BEQ R0, R0, 12**    | Compares R0 with R0, and if they are equal, branches to a target offset of 12           | `32'h00000c63`       | `32'h00c00002`       |
| **SW R2, R6, 4**      | Saves the value in R2 to the memory location calculated as R6 plus an offset of 4       | `32'h0020a223`       | `32'h00409281`       |
| **LW R9, R6, 4**      | Loads a word from memory at address (R6 + 4) into the R9 register                       | `32'h0040a683`       | `32'h00408681`       |
| **SRL R10, R8, R2**   | Shifts the bits in R8 right by the amount specified in R2, and stores the result in R10 | `32'h0020c293`       | `32'h0028a203`       |
| **SLL R11, R2, R3**   | Shifts the bits in R2 left by the value in R3, placing the result in R11                | `32'h003091b3`       | `32'h00308783`       |



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

6. SLT R1,R2,R4 : 
The SLT (Set on Less Than) instruction is an R-Type instruction in RISC-V assembly language, used to compare two registers and set a destination register to 1 if the first source register is less than the second source register. Otherwise, the destination register is set to 0.

![inst6-SLT](https://github.com/user-attachments/assets/428bd51d-478f-4cf4-a712-80878ad2f8dc)

7. ADDI R12,R4,5

![inst7-ADDI](https://github.com/user-attachments/assets/2c1f3a63-e42a-4f80-8f49-e66f7801a0a8)

8. SW R3,R1,2 : 
The SW (Store Word) instruction stores a 32-bit word from a source register into a memory address calculated as the sum of a base register and an immediate offset.

![inst8-SW](https://github.com/user-attachments/assets/3b2f8b35-5255-4ccd-ba43-b7b86f59e87f)


9. SRL R16,R11,R2: 
The SRL (Shift Right Logical) instruction shifts the value in a source register to the right by a specified number of bits, filling the vacated bits with zeros.

![inst9-SRL](https://github.com/user-attachments/assets/f9b69424-72b1-4abf-9764-1b049aeae6f9)

10. BEQ R0, R0, 15
The BEQ (Branch if Equal) instruction in RISC-V compares two registers; if their values are equal, it updates the Program Counter (PC) to branch to a specified offset. Otherwise, the PC increments to the next sequential instruction.

![inst10-BEQ](https://github.com/user-attachments/assets/46c4ff6a-f9c2-4fe8-a65f-b87a8e8039da)

The new PC value is: 10 + 15 = 25 (0x19)

11. BNE R0, R1, 20 :
The BNE (Branch if Not Equal) instruction in RISC-V compares two registers; if their values are not equal, it updates the Program Counter (PC) to branch to a specified offset. Otherwise, the PC increments to the next sequential instruction.

![inst11-BNE](https://github.com/user-attachments/assets/c7561294-4fa1-4edc-9906-cf549092640b)

The new PC value is = 10 + 15 = 25 (0x19)

12. SLL R15, R1, R2: 
The SLL (Shift Left Logical) instruction shifts the value in a source register to the left by a specified number of bits, filling the vacated bits with zeros.

![Inst12-SLL](https://github.com/user-attachments/assets/a80def9a-4553-44bb-9c5e-31c85c8f5eb0)
</details>


<details>
<summary><b>Task 5:</b> Implementing Simple ALU using VSDSquadron Mini</summary>  
  
## **Overview**  

This project focuses on implementing a Basic Arithmetic Logic Unit (ALU) capable of performing addition, subtraction, multiplication, and division operations. Designed using a RISC-V-based SoC development kit, the ALU takes two user-provided inputs and sequentially computes the corresponding sum, difference, product, and quotient of the numbers, without requiring additional control signals.
  
## **Components Required**  
* VSDSquadron Mini  
* I2C LCD DISPLAY(16*2)
* 4*4 MATRIX KEYPAD
* Jumper Wires   
* Breadboard
* VS Code for Software Development  
* PlatformIO multi framework professional IDE  
  
## **Board being used:-**
![board](https://github.com/user-attachments/assets/0f354f5a-03d5-417c-9df4-4c5dc3ff019a)


## **Circuit Diagram**
![connections](https://github.com/user-attachments/assets/3992e617-bc43-4d72-a6ab-b7d0c9e06c90)

## Hardware connections:

### I2C LCD :

| **LCD Pin** | **Description**       | **VSD Squadron Mini Pin** | **Board Connection** |
|-------------|-----------------------|----------------------------|-----------------------|
| **GND**     | Ground                | GND                        | Common Ground         |
| **VCC**     | Power Supply (+5V)    | 5V                         | 5V Power Rail         |
| **SDA**     | Serial Data Line (I2C)| PC6                        | I2C Data (SDA)        |
| **SCL**     | Serial Clock Line (I2C)| PC5                       | I2C Clock (SCL)       |

### 4x4 Keypad :

| **Wire** | **Keypad Function** | **VSD Squadron Mini Pin** | **Description** |
|----------|----------------------|---------------------------|------------------|
| Wire 2   | Column 3            | PD1                       | Connected to Column 3 |
| Wire 3   | Column 2            | PD2                       | Connected to Column 2 |
| Wire 4   | Column 1            | PD3                       | Connected to Column 1 |
| Wire 5   | Row 4               | PD4                       | Connected to Row 4    |
| Wire 6   | Row 3               | PD6                       | Connected to Row 3    |
| Wire 7   | Row 2               | PD7                       | Connected to Row 2    |
| Wire 8   | Row 1               | PA1                       | Connected to Row 1    |

# DEMO
-
The setup demonstrates the working of the application- "Simple Aritmetic Unit".
Below are the code and video to view the working of the application.
## CODE
```
//Simple arithmetic unit

#include <ch32v00x.h>
#include <ch32v00x_gpio.h>
#include <stdio.h>
#include <stdlib.h>

// Define Keypad Pins
#define R1 GPIO_Pin_5 // PD5
#define R2 GPIO_Pin_2 // PD2
#define R3 GPIO_Pin_3 // PD3
#define R4 GPIO_Pin_4 // PD4
#define C1 GPIO_Pin_4 // PC4
#define C2 GPIO_Pin_5 // PC5
#define C3 GPIO_Pin_6 // PC6
#define C4 GPIO_Pin_7 // PC7

// LCD I2C Address
#define LCD_Address 0x27

// I2C Pins
#define SDA_PIN GPIO_Pin_1
#define SCL_PIN GPIO_Pin_2

// Function Prototypes
void GPIO_INIT(void);
char keypad_get_key(void);
void delay_ms(uint32_t ms);
void lcd_init(void);
void lcd_send_cmd(unsigned char cmd);
void lcd_send_data(unsigned char data);
void lcd_send_string(const char *str);
void i2c_start(void);
void i2c_stop(void);
void i2c_write(unsigned char data);
int get_number_from_keypad(void);

// GPIO Initialization
void GPIO_INIT(void) {
    GPIO_InitTypeDef GPIO_InitStructure;

    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC | RCC_APB2Periph_GPIOD, ENABLE);

    // Initialize rows (R1-R4) as output
    GPIO_InitStructure.GPIO_Pin = R1 | R2 | R3 | R4;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOD, &GPIO_InitStructure);

    // Initialize columns (C1-C4) as input pull-up
    GPIO_InitStructure.GPIO_Pin = C1 | C2 | C3 | C4;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;
    GPIO_Init(GPIOC, &GPIO_InitStructure);

    // Initialize I2C Pins
    GPIO_InitStructure.GPIO_Pin = SDA_PIN | SCL_PIN;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_OD;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOC, &GPIO_InitStructure);

    lcd_init(); // Initialize LCD
}

// Delay Function
void delay_ms(uint32_t ms) {
    while (ms--) {
        for (uint32_t i = 0; i < 4000; i++) {
            __NOP();
        }
    }
}

// Keypad Scan
char keypad_get_key(void) {
    const char keys[4][4] = {
        {'1', '2', '3', 'A'},
        {'4', '5', '6', 'B'},
        {'7', '8', '9', 'C'},
        {'*', '0', '#', 'D'}
    };

    uint16_t rows[] = {R1, R2, R3, R4};
    uint16_t cols[] = {C1, C2, C3, C4};

    for (int row = 0; row < 4; row++) {
        for (int r = 0; r < 4; r++) {
            GPIO_WriteBit(GPIOD, rows[r], Bit_SET);
        }
        GPIO_WriteBit(GPIOD, rows[row], Bit_RESET);

        for (int col = 0; col < 4; col++) {
            if (GPIO_ReadInputDataBit(GPIOC, cols[col]) == RESET) {
                delay_ms(200); // Debounce delay
                return keys[row][col];
            }
        }
    }
    return '\0';
}

// I2C Functions
void i2c_start(void) {
    GPIO_SetBits(GPIOC, SDA_PIN);
    GPIO_SetBits(GPIOC, SCL_PIN);
    delay_ms(1);
    GPIO_ResetBits(GPIOC, SDA_PIN);
    delay_ms(1);
    GPIO_ResetBits(GPIOC, SCL_PIN);
}

void i2c_stop(void) {
    GPIO_ResetBits(GPIOC, SDA_PIN);
    delay_ms(1);
    GPIO_SetBits(GPIOC, SCL_PIN);
    delay_ms(1);
    GPIO_SetBits(GPIOC, SDA_PIN);
}

void i2c_write(unsigned char data) {
    for (int i = 0; i < 8; i++) {
        if (data & 0x80) {
            GPIO_SetBits(GPIOC, SDA_PIN); // Send 1
        } else {
            GPIO_ResetBits(GPIOC, SDA_PIN); // Send 0
        }
        delay_ms(1);
        GPIO_SetBits(GPIOC, SCL_PIN); // Clock high
        delay_ms(1);
        GPIO_ResetBits(GPIOC, SCL_PIN); // Clock low
        data <<= 1;
    }
    // Acknowledge
    GPIO_SetBits(GPIOC, SDA_PIN); 
    delay_ms(1);
    GPIO_SetBits(GPIOC, SCL_PIN);
    delay_ms(1);
    GPIO_ResetBits(GPIOC, SCL_PIN);
}


// LCD Functions
void lcd_init(void) {
    delay_ms(50); // Wait for LCD power-on

    lcd_send_cmd(0x03);
    delay_ms(5);
    lcd_send_cmd(0x03);
    delay_ms(5);
    lcd_send_cmd(0x03);
    delay_ms(5);
    lcd_send_cmd(0x02); // 4-bit mode

    lcd_send_cmd(0x28); // 2 lines, 5x8 matrix
    lcd_send_cmd(0x0C); // Display ON, Cursor OFF
    lcd_send_cmd(0x06); // Entry mode: auto-increment, no shift
    lcd_send_cmd(0x01); // Clear display
    delay_ms(5);
}


void lcd_send_cmd(unsigned char cmd) {
    unsigned char cmd_u = (cmd & 0xF0);
    unsigned char cmd_l = ((cmd << 4) & 0xF0);
    i2c_start();
    i2c_write(LCD_Address << 1);
    i2c_write(cmd_u | 0x0C); // Enable=1, RS=0
    i2c_write(cmd_u | 0x08); // Enable=0
    delay_ms(2);
    i2c_write(cmd_l | 0x0C);
    i2c_write(cmd_l | 0x08);
    delay_ms(2);
    i2c_stop();
}

void lcd_send_data(unsigned char data) {
    unsigned char data_u = (data & 0xF0);
    unsigned char data_l = ((data << 4) & 0xF0);
    i2c_start();
    i2c_write(LCD_Address << 1);
    i2c_write(data_u | 0x0D); // Enable=1, RS=1
    i2c_write(data_u | 0x09); // Enable=0
    delay_ms(2);
    i2c_write(data_l | 0x0D);
    i2c_write(data_l | 0x09);
    delay_ms(2);
    i2c_stop();
}


void lcd_send_string(const char *str) {
    while (*str) {
        lcd_send_data(*str++);
    }
}

// Get Number from Keypad
int get_number_from_keypad(void) {
    char num_str[5] = {0};
    int index = 0;
    char key;

    while (1) {
        key = keypad_get_key();
        if (key >= '0' && key <= '9') {
            num_str[index++] = key;
            lcd_send_data(key);
        } else if (key == '#') {
            return atoi(num_str);
        }
    }
}

int main(void) {
    GPIO_INIT();

    int num1, num2;

    // Prompt for num1
    lcd_send_cmd(0x01);  // Clear screen
    lcd_send_string("Enter Num1: ");
    num1 = get_number_from_keypad();

    // Prompt for num2
    lcd_send_cmd(0x01);  // Clear screen
    lcd_send_string("Enter Num2: ");
    num2 = get_number_from_keypad();

    // Perform Operations
    char result[16];

    // Display Sum
    lcd_send_cmd(0x01);  // Clear screen
    lcd_send_string("ADDITION");            // First line: Operation
    lcd_send_cmd(0xC0);                // Move to second line
    sprintf(result, "=%d", num1 + num2);
    lcd_send_string(result);
    delay_ms(2000);

    // Display Subtraction
    lcd_send_cmd(0x01);  // Clear screen
    lcd_send_string("SUBTRACTION");     // First line: Operation
    lcd_send_cmd(0xC0);                // Move to second line
    sprintf(result, "=%d", num1 - num2);
    lcd_send_string(result);
    delay_ms(2000);

    // Display Multiplication
    lcd_send_cmd(0x01);  // Clear screen
    lcd_send_string("MULTIPLICATION");        // First line: Operation
    lcd_send_cmd(0xC0);                // Move to second line
    sprintf(result, "=%d", num1 * num2);
    lcd_send_string(result);
    delay_ms(2000);

    // Display Division
    lcd_send_cmd(0x01);  // Clear screen
    lcd_send_string("Division");       // First line: Operation
    lcd_send_cmd(0xC0);                // Move to second line
    if (num2 != 0)
        sprintf(result, "=%d", num1 / num2);
    else
        sprintf(result, "Div=Error");
    lcd_send_string(result);
    delay_ms(2000);

    // End of Program
    lcd_send_cmd(0x01);  // Clear screen
    lcd_send_string("Operations Done");

    while (1);
}
```

## Video:
[Video Link](https://1drv.ms/v/s!AodE6TxsOsS6kPx-Yo1-q3fEuc6v-w?e=rpjPT6)

</details>
<details>
<summary><b>Acknowledgment </b>  </summary><br />
 
I would like to extend my heartfelt gratitude to Kunal Ghosh Sir for providing me with this incredible opportunity to explore and learn about RISC-V Architecture through the VSDSquadron Mini internship program.

Throughout the program, I gained invaluable insights, hands-on experience, and a deeper understanding of RISC-V, which has further fueled my enthusiasm for VLSI and processor design.

I am also grateful to VLSI System Design (VSD) for launching such a phenomenal research-focused internship. This program has been a perfect blend of learning, innovation, and practical exposure.

Thank you once again for this learning experience.




