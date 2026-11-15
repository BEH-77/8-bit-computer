# Instruction set status

## Current SAP-1 section

The supplied simulation contains five decoder annotations: `LDA`, `ADD`, `SUB`, `OUT`, and `HLT`, beside five four-input AND gates. They identify the instruction names targeted by the decoder; their presence does not establish complete instruction execution on a full computer.

TODO: transcribe the actual opcode-to-output truth table, input bit order, operand format, and timing/control table from the circuit, then attach test evidence. No opcode values or instruction execution guarantees are specified here without that record.

Badreddine reports successful individual decoder/control tests and combined subsystem tests. Full SAP-1 program execution with Ihab's section remains pending; see [testing](testing.md).

## Future computer

The advanced computer's architecture and instruction set are not finalized. TODO: agree on instruction encoding, semantics, operand/addressing rules, and any flags before developing an assembler.
