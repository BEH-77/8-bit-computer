# Adder/subtractor (ALU)

## Purpose and implementation status

**Implemented by Ihab Mahiaoui**, who confirmed this component as part of his completed work. It supplies the SAP-1 arithmetic path for addition and subtraction of the accumulator A and B register values.

The implementation record combines Ihab's technical description with static inspection of `Our_8Bit_Computer.circ`, supplied for documentation and identifying Logisim Evolution 5.0.0. The circuit has not yet been added to the repository; see [source provenance](../../simulations/sap-1/ihab-mahiaoui/README.md). Ihab reports basic arithmetic and combined B-register/ALU operation working; the scope is recorded below.

## Width, inputs, outputs, and controls

| Interface | Width | Role |
| --- | --- | --- |
| Accumulator A | 8 bits, split into two 4-bit paths | First arithmetic operand |
| B register | 8 bits, split into individual bits and regrouped | Second operand, conditionally complemented by XOR gates |
| `SU` | 1 bit | Selects addition (`0`) or subtraction (`1`) through the XOR bank and initial carry input |
| Arithmetic result | 8 bits, from two 4-bit adders | Result routed toward the shared transfer path through controlled buffers |
| `EU` | 1 bit | Active-high enable for the eight result buffers |

This is a combinational datapath. The A and B registers retain its operands; loading the result into A is a separate register operation. See [registers and displays](other-components.md).

## Internal logic and operation

- Two built-in Adders at `(2210,320)` and `(2210,390)` are explicitly configured to four bits each. Ihab describes them as `ALU_LOW` (bits 0–3) and `ALU_HIGH` (bits 4–7); these are descriptive names, not serialized component labels in the reference XML.
- Eight XOR gates are labeled `XOR_B0` through `XOR_B7`. `SU` reaches one input of each gate and the low-order adder's carry input.
- The low-order carry output is wired to the high-order carry input. A's low and high register outputs reach the corresponding adder operand inputs.
- Two four-bit result splitters feed eight controlled buffers; their enable pins share `EU`.

The implemented design equation is `R = (A + (B XOR {8{SU}}) + SU) mod 256`, where `{8{SU}}` repeats `SU` across eight bits. `SU=0` selects addition; `SU=1` selects two's-complement subtraction. Ihab confirms this arrangement, and static wiring inspection supports it. Port interpretation follows the version-matched [Adder source](https://github.com/logisim-evolution/logisim-evolution/blob/v5.0.0/src/main/java/com/cburch/logisim/std/arith/Adder.java); buffer enabling follows the [Controlled Buffer source](https://github.com/logisim-evolution/logisim-evolution/blob/v5.0.0/src/main/java/com/cburch/logisim/std/gates/ControlledBuffer.java). The formula is a design description, not a comprehensive test result.

## Integration and design decisions

Ihab's design uses a pair of four-bit adders and a shared XOR/adder path for both operations. A and B feed the arithmetic logic continuously; `EU` controls the W-Bus output drivers rather than computation. Only one W-Bus source should be enabled at a time. The final carry-out is unused in Ihab's section, and no dedicated carry/overflow-status register or overflow flag is implemented.

Badreddine's control matrix has annotations `Su` and `Eu`. They are candidate control interfaces for `SU` and `EU`, but capitalization and similar names do not establish compatible polarity, timing, or a completed connection. Before integration, confirm the bit ordering and ensure only the intended source drives the shared bus.

## Testing and limitations

**Basic arithmetic functionality manually tested and reported working by Ihab.** He reports that an incorrect connection involving the low/high nibble paths caused unexpected results during construction; he corrected it and subsequently reported working arithmetic. B-register/ALU combined operation was also manually tested. No comprehensive test matrix, operand list, or measured timing evidence was supplied. This documentation update did not independently execute the simulation; see [testing](../testing.md).

Results wrap modulo 256. The arithmetic supports unsigned or two's-complement interpretation of the same eight bits, but signed results can overflow without a status flag. Decimal display conversion does not change the arithmetic or add instructions. TODO: record reproducible operand/control sequences, expected and observed results, carry-chain and overflow boundary cases, bus-enable checks, and an annotated bit-level diagram. Full control-unit integration and complete instruction/program execution remain pending confirmation.
