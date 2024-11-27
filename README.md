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
<summary><b>Task 2:</b> SPIKE simulation and Debugging of C code Using Spike  </summary>   
<br>
 

![Task-2-1](https://github.com/user-attachments/assets/9fa16c2f-6699-4426-bc1a-f68c3153afd5)

Debugging using the command

$spike -d pk sum1ton.o

Assembly Language :-

![Task-2-2](https://github.com/user-attachments/assets/cdf273bd-d94d-4b1f-92af-af6bbfb16c7d)

Debugger:

![Task-2-3](https://github.com/user-attachments/assets/663ef5cf-651f-44a8-b6e5-33ecd90bb569)


![Task-2-4](https://github.com/user-attachments/assets/e864276a-1242-49ab-bfc0-9db3db0755ce)
![Task-2-4(calc)](https://github.com/user-attachments/assets/2056bdb2-7875-4978-aeb6-441cf3594ab9)

At address `100b4` the value of stack point `sp`= `0x0000003ffffffb50` 
after completion of instruction`sp, sp, -16` = `0x0000003ffffffb40`
By the above calculation :- Difference between the values at stack point in both the cases = 10 (decimal)

At address '100d8' the value of sum of the program is returned (= 55).

## About instructions used:

LUI (LOAD UPPER IMMEDIATE):
This instruction is a key feature in RISC-V architecture.. It is used to load a 20-bit immediate value into the upper 20 bits of a register, while setting the lower 12 bits to zero.
Format - LUI rd, immediate [ rd- destination register, immediate- 20-bit immediate value to be loaded]
The 20- bit immediate value is shifted left by 12 bits(appended with 12 zeros). 
The lower 12 bits of the destination register are set to zero. The resulting 32-bit value is stored in rd.

ADDI
This instruction is a common operation in RISC-V architecture.It performs an addition between a register and a sign-extended immediate value, storing the result in a destination register.
Format-ADDI rd, rs1, immediate (rd- destination register, rs- source register, immediate-


--

</details>
***


 
