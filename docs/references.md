# References and attribution

- *Digital Computer Electronics*, Third Edition, Albert Paul Malvino and Jerald A. Brown. Its SAP-1 design served as the architectural inspiration for this project. Ihab supplied the edition information; page references remain TODO.
- Logisim Evolution is the circuit design and simulation tool. Badreddine's committed file identifies version 4.1.0; Ihab's documentation reference identifies 5.0.0. Compatibility between these versions has not been tested.
- [Badreddine’s simulation](../simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ) and Badreddine El Habra's manual testing report are the sources for the current implementation observations and reported results. See [architecture](architecture.md) and [testing](testing.md).
- Ihab Mahiaoui's contribution confirmation and supplied notes, titled *SAP-1 Project — Technical Documentation of My Contributions*, establish his responsibilities, design decisions, manually reported results, and pending checks. Their implementation observations are supplemented by static inspection of `Our_8Bit_Computer.circ`; see its [provenance record](../simulations/sap-1/ihab-mahiaoui/README.md). The reference is not yet a committed simulation.
- Version-matched Logisim Evolution 5.0.0 primitive definitions support the port/default interpretations cited on the [ALU](components/alu.md) and [register/display](components/other-components.md) pages. Source inspection is separate from functional test evidence.

SAP-1 concepts originate in the referenced textbook. This repository contains the team's Logisim Evolution implementation and project documentation. The textbook authors have not been represented as endorsing or contributing to this project.

Badreddine's section is committed here; Ihab's completed component work is now documented, with the final simulation to be added separately. His signed decimal display is an additional Logisim visualization feature, not a required part of the textbook SAP-1. See [contributors](contributors.md).

Project licensing is [undecided](../LICENSE). Textbook material and third-party tools retain their own rights and licensing; this repository does not grant rights to them.
