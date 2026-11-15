# 8-Bit Computer

An evolving digital computer project by **Badreddine El Habra** and **Ihab Mahiaoui**, designed and simulated in **Logisim Evolution**. The current work follows SAP-1 concepts from *Digital Computer Electronics* by Albert Paul Malvino and Jerald A. Brown.

The project explores how registers, memory, timing logic, and control signals cooperate to execute instructions. Our objectives are to document reproducible simulations, integrate our SAP-1 sections, and use that experience to design a more advanced 8-bit computer. The future architecture and specifications remain undecided.

## Current status

Badreddine's SAP-1 components have been implemented and successfully tested both individually and together in Logisim Evolution. The complete SAP-1 computer has not yet been assembled from both contributors' simulation files, and full-system integration remains pending.

Badreddine's completed section includes:

- Program Counter (PC)
- Memory Address Register (MAR)
- Random Access Memory (RAM)
- Instruction Register (IR)
- Control Unit (CU): Control Matrix, Ring Counter, and 4-to-5 Decoder

The successful manual simulation results were reported by Badreddine; repository preparation did not independently reproduce those tests. Detailed test evidence remains to be added. Ihab's simulation file and specific contribution details are pending. This repository does not yet contain a complete integrated SAP-1 computer.

## Tools

- **Logisim Evolution:** circuit design and simulation; the supplied file identifies version **4.1.0**.
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
   ihab-mahiaoui/               Placeholder README; simulation pending
 tests/                        Test procedure and artifact guidance
 assets/diagrams/              Reserved for circuit diagrams
 assets/screenshots/           Reserved for simulation evidence
 .github/                      Issue and pull request templates
```

## Documentation

- [Architecture and source inspection](docs/architecture.md)
- [Instruction set status](docs/instruction-set.md)
- Components: [PC](docs/components/program-counter.md), [MAR](docs/components/mar.md), [RAM](docs/components/ram.md), [IR](docs/components/instruction-register.md), [CU](docs/components/control-unit.md)
- Pending documentation: [ALU](docs/components/alu.md), [other components](docs/components/other-components.md)
- [Testing and reported results](docs/testing.md)
- [Design decisions](docs/design-decisions.md)
- [Roadmap](docs/roadmap.md) and [changelog](CHANGELOG.md)

## Development roadmap

1. Record component behavior and test evidence for the existing simulations.
2. Add Ihab's section, agree on interfaces, integrate, and verify the complete SAP-1 with test programs.
3. Finalize the advanced computer's architecture, instruction set, memory, and registers, then implement and verify its simulation.
4. Develop an assembler and Arduino programming interface once the architecture is defined.

See the [milestone checklist](docs/roadmap.md). Assembler and Arduino development have not started in this repository.

## Contributors

**Badreddine El Habra** ([BEH-77](https://github.com/BEH-77)) implemented and manually tested the PC, MAR, RAM, IR, Control Matrix, Ring Counter, and 4-to-5 Decoder. He prepared the initial repository setup and documentation with Codex assistance.

**Ihab Mahiaoui** is the second contributor to the SAP-1 project. He has implemented other SAP-1 components; their specific responsibilities and simulation will be documented when supplied. His GitHub username remains a TODO in the [contributor record](docs/contributors.md).

See [CONTRIBUTING.md](CONTRIBUTING.md) for the lightweight review workflow.

## References and licensing

SAP-1 architectural inspiration: *Digital Computer Electronics*, Albert Paul Malvino and Jerald A. Brown. Original SAP-1 concepts are distinct from this team's Logisim Evolution implementation; see [references and attribution](docs/references.md).

Licensing is undecided. The [LICENSE](LICENSE) placeholder does not grant public reuse permissions.
