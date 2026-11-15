# Changelog

A simplified Keep a Changelog record. `Unreleased` groups imported work and repository preparation; it does not imply separate historical commits, dates, or releases.

## Unreleased

### Previously completed SAP-1 simulation work

#### Badreddine El Habra

Reported by Badreddine El Habra; the supplied XML contains the corresponding circuit regions.

- Implemented the Program Counter, MAR, RAM, and Instruction Register.
- Implemented the Control Matrix, Ring Counter, and 4-to-5 Decoder.
- Successfully tested each component individually in Logisim Evolution, according to Badreddine's manual testing report.
- Successfully tested the implemented components together in one simulation, according to the same report.

#### Ihab Mahiaoui

Reported by Ihab in his contribution confirmation and technical/testing notes; the separately supplied `Our_8Bit_Computer.circ` was inspected as a documentation reference. These development activities predate this documentation update; their dates and historical Git commits are not specified.

- Implemented eight-bit accumulator A, B register, and output register using pairs of four-bit registers and active-low load controls.
- Implemented an eight-bit adder/subtractor using two four-bit adders, eight XOR gates, carry chaining, and controlled W-Bus output buffers.
- Implemented binary LED output and a signed decimal visualization extension with sign/magnitude handling and decimal digit extraction.
- Manually tested accumulator storage/bus output with expected and observed `0x35`, according to Ihab's report.
- Reported working basic arithmetic after correcting low/high nibble wiring, and basic combined B-register/ALU operation; no exhaustive verification is claimed.
- Sent his section to Badreddine for integration, according to Ihab. Final output/display verification, full integration, and end-to-end execution remain pending confirmation.

### Repository initialization

- Created the repository structure and initialized project documentation.
- Added Badreddine's initial Logisim simulation as `simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ`, byte-identical to the supplied `SAP_1.circ`; removed the redundant root copy after confirming byte equality.
- Added contributor information for Badreddine El Habra and Ihab Mahiaoui.
- Documented current status, reported testing results, source inspection observations, and the future roadmap.
- Added contribution guidance, GitHub templates, ignore rules, and an undecided-license placeholder.

### Ihab contribution documentation

- Replaced component placeholders with confirmed register, arithmetic, and display documentation, using Ihab's report and static reference-circuit inspection.
- Updated contributor attribution, architecture/instruction roles, design decisions, references, README, and roadmap.
- Separated individual tests, combined subsystem tests, integration, and complete program execution; retained Badreddine's reported results and scoped Ihab's manual results to the evidence supplied.
- Recorded the reference file's provenance without adding or modifying a circuit. The final simulation will be provided separately; this is a documentation-only update.

Integration of both sections and complete SAP-1 verification remain pending confirmation. No advanced architecture, assembler, or Arduino interface has been implemented here.
