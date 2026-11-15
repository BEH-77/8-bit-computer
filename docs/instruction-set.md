# Instruction set

The decoder in [Badreddine's circuit](../simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ) targets five SAP-1 instructions. The table describes their intended effects, not verified execution of a complete computer.

| Instruction | Intended operation | Datapath action |
| --- | --- | --- |
| `LDA` | Load A from memory | Address through MAR; memory value through the W-Bus into A |
| `ADD` | Add a memory operand to A | Load B, select addition, then load the ALU result into A |
| `SUB` | Subtract a memory operand from A | Load B, select subtraction, then load the ALU result into A |
| `OUT` | Copy A to the output register | Enable A on the bus and load OUT |
| `HLT` | Stop instruction execution | Halt the control/clock sequence |

IR has eight bits of storage split across two four-bit registers. The SAP-1 model uses a four-bit opcode and a four-bit address field; the decoder input order, actual opcode truth table, and field routing still need to be transcribed from this implementation. Opcode values and control-cycle counts are therefore not yet published as a programming specification.

Badreddine reports successful decoder/control and subsystem tests. Ihab reports basic arithmetic operation, with `SU=0` selecting addition and `SU=1` subtraction. Neither report establishes complete fetch/decode/execute sequences in the assembled circuit. See [control unit](components/control-unit.md), [ALU](components/alu.md), and [testing](testing.md).

Before writing test programs, record the decoder truth table and the timing-state/control table, including halt and unrecognized-opcode behavior. The future architecture's instruction set is undecided. Decimal-display division does not add an instruction to SAP-1.
