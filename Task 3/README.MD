**RISC-V Instruction Analysis**<br>
This repository focuses on analyzing and decoding 15 distinct RISC-V instructions extracted from application code.
Each instruction is categorized based on its type (R, I, S, B, U, J) and represented by its 32-bit binary encoding.

**Overview**<br>
The primary objectives of this project are to:
Explore the various RISC-V instruction types: R, I, S, B, U, and J.
Extract and classify 15 unique RISC-V instructions from the riscv-objdump output of the application code.
Decode these instructions into their corresponding 32-bit binary representations.<br>

**1. auipc gp, 0x13**

opcode: 0010111 (7 bits)

immediate (imm): 0x13 = 0000 0000 0001 0011 (20 bits)

destination register (rd): gp (3, 5 bits) = 00011

32-bit Code: 0000 0000 0001 0011 | 00011 | 0010111
