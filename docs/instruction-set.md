# Instruction set status

## Current SAP-1 section

The supplied simulation contains five decoder annotations: `LDA`, `ADD`, `SUB`, `OUT`, and `HLT`, beside five four-input AND gates. They identify the instruction names targeted by the decoder; their presence does not establish complete instruction execution on a full computer.

TODO: transcribe the actual opcode-to-output truth table, input bit order, operand format, and timing/control table from the circuit, then attach test evidence. No opcode values or instruction execution guarantees are specified here without that record.

Badreddine reports successful individual decoder/control tests and combined subsystem tests. Full SAP-1 program execution with Ihab's section remains pending; see [testing](testing.md).

## Ihab's implemented datapath and instruction roles

Ihab has completed the accumulator A, B register, adder/subtractor, output register, binary display, and decimal display. Static inspection of his supplied reference establishes these components, but not complete instruction execution. The reference lacks the complete decoder/timing/control-matrix section.

| Target instruction | Role of Ihab's components in the SAP-1 model | Execution status |
| --- | --- | --- |
| `LDA` | A retains the value transferred from memory through the bus | Complete fetch/decode/load sequence not verified |
| `ADD` | B retains the memory operand; the adder/subtractor forms A+B for transfer back to A | Arithmetic structure documented; complete instruction not verified |
| `SUB` | B retains the memory operand; XOR conditioning and carry input select A−B for transfer back to A | Arithmetic structure documented; complete instruction not verified |
| `OUT` | OUT captures A's bus value and supplies the binary/decimal displays | Output structure documented; complete instruction not verified |
| `HLT` | Requires the control/clock subsystem to stop execution | Complete system halt not verified |

This table connects implemented hardware to intended instruction roles; it is not an opcode or microinstruction specification. The [adder/subtractor page](components/alu.md) records `SU` operation selection and `EU` result enabling. The [register/display page](components/other-components.md) records load and output controls. Decimal-conversion Dividers are display circuitry and do not implement a division instruction.

TODO: reconcile the actual decoder truth table with the control sequence, agree on signal polarities and timing, and record instruction/program test results after integration. No additional instructions, flags, opcode values, or cycle counts are claimed.

## Future computer

The advanced computer's architecture and instruction set are not finalized. TODO: agree on instruction encoding, semantics, operand/addressing rules, and any flags before developing an assembler.
