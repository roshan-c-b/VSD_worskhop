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
...
LUI (LOAD UPPER IMMEDIATE):
This instruction is a key feature in RISC-V architecture. It is used to load a 20-bit immediate value into the upper 20 bits of a register, while setting the lower 12 bits to zero.

Format - LUI rd, immediate [ rd- destination register, immediate- 20-bit immediate value to be loaded]
The 20- bit immediate value is shifted left by 12 bits(appended with 12 zeros). 
The lower 12 bits of the destination register are set to zero. 

ADDI
This instruction is a common operation in RISC-V architecture.It performs an addition between a register and a sign-extended immediate value, storing the result in a destination register.

Format- ADDI rd, rs1, immediate (rd- destination register, rs- source register, immediate- the immediate value to be added).

--
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
-

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
***


 
