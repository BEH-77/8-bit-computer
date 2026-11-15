# Adder/subtractor (ALU)

Ihab Mahiaoui implemented the eight-bit arithmetic path using two four-bit adders, eight XOR gates, and controlled output buffers. The description below follows [Ihab's circuit](../../simulations/sap-1/ihab-mahiaoui/Our_8Bit_Computer.circ); the same component arrangement is present on Badreddine's assembled canvas.

## Operation

| Input or output | Function |
| --- | --- |
| A, B | Eight-bit stored operands, each split into low and high nibbles |
| `SU` | `0` selects addition; `1` selects subtraction |
| Result | Eight-bit sum or difference |
| `EU` | Active-high enable for the result's W-Bus buffers |

The low-nibble adder's carry output feeds the high-nibble adder. `SU` drives both the `XOR_B0`–`XOR_B7` gates and the low adder's carry input. The resulting operation is:

```text
SU = 0: result = (A + B) mod 256
SU = 1: result = (A + NOT B + 1) mod 256 = (A - B) mod 256
```

A and B feed the arithmetic logic continuously. `EU` controls bus access, not computation; loading the result into A is a separate clocked operation. Only one source should drive the W-Bus during a transfer.

The pair of adders is explicitly four bits each. Carry-port interpretation follows the [Logisim 5.0.0 Adder definition](https://github.com/logisim-evolution/logisim-evolution/blob/v5.0.0/src/main/java/com/cburch/logisim/std/arith/Adder.java), and output-enable behavior follows the [Controlled Buffer definition](https://github.com/logisim-evolution/logisim-evolution/blob/v5.0.0/src/main/java/com/cburch/logisim/std/gates/ControlledBuffer.java).

The final carry-out is unused and there is no carry/overflow flag register. Values can be interpreted as unsigned or two's complement, but arithmetic wraps at eight bits in either case. The decimal display does not change this behavior.

## Testing and integration

Ihab reports working basic arithmetic after correcting a low/high nibble connection, and successful basic operation with B connected to the XOR/adder path. The report does not include operand vectors or boundary results. No exhaustive arithmetic pass is claimed.

The assembled circuit still has manual `SU` and `EU` pins rather than connections from the control matrix. Pending checks include carry propagation between nibbles, subtraction and wraparound, bus enabling, and loading the result back into A. See [registers and displays](registers-and-displays.md) and [testing](../testing.md).
