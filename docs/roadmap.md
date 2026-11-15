# Roadmap

Checked items reflect completed work within the stated scope, including each contributor's explicitly reported manual tests. Completed component implementation, documentation, and full-system verification are separate milestones. No historical dates are inferred.

## Phase 1 — SAP-1 Component Development

- [x] Individual circuit implementations: Badreddine's PC, MAR, RAM, IR, Control Matrix, Ring Counter, and 4-to-5 Decoder.
- [x] Initial simulations: Badreddine reports successful individual and combined subsystem tests in Logisim Evolution.
- [x] Initial documentation of the supplied section and project status.
- [x] Ihab's component implementations: accumulator A, B register, adder/subtractor, output register, binary LEDs, and signed decimal display extension.
- [x] Ihab's reported manual accumulator storage/bus-output test and basic arithmetic/B-register–ALU operation.
- [x] Document Ihab's confirmed responsibilities, technical design, reported test scope, and inspected reference-file provenance.
- [ ] Add detailed test evidence and diagrams.
- [ ] Complete reproducible register/ALU test records and confirm standalone B-register coverage.
- [ ] Confirm final output-register and binary-display test results.
- [ ] Verify the signed decimal display across positive, negative, zero, and boundary cases.
- [ ] Record combined verification of Ihab's full six-component section.

## Phase 2 — SAP-1 Integration

- [x] Hand off Ihab's section to Badreddine for integration, as reported by Ihab; this is a handoff milestone, not successful integration.
- [ ] Add the final simulation file in a separately authorized simulation update.
- [ ] Complete and confirm integration of both sections, led by Badreddine.
- [ ] Resolve interface and signal compatibility problems.
- [ ] Agree on shared clock/reset behavior and verify compatibility between the source files' Logisim versions.
- [ ] Verify complete SAP-1 behavior.
- [ ] Execute test programs.
- [ ] Document results.

## Phase 3 — Advanced Computer Architecture

- [ ] Finalize architecture.
- [ ] Define instruction set.
- [ ] Define memory and register specifications.
- [ ] Design datapath and control unit.
- [ ] Implement simulation.
- [ ] Test and verify system.

## Phase 4 — Programming and Hardware Interface

- [ ] Develop assembler.
- [ ] Design Arduino programming interface.
- [ ] Implement memory programming.
- [ ] Verify complete program execution.

The future architecture and specifications are undecided. Later phases describe intended work, not existing capabilities or a fixed schedule.
