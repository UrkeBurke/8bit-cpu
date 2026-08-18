# 8-bit CPU

A programmable 8-bit CPU designed and implemented from basic digital logic components in Logisim Evolution.

## Overview

This project originally started as an attempt to apply the knowledge gained from the **Fundamentals of Computer Engineering (Osnovi računarske tehnike)** course at the **School of Electrical Engineering, University of Belgrade (ETF)**. The original goal was to design an operational unit (datapath) and a specialized control unit for a specific computational task from the bottom up.

Out of curiosity, the project gradually evolved beyond its original scope into a fully functional programmable 8-bit CPU designed and implemented from scratch in Logisim Evolution.

The project explores the design of digital systems at both the application-specific and general-purpose levels, from dedicated hardware implementations to a programmable processor capable of executing different instructions and programs.

The fundamental idea behind this project was to build its components from scratch. Alongside the main CPU, the project therefore includes several custom modules that were independently designed and implemented.

Although the main CPU uses Logisim Evolution's built-in RAM component for practicality and optimization, I also implemented a custom RAM module from basic digital logic components as part of the project. The custom implementation was developed primarily for experimentation and optimization rather than being required by the CPU architecture.

## Features

### Custom Modules

The project includes custom-built combinational and sequential logic modules implemented from basic digital logic components, including:

- Decoders and Multiplexers
- an ALU
- Flip-flops
- Registers
- Other supporting modules

### Specialized Processing Units

The project includes two dedicated processing units, each designed for a specific computational task. Each unit consists of:

- A custom operational unit (datapath) - fixed for both units
- A dedicated control unit

The two specialized units implement:

- `ADDABS2`
- `MUL2`

### Programmable 8-bit CPU

Finally, the project includes a general-purpose programmable 8-bit CPU featuring:

- 8-bit datapath
- Custom instruction set
- Direct and indirect addressing
- Conditional and unconditional jumps
- Two-phase instruction execution

## Architecture

The CPU consists of the following main components:

- Program Counter (PC)
- Instruction Register (IR)
- Register File (Registers A and B)
- Arithmetic Logic Unit (ALU)
- Control Unit
- 256 × 8-bit RAM

Instructions are executed in two phases:

- **Phase F0:** Instruction fetch
- **Phase F1:** Instruction execution

## Instruction Format

Each instruction is 8 bits wide:

```text
┌────────────┬────────────┐
│   OPCODE   │  OPERAND   │
│   4 bits   │   4 bits   │
└────────────┴────────────┘
```
## Instruction Set

| Mnemonic | Opcode | Description |
|----------|--------|-------------|
| `STA (B)` | `0000` | Store A at the memory address stored in B |
| `LDA X` | `0001` | Load A from memory address X |
| `LDB X` | `0010` | Load B from memory address X |
| `STA X` | `0011` | Store A at memory address X |
| `INC` | `0100` | Increment A |
| `ADD` | `0101` | Add B to A |
| `DEC` | `0110` | Decrement A |
| `SUB` | `0111` | Subtract B from A |
| `AND` | `1000` | Bitwise AND of A and B |
| `OR` | `1001` | Bitwise OR of A and B |
| `JMP (B)` | `1010` | Jump to the address stored in B |
| `JZ (B)` | `1011` | Jump to B if A is zero |
| `JMP X` | `1100` | Jump to address X |
| `JZ X` | `1101` | Jump to X if A is zero |
| `LDA (B)` | `1110` | Load A from the address stored in B |
| `HLT` | `1111` | Halt program execution |

## Addressing Modes

The CPU supports both direct and indirect addressing.

- **Direct addressing:** The 4-bit operand specifies a memory address from `0x00` to `0x0F`.
- **Indirect addressing:** Register B contains an 8-bit memory address, allowing access to the entire memory space from `0x00` to `0xFF`.

Indirect addressing allows instructions `STA (B)`, `JMP (B)`, `JZ (B)`, and `LDA (B)` to access all 256 memory locations.

## Memory

The CPU uses a `256 × 8-bit` RAM.

Each memory location stores one 8-bit value and is addressed using an 8-bit address.

Direct addressing can access the first 16 memory locations (`0x00`–`0x0F`), while indirect addressing through register B allows access to the entire memory space (`0x00`–`0xFF`).

## Project File

The CPU was designed and implemented using [Logisim Evolution](https://github.com/logisim-evolution/logisim-evolution). The version used was v4.1.0, and the project was not tested on any other versions.

The complete Logisim Evolution project is available in `8bit_cpu.circ`.
