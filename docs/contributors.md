# Contributors

| Team member | GitHub username | Assigned responsibilities | Implemented components | Contribution status |
| --- | --- | --- | --- | --- |
| Badreddine El Habra | [BEH-77](https://github.com/BEH-77) | PC, memory, and control section; initial repository setup and documentation | Program Counter, MAR, RAM, IR, Control Matrix, Ring Counter, 4-to-5 Decoder | Implemented; individual and combined subsystem manual tests passed, as reported by Badreddine |
| Ihab Mahiaoui | TODO: username not supplied | Accumulator and operand storage, arithmetic datapath, output storage, and binary/signed-decimal presentation | Accumulator A, B register, adder/subtractor, output register, binary display, and signed decimal display | Implementation complete; accumulator storage/bus-output and basic arithmetic/B-register–ALU operation manually tested, as reported by Ihab; final output/display verification and circuit addition pending |

The initial repository setup and documentation were prepared by Badreddine El Habra with Codex assistance. The SAP-1 project is a collaboration between Badreddine and Ihab; this record does not assign exclusive authorship of the overall project or attribute unspecified components to either contributor.

## Ihab's confirmed contribution

Ihab explicitly identified the six components above as his work. Their development was completed before this documentation update; no historical development dates or commits are inferred. His [adder/subtractor](components/alu.md) and [registers/displays](components/other-components.md) are documented from his technical report and static inspection of `Our_8Bit_Computer.circ` (Logisim Evolution 5.0.0). The signed decimal display is his additional visualization feature. The [reference-file record](../simulations/sap-1/ihab-mahiaoui/README.md) distinguishes inspection from adding the circuit to Git.

The reference also contains PC, MAR, RAM, and IR sections. These are not attributed to Ihab; Badreddine's established component ownership remains unchanged. This documentation update was prepared for Ihab with Codex assistance.

## Testing and remaining information

Badreddine's reported successful individual and combined manual tests are preserved in [testing](testing.md). Ihab reports a successful accumulator storage/bus-output test with `0x35`, working basic arithmetic after correcting low/high nibble wiring, and basic combined B-register/ALU operation. Standalone B-register coverage, final output/LED evidence, and comprehensive signed-display verification are not established by that report.

Ihab reports sending his section to Badreddine, who is responsible for integrating both sections. Successful integration and complete SAP-1 program execution remain pending confirmation; no completed integration is credited here.

TODO: add Ihab's GitHub username and the missing reproducible test procedures/results. No contribution percentages or unprovided work history are assigned.
