# Multiplication

A program for the 8-bit CPU that calculates the product of two non-negative whole numbers.

## Input

The program takes two non-negative whole numbers as input:

- `X`
- `Y`

The input values are stored in memory locations `0` and `1`, respectively.

It is recommended to use the smaller value as `Y`, since the multiplication is performed using repeated addition.

## Output

The result `X × Y` is stored in memory location `2`.

## Memory Layout

| Address | Description |
|---------|-------------|
| `0` | Input `X` |
| `1` | Input `Y` |
| `2` | Result |

## Algorithm

The multiplication is performed using repeated addition.

The program repeatedly adds `X` to the accumulator while decrementing `Y`:

**X × Y = X + X + ... + X** (Y times)

The algorithm is:

1. Load `X` into register `B`.
2. Load `Y` into register `A`.
3. If `Y = 0`, halt.
4. Load the current result from memory location `2`.
5. Add `X` to the result.
6. Store the updated result back into memory location `2`.
7. Load `Y`.
8. Decrement `Y`.
9. Store the updated `Y` back into memory location `1`.
10. Repeat from step 3.
11. Halt when `Y = 0`.

### Pseudocode

The following shows the contents of memory, where each number represents a memory address:

| Address | Instruction / Data | Description |
|--------:|--------------------|-------------|
| `0` | `X` | Input value X |
| `1` | `Y` | Input value Y |
| `2` | `0` | Sum `S`, initially 0 |
| `3` | `LDB 0` | B = X |
| `4` | `LDA 1` | A = Y |
| `5` | `JZ 13` | If A = 0, jump to address 13 |
| `6` | `LDA 2` | A = S |
| `7` | `ADD` | A = A + B = S + X |
| `8` | `STA 2` | MEM[2] = A = S + X |
| `9` | `LDA 1` | A = Y |
| `10` | `DEC` | A = A − 1 = Y − 1 |
| `11` | `STA 1` | MEM[1] = A = Y − 1 |
| `12` | `JMP 5` | Jump back to address 5 |
| `13` | `HLT` | Halt program execution |

## Machine Code

The following machine code is designed to be reusable.

```text
v2.0 raw
XX YY 00 20 11 DD 12 50 32 11 60 31 C5 F0
```

To change the input values, replace `XX` and `YY` with the desired values in hexadecimal. The remaining instructions should not be modified.

Examples:

- `5` → `05`
- `11` → `0B`
- `56` → `38`

For example, to calculate:

```text
5 × 11
```
the beginning of the machine code should be:
```
05 0B 00 ...
```

An example machine code is provided in [`multiplication.txt`](./multiplication.txt), where the numbers being multiplied are 13 and 9.

## Running the Program

1. Set the clock to any desired frequency.
2. Set `RESET = 1` and let the clock tick at least 4 times (2 complete cycles).
3. Load the modified machine code into the RAM:
   - Right-click the RAM component.
   - Select the option to load the machine code file.
   - Select [`multiplication.txt`](./multiplication.txt).
4. Set the `START_FROM` input to `3` (`00000011`).
5. Set `RESET = 0` to release the CPU from reset and start program execution.
6. The program will execute automatically.
7. When the program finishes, the LED connected to the Control Unit's `HLT` output will turn on.
8. To run the program again, repeat the procedure from step 2.

The result is stored in memory location `2`.
