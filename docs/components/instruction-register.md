# Instruction Register (IR)

Badreddine El Habra implemented IR with two four-bit Register primitives, giving eight bits of instruction storage. In [his circuit](../../simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ), the pair sits below RAM. A four-bit controlled buffer provides the address-field output path, while a four-bit path leads toward the instruction decoder.

IR is intended to capture an instruction from the memory/W-Bus path and hold it while the control unit executes it. The SAP-1 model separates the byte into an opcode and an address field. The precise assignment and bit order of the two registers still need to be recorded against the decoder truth table.

| Annotation | Intended role |
| --- | --- |
| `Li` | Load the instruction |
| `Ei` | Enable the address field onto the transfer path |
| `CLK`, `CLR` | Clock and clear the stored instruction |

Both registers omit a trigger override and therefore use Logisim 4.1.0's rising-edge default. This does not by itself define the input clock phase or the load/enable polarities; those depend on the surrounding wiring. See the [Register definition](https://github.com/logisim-evolution/logisim-evolution/blob/v4.1.0/src/main/java/com/cburch/logisim/std/memory/Register.java).

Badreddine reports successful individual IR and combined subsystem tests. A reproducible fetch/load/hold procedure, control polarities, and opcode mapping remain to be documented. See [instruction set](../instruction-set.md) and [testing](../testing.md).
