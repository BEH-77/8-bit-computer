# 8-Bit Computer

A Computer Architecture honors component project by Badreddine El Habra and Ihab Mahiaoui. We are building a computer in Logisim Evolution to understand how registers, memory, arithmetic, and control signals work together to execute instructions.

Our starting point is SAP-1 from *Digital Computer Electronics* by Albert Paul Malvino and Jerald A. Brown. A more advanced 8-bit architecture is planned after the SAP-1 implementation is verified.

## Current status

- Badreddine implemented the PC, MAR, RAM, instruction register, ring counter, instruction decoder, and control matrix. He reports successful manual tests of each component and of his combined subsystem.
- Ihab implemented the accumulator, B register, adder/subtractor, output register, binary LEDs, and a signed decimal display extension. He reports successful accumulator and basic arithmetic/B-register–ALU tests; final output/display verification remains pending.
- Both circuit files are included. Badreddine's current file contains both sections on one canvas, but the datapath still has manual control and clock pins. Automatic control integration and complete program execution remain unfinished.

The [testing record](docs/testing.md) separates reported results from pending checks. The manual results have not been independently reproduced, and no automated circuit test suite is included.

## Open the circuits

1. Install [Logisim Evolution](https://github.com/logisim-evolution/logisim-evolution/releases) and clone or download this repository.
2. Choose **File → Open** and select a circuit:
   - [PC, memory, control, and assembled datapath](simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ) — saved with version 4.1.0.
   - [Ihab's datapath and displays](simulations/sap-1/ihab-mahiaoui/Our_8Bit_Computer.circ) — saved with version 5.0.0; also contains PC/memory regions.
3. Select `main`, then zoom out to locate the labeled sections. Each file uses one canvas rather than separate component subcircuits.

Use the recorded version for each file where possible; cross-version compatibility has not been tested. See [simulation notes](simulations/sap-1/README.md) for the canvas layout and current operating limits.

## Documentation

- [Architecture](docs/architecture.md) and [instruction set](docs/instruction-set.md)
- Components: [PC](docs/components/program-counter.md), [MAR](docs/components/mar.md), [RAM](docs/components/ram.md), [IR](docs/components/instruction-register.md), [control unit](docs/components/control-unit.md), [ALU](docs/components/alu.md), [registers and displays](docs/components/registers-and-displays.md)
- [Testing](docs/testing.md), [design decisions](docs/design-decisions.md), and [roadmap](docs/roadmap.md)
- [Contributors](docs/contributors.md), [contribution workflow](CONTRIBUTING.md), and [changelog](CHANGELOG.md)

Badreddine El Habra ([BEH-77](https://github.com/BEH-77)) and Ihab Mahiaoui maintain the project. See [references](docs/references.md) for the textbook and implementation sources. A project license has [not yet been selected](LICENSE).
