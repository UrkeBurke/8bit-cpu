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
