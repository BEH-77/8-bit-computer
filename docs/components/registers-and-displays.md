# Registers and displays

Ihab Mahiaoui implemented accumulator A, B, OUT, binary LEDs, and the signed decimal display. This page follows the labeled components in [Ihab's circuit](../../simulations/sap-1/ihab-mahiaoui/Our_8Bit_Computer.circ). They are also present in Badreddine's assembled canvas.

## Register controls

A, B, and OUT each use two explicitly four-bit Register primitives. The `LOW` register stores bits 0–3 and `HIGH` stores bits 4–7. Each pair loads from the W-Bus and shares the datapath `CLK` input.

| Register labels | Load request | Outputs |
| --- | --- | --- |
| `A_LOW`, `A_HIGH` | `LA_N` | Direct ALU operand and buffered W-Bus output controlled by `EA` |
| `B_LOW`, `B_HIGH` | `LB_N` | Second ALU operand through the XOR bank |
| `OUT_LOW`, `OUT_HIGH` | `LO_N` | Binary LEDs and signed decimal conversion |

The load requests pass through NOT gates before the active-high register enables. A low request loads on a rising clock edge; a high request holds the value. Ihab reports this behavior, and the omitted trigger setting uses the same rising-edge default in the [5.0.0 Register definition](https://github.com/logisim-evolution/logisim-evolution/blob/v5.0.0/src/main/java/com/cburch/logisim/std/memory/Register.java). Wire inspection confirms a common clock and grounded clear inputs for these six registers in both files. A shared CPU reset is not connected to them.

## Accumulator A

A retains the first operand and arithmetic result. Its outputs feed the two adders directly and a bank of eight controlled bus buffers. `EA` is active-high. Disabling A's bus output leaves its stored value available to the ALU; loading and output enabling are separate operations.

Ihab reports a successful storage/bus-output example: high nibble `0x3`, low nibble `0x5`, and `EA=1` produced the expected W-Bus value `0x35` (`00110101`). The exact loading/clock sequence and other bus-driver states were not recorded.

## B register

B holds the second arithmetic operand. Its outputs feed `XOR_B0` through `XOR_B7`; `SU` changes the operand presented to the adders without modifying the stored B value. B has no direct bus-output enable.

Ihab reports basic combined B-register/ALU operation. A separate load/hold test record is still needed. See [ALU](alu.md) for the arithmetic path.

## Output register and binary display

OUT retains a bus value independently of subsequent changes to A or the ALU. The intended `OUT` instruction enables A on the bus and loads this register pair. OUT feeds eight binary LEDs and the decimal-conversion logic; it does not drive the W-Bus.

The LEDs show the raw stored bits. Ihab describes them as D7 through D0, with ON representing 1. Their physical bit order and observed patterns still need an annotated test record. Output capture, retention while A changes, and final LED verification remain pending confirmation.

## Decimal display

The signed display is an extension to the textbook SAP-1 output. It interprets OUT as an eight-bit two's-complement value from -128 to +127.

D7 selects either the original byte or its eight-bit negation through a multiplexer. The selected value is treated as an unsigned magnitude. Two divide-by-10 stages extract units, tens, and hundreds: the first remainder gives units, and the second remainder and quotient give tens and hundreds. Three Bit Extenders reduce the digit paths to four bits for Hex Digit Displays. Expected digits are 0–9; D7 also drives the middle segment of a separate sign display.

The Negator and Dividers omit their widths. Logisim 5.0.0 defaults these to eight bits and uses unsigned division; see [Negator](https://github.com/logisim-evolution/logisim-evolution/blob/v5.0.0/src/main/java/com/cburch/logisim/std/arith/Negator.java) and [Divider](https://github.com/logisim-evolution/logisim-evolution/blob/v5.0.0/src/main/java/com/cburch/logisim/std/arith/Divider.java). Each divisor is an eight-bit constant equal to 10. For -128, eight-bit negation produces `0x80`, interpreted as magnitude 128 by this unsigned path.

These are expected examples supplied by Ihab, not recorded passes:

| OUT bits | Signed value | Expected display |
| --- | --- | --- |
| `00000000` | 0 | `000` |
| `00001000` | 8 | `008` |
| `01111111` | 127 | `127` |
| `11111111` | -1 | `-001` |
| `11111110` | -2 | `-002` |
| `10000000` | -128 | `-128` |

Comprehensive display verification remains pending, including sign behavior, digit order, leading zeros, and the boundary values. This is combinational presentation logic driven by OUT; it does not implement a CPU division instruction. See the [testing record](../testing.md).
