# ArraySum

A program for the 8-bit CPU that calculates the sum of an array with an arbitrary number of elements `N`.

## Input

The program takes one non-negative whole number `N` as input and an array of `N` elements:

The input value `N` is stored in memory location `0`, and the array begins from the memory location `32`.

## Output

The result is stored in memory location `15`.

## Memory Layout

| Address | Description |
|---------|-------------|
| `0` | Input `N` |
| `15` | Sum of the elements |
| `32` | Start of the array |

The initial value of the sum is `0`:

```text
MEM[15] = 0
```

## Algorithm

The program calculates the sum of all elements in an array using an iterative approach.

The memory is divided into three logical zones:

- **Fixed Zone:** The first 16 memory locations (`0`–`15`) are reserved for fixed data and control information.
- **Code Zone:** The program instructions start at memory location `16`.
- **Higher Zone:** The array is stored starting at memory location `32` and extends for `N` elements.

The program uses an 8-bit pointer stored in the Fixed Zone to keep track of the current array element.

For each iteration, the program:

1. Loads the address of the current array element.
2. Loads the element using indirect addressing.
3. Adds the element to the current sum.
4. Stores the updated sum.
5. Advances the array pointer to the next element.
6. Decrements the number of remaining elements.
7. Repeats until all elements have been processed.
8. Halts when the number of remaining elements reaches zero.

The final sum is stored in memory location `15`.

### Pseudocode

The following shows the memory organization and instructions used by the program.

#### Fixed Zone

| Address | Instruction / Data | Description |
|--------:|--------------------|-------------|
| `0` | `N` | Number of elements remaining |
| `1` | `32`| Address of the current array element |
| `2` | `31` | Address of the `HLT` instruction |
| `3` | `16` | Address of the beginning of the Code Zone |
| `4`–`14` | — | Reserved |
| `15` | `0` | Sum |

#### Code Zone

| Address | Instruction | Description |
|--------:|-------------|-------------|
| `16` | `LDB 1` | B = MEM[1] = address of current array element |
| `17` | `LDA (B)` | A = MEM[MEM[B]] = current array element |
| `18` | `LDB 15` | B = MEM[15] = current sum |
| `19` | `ADD` | A = A + B = updated sum |
| `20` | `STA 15` | MEM[15] = A = updated sum |
| `21` | `LDA 1` | A = current array address |
| `22` | `INC` | A = A + 1 = address of next element |
| `23` | `STA 1` | MEM[1] = A |
| `24` | `LDA 0` | A = number of remaining elements |
| `25` | `DEC` | A = A − 1 |
| `26` | `STA 0` | MEM[0] = A |
| `27` | `LDB 2` | B = MEM[2] = address of HLT |
| `28` | `JZ (B)` | If A = 0, jump to HLT |
| `29` | `LDB 3` | B = MEM[3] = address of Code Zone |
| `30` | `JMP (B)` | Jump to the beginning of the Code Zone |
| `31` | `HLT` | Halt program execution |

#### Higher Zone

| Address | Description |
|--------:|-------------|
| `32` | First array element |
| `33` | Second array element |
| `...` | ... |
| `31 + N` | Last array element |

The Higher Zone generally has neither a fixed starting nor ending address. It begins immediately after the Code Zone and extends for as many memory locations as required by the array.

Its starting address therefore depends on the length of the program.

In this implementation, the Code Zone occupies memory locations `16`–`31`, so the Higher Zone starts at `32`.

## Machine Code

The following machine code is designed to be reusable.

```text
v2.0 raw
NN 20 1F 10 00 00 00 00 00 00 00 00 00 00 00 00
21 E0 2F 50 3F 11 40 31 10 60 30 22 B0 23 A0 F0
AR 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
```

To change the input value, replace `NN` with the desired value in hexadecimal. Enter `N` numbers in hexadecimal starting from the `AR` label in the code. The remaining instructions should not be modified.

Examples:

- `5` → `05`
- `11` → `0B`

For example, to calculate the sum of the array `1, 2, 3` the machine code should look like:
```
03 20 1F ... A0 F0 01 02 03
```

An example machine code is provided in [`arraySum.txt`](./arraySum.txt), where the array is `4, 12, 22, 3, 9`.

## Running the Program

1. Set the clock to any desired frequency.
2. Set `RESET = 1` and let the clock tick at least 4 times (2 complete cycles).
3. Load the modified machine code into the RAM:
   - Right-click the RAM component.
   - Select the option to load the machine code file.
   - Select [`arraySum.txt`](./arraySum.txt).
4. Set the `START_FROM` input to `16` (`00010000`).
5. Set `RESET = 0` to release the CPU from reset and start program execution.
6. The program will execute automatically.
7. When the program finishes, the LED connected to the Control Unit's `HLT` output will turn on.
8. To run the program again, repeat the procedure from step 2.

The result is stored in memory location `15`.

