# Multiplication

A program for the 8-bit CPU that calculates the product of two non-negative whole numbers.

## Input

The program takes two non-negative whole numbers as input:

- `X`
- `Y`

The input values are stored in memory locations `0` and `1`.

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

\[
X \times Y =
\underbrace{X + X + \dots + X}_{Y\text{ times}}
\]

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

## Machine Code

The complete machine code is provided in [`Multiplication.txt`](./Multiplication.txt).

```text
v2.0 raw
XX YY 00 20 11 DD 12 50 32 11 60 31 C5 F0
```

The machine code is designed to be reusable.

To change the input values, replace `XX` and `YY` with the desired values in hexadecimal. The remaining instructions should not be modified.

Examples:

- `5` → `05`
- `11` → `0B`
- `56` → `38`

For example, to calculate:

```text
5 × 11
```
the beginning of the machine code should be: 05 0B 00 ...
