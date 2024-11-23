# VSDSquadron Mini Internship November_2024
 The goal of the VSDSquadron Mini-Internship program is to use open-source tools to introduce participants to RISC-V architecture and VLSI chip design. Using the VSDSquadron Mini RISC-V Development Board, the program's central component, it offers a practical learning experience.

This development board has a 32-bit RISC-V CPU with a clock speed of 24MHz, 16KB of flash memory, and 2KB of SRAM. With its 15 GPIO pins for hardware interface and support for SPI, USART, and I2C, it may be used for a wide range of projects. Participants in the program develop and test hardware applications to use their understanding of the RISC-V ecosystem.<br />



***

<details>
<summary><b>Task 1:</b>Sample C program with GNU GCC and RISC GCC compiler and understanding the assembly code. </summary><br />
  

  **1.Command for Installing Leafpad**<br />
  ```
  $ sudo apt install leafpad
  ```
  
  **2.Command for Opening Leafpad**<br />
  ```
  $ cd
  $ leafpad filename.c &
  ```
  ![git-1](https://github.com/user-attachments/assets/882a740c-66b9-4aa8-9a4b-b54c03f15fb2)

  
  **3.Commands to Compiling and View the Output**<br />
  ```
  $ gcc filename.c
  $ cat filename.c
  $ ./a.out
  ```
  ![git-2](https://github.com/user-attachments/assets/8fc91ce4-b25e-411c-bc89-cb6063bc6f75)
  **4.Command for Compiling the Code using RISCV Compiler**<br />
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

  Same number of instructions as the previous command.

  ```

  
</details>

***


 
