# Multiplication

A program for the 8-bit CPU that calculates the product of two non-negative integers.

## Input

Two non-negative integers:

- `X`
- `Y`

The input values are stored in memory locations `0` and `1`.

## Output

The product `X × Y` is stored in memory location `2`.

The program uses repeated addition:

\[
X \times Y = \underbrace{X + X + \dots + X}_{Y\text{ times}}
\]

For efficiency, it is recommended to use the smaller value as `Y`.

## Memory Layout

| Address | Description |
|---------|-------------|
| `0` | `X` |
| `1` | `Y` |
| `2` | Result / accumulator |

## Program

The program is provided as machine code in [`Multiplication.txt`](./Multiplication.txt).

The machine code is reusable. To change the input values, replace `XX` and `YY` with the desired hexadecimal values.

For example:

```text
X = 5  → 05
Y = 11 → 0B
X = 56 → 38
