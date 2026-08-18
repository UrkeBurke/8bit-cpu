# 8-bit CPU

A programmable 8-bit CPU designed and implemented from basic digital logic components in Logisim Evolution.

## Overview

This project implements a fully functional programmable 8-bit CPU built in Logisim Evolution.

The CPU features an 8-bit datapath, a custom instruction set, a control unit, an ALU, registers, a program counter, an instruction register, and 256 × 8-bit RAM.

## Features

- 8-bit datapath
- Custom programmable instruction set
- Program Counter (PC)
- Instruction Register (IR)
- Register File (Registers A and B)
- Arithmetic Logic Unit (ALU)
- Control Unit
- 256 × 8-bit RAM
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
