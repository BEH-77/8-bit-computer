# Changelog

A simplified Keep a Changelog record. `Unreleased` groups imported work and repository preparation; it does not imply separate historical commits, dates, or releases.

## Unreleased

### Previously completed SAP-1 simulation work

Reported by Badreddine El Habra; the supplied XML contains the corresponding circuit regions.

- Implemented the Program Counter, MAR, RAM, and Instruction Register.
- Implemented the Control Matrix, Ring Counter, and 4-to-5 Decoder.
- Successfully tested each component individually in Logisim Evolution, according to Badreddine's manual testing report.
- Successfully tested the implemented components together in one simulation, according to the same report.

### Repository initialization

- Created the repository structure and initialized project documentation.
- Added Badreddine's initial Logisim simulation as `simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ`, byte-identical to the supplied `SAP_1.circ`; removed the redundant root copy after confirming byte equality.
- Added contributor information for Badreddine El Habra and Ihab Mahiaoui.
- Documented current status, reported testing results, source inspection observations, and the future roadmap.
- Added contribution guidance, GitHub templates, ignore rules, and an undecided-license placeholder.

Ihab's simulation and component details have not yet been added. Integration of both sections and complete SAP-1 verification remain pending. No advanced architecture, assembler, or Arduino interface has been implemented here.
