# Fibonacci

A program for the 8-bit CPU that calculates the N-th Fibonacci number.

The Fibonacci sequence is defined as:

- `F₀ = 0`
- `F₁ = 1`
- `Fₙ = Fₙ₋₁ + Fₙ₋₂`

## Input

The program takes one non-negative whole number as input:

- `N`

The input value is stored in memory location `12`.

## Output

The result `Fₙ` is stored in memory location `13`. Additionally, the (N+1)-st Fibonacci number `Fₙ₊₁` is stored in memory location `14`.

## Memory Layout

| Address | Description |
|---------|-------------|
| `12` | Input `N` |
| `13` | `Fₙ` |
| `14` | `Fₙ₊₁` |

The initial values are:

```text
MEM[13] = 0
MEM[14] = 1
```

## Algorithm

The program calculates the N-th and (N+1)-st Fibonacci numbers using an iterative approach.

The algorithm maintains two consecutive Fibonacci numbers in memory:

- `MEM[13]` stores the current `Fₙ`
- `MEM[14]` stores the current `Fₙ₊₁`

For each iteration, the program:

1. Checks whether `N = 0`.
2. Decrements `N`.
3. Moves `Fₙ₊₁` into the position of `Fₙ`.
4. Calculates the next Fibonacci number by adding the previous two values.
5. Stores the new pair of consecutive Fibonacci numbers.
6. Repeats until `N = 0`.

When the program halts, `MEM[13]` contains `Fₙ` and `MEM[14]` contains `Fₙ₊₁`.

### Pseudocode

The following shows the contents of memory, where each number represents a memory address:

| Address | Instruction / Data | Description |
|--------:|--------------------|-------------|
| `0` | `LDA 12` | A = MEM[12] = N |
| `1` | `JZ 11` | If A = 0, jump to address 11 |
| `2` | `DEC` | A = A − 1 = N − 1 |
| `3` | `STA 12` | MEM[12] = A = N − 1 |
| `4` | `LDA 14` | A = MEM[14] |
| `5` | `LDB 13` | B = MEM[13] |
| `6` | `STA 13` | MEM[13] = A |
| `7` | `ADD` | A = A + B |
| `8` | `STA 14` | MEM[14] = A |
| `9` | `LDA 12` | A = MEM[12] |
| `10` | `JMP 1` | Jump back to address 1 |
| `11` | `HLT` | Halt program execution |
| `12` | `N` | Input value N |
| `13` | `0` | Initial value of Fₙ |
| `14` | `1` | Initial value of Fₙ₊₁ |

## Machine Code

The following machine code is designed to be reusable.

```text
v2.0 raw
1C DB 60 3C 1E 2D 3D 50 3E 1C C1 F0 NN 00 01 00
```

To change the input value, replace `NN` with the desired value in hexadecimal. The remaining instructions should not be modified.

Examples:

- `5` → `05`
- `11` → `0B`

For example, to calculate the fifth Fibonacci number the end of the machine code should be:
```
... 05 00 01 00
```

An example machine code is provided in [`fibonacci.txt`](./fibonacci.txt), where the sixth Fibonacci number is calculated.

## Running the Program

1. Set the clock to any desired frequency.
2. Set `RESET = 1` and let the clock tick at least 4 times (2 complete cycles).
3. Load the modified machine code into the RAM:
   - Right-click the RAM component.
   - Select the option to load the machine code file.
   - Select [`multiplication.txt`](./multiplication.txt).
4. Set the `START_FROM` input to `0` (`00000000`).
5. Set `RESET = 0` to release the CPU from reset and start program execution.
6. The program will execute automatically.
7. When the program finishes, the LED connected to the Control Unit's `HLT` output will turn on.
8. To run the program again, repeat the procedure from step 2.

The result is stored in memory location `13`.
