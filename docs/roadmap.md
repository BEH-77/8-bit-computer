# Roadmap

## Completed component work

- Badreddine's PC, MAR, RAM, IR, ring counter, decoder, and control matrix are implemented. He reports successful individual and combined subsystem tests.
- Ihab's A/B/OUT registers, ALU, binary LEDs, and signed decimal display are implemented. He reports successful accumulator and basic arithmetic/B-register–ALU tests.
- Both circuit files are available, with both sections present on Badreddine's current canvas.

## Current work: integration and verification

- [ ] Connect the control matrix to the datapath and resolve signal polarity, clocking, reset, and bus ownership.
- [ ] Choose and test a Logisim version for the combined circuit; reconcile RAM trigger settings.
- [ ] Record the opcode truth table, control timing, and memory-loading procedure.
- [ ] Add reproducible component/subsystem results and confirm standalone B-register and final output/display behavior.
- [ ] Run complete instructions and test programs with expected and observed results.

Badreddine leads integration following Ihab's reported handoff. Having both sections on one canvas is progress toward integration, not a complete-system test result. Detailed checks are listed in [testing](testing.md).

## Future work

After SAP-1 verification, define a more advanced eight-bit architecture: instruction set, registers, memory, datapath, and control. Implement and test that design before developing an assembler or Arduino programming interface. These remain planned work, with no fixed specifications or schedule.

The contributors also need to agree on a project license.
