# 8-Bit Computer

An evolving digital computer project by **Badreddine El Habra** and **Ihab Mahiaoui**, designed and simulated in **Logisim Evolution**. The current work follows SAP-1 concepts from *Digital Computer Electronics* by Albert Paul Malvino and Jerald A. Brown.

The project explores how registers, memory, timing logic, and control signals cooperate to execute instructions. Our objectives are to document reproducible simulations, integrate our SAP-1 sections, and use that experience to design a more advanced 8-bit computer. The future architecture and specifications remain undecided.

## Current status

Both contributors have completed their assigned component implementations:

| Contributor | Completed components | Testing record |
| --- | --- | --- |
| Badreddine El Habra | Program Counter (PC), Memory Address Register (MAR), RAM, Instruction Register (IR), Control Matrix, Ring Counter, and 4-to-5 Decoder | Individual and combined subsystem manual tests passed, as reported by Badreddine |
| Ihab Mahiaoui | Accumulator A, B register, adder/subtractor, output register, binary display, and signed decimal display | Accumulator storage/bus-output and basic arithmetic/B-register–ALU operation manually tested, as reported by Ihab; final output/display verification pending |

The reported manual results have not been independently reproduced. Ihab supplied `Our_8Bit_Computer.circ` and a technical/testing report for documentation. His signed decimal display is an additional visualization feature beyond textbook SAP-1. This update adds his documentation; the final simulation will be added separately. successful full integration and program execution remain unconfirmed. See the [testing record](docs/testing.md) for exact scope and missing evidence.

## Tools

- **Logisim Evolution:** circuit design and simulation. Badreddine's committed file identifies **4.1.0**; Ihab's documentation reference identifies **5.0.0**. Cross-version compatibility has not been tested.
- **Git:** version control.
- **GitHub:** repository hosting, issue tracking, and pull request review.

## Open the simulation

1. Install Logisim Evolution; use **4.1.0** to match the file's recorded source version. Compatibility with other versions has not been checked.
2. Clone or download this repository.
3. In Logisim Evolution, choose **File → Open** and select [sap1-pc-memory-control.circ](simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ).
4. Select the `main` circuit. The sections occupy one canvas; zoom and scroll to inspect them.
5. Review the [simulation notes](simulations/sap-1/README.md) and [testing record](docs/testing.md) before attempting to reproduce the manual tests. Exact stimulus sequences remain TODOs.

The simulation is preserved unchanged from the supplied file. See the simulation notes for its import checksum and provenance.

## Repository layout

```text
README.md / LICENSE / CONTRIBUTING.md / CHANGELOG.md
 docs/                         Architecture, components, tests, and project records
 simulations/sap-1/
   badreddine-el-habra/         PC, memory, and control simulation
   ihab-mahiaoui/               Contribution/source notes; circuit addition pending
 tests/                        Test procedure and artifact guidance
 assets/diagrams/              Reserved for circuit diagrams
 assets/screenshots/           Reserved for simulation evidence
 .github/                      Issue and pull request templates
```

## Documentation

- [Architecture and source inspection](docs/architecture.md)
- [Instruction set status](docs/instruction-set.md)
- Components: [PC](docs/components/program-counter.md), [MAR](docs/components/mar.md), [RAM](docs/components/ram.md), [IR](docs/components/instruction-register.md), [CU](docs/components/control-unit.md)
- Ihab's components: [adder/subtractor](docs/components/alu.md), [registers and displays](docs/components/other-components.md)
- [Testing and reported results](docs/testing.md)
- [Design decisions](docs/design-decisions.md)
- [Roadmap](docs/roadmap.md) and [changelog](CHANGELOG.md)

## Development roadmap

1. Complete the remaining interface documentation and record test procedures/results for both contributors' completed components.
2. Add Ihab's circuit in a separate simulation update, agree on interfaces, integrate the full control/datapath, and verify complete SAP-1 test programs.
3. Finalize the advanced computer's architecture, instruction set, memory, and registers, then implement and verify its simulation.
4. Develop an assembler and Arduino programming interface once the architecture is defined.

See the [milestone checklist](docs/roadmap.md). Assembler and Arduino development have not started in this repository.

## Contributors

**Badreddine El Habra** ([BEH-77](https://github.com/BEH-77)) implemented and manually tested the PC, MAR, RAM, IR, Control Matrix, Ring Counter, and 4-to-5 Decoder.His implementation and reported manual test scope are documented.

**Ihab Mahiaoui** implemented the accumulator A, B register, adder/subtractor, output register, binary display, and signed decimal display. His implementation and reported manual test scope are documented.

See [CONTRIBUTING.md](CONTRIBUTING.md) for the lightweight review workflow.

## References and licensing

SAP-1 architectural inspiration: *Digital Computer Electronics*, Third Edition, Albert Paul Malvino and Jerald A. Brown. Original SAP-1 concepts are distinct from this team's Logisim Evolution implementation and signed-display extension; see [references and attribution](docs/references.md).

Licensing is undecided. The [LICENSE](LICENSE) placeholder does not grant public reuse permissions.
