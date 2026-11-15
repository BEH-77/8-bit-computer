# Architecture

## Scope and status

The current design is inspired by SAP-1 from *Digital Computer Electronics*. Badreddine El Habra's PC, MAR, RAM, IR, Control Matrix, Ring Counter, and 4-to-5 Decoder are implemented and manually tested successfully, both individually and together, according to his report. Ihab Mahiaoui's separate section has not been supplied. Complete SAP-1 integration and verification are pending.

The conceptual SAP-1 flow is: PC supplies an instruction address, MAR holds a memory address, RAM supplies instruction/data values, IR retains an instruction, and control logic coordinates transfers using instruction decoding and timing states. This describes architectural roles; the complete connection map and timing contract still need documentation from the simulation before integration.

## Source inspection

Inspected source: [Badreddine's simulation](../simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ), imported unchanged from the supplied `SAP_1.circ`.

- XML project `source="4.1.0"`, format `version="1.0"`; the file explicitly identifies Logisim Evolution v4.1.0.
- Exactly one circuit, `main`. The components are regions of that canvas, not separately named subcircuits.
- Built-in libraries are referenced; no external circuit-library file references were found.
- Present primitives: 13 J-K flip-flops, three explicitly 4-bit registers, one RAM with explicit 4-bit address width, one 4-bit multiplexer, six controlled buffers, 13 splitters, 26 AND gates, seven OR gates, ten NOT gates, one clock, switches, buttons, and LED displays.
- PC region: four J-K flip-flops. MAR: register labeled `MAR`, explicitly width 4. IR region: two registers, each explicitly width 4.
- RAM data width is not explicitly serialized. Adjacent 8-bit splitters and an 8-bit buffer support an 8-bit data path; confirm the RAM's effective Data Bits setting in Logisim before publishing a definitive memory specification.
- CU region includes a six-way timing splitter/display, a labeled Ring Counter, a four-input/five-output gate decoder, and a subsequent AND/OR matrix with control labels.
- Source labels include `W Bus`, `Cp`, `Ep`, `Lm`, `CE`, `Li`, `Ei`, `CLR`, `CLK`, `Lo`, `Lb`, `Eu`, `Su`, `Ea`, `La`, and decoder labels `LDA`, `ADD`, `SUB`, `OUT`, `HLT`. Text annotations alone do not establish pin direction, polarity, or electrical connectivity.

## Discrepancies and limits

- The requested input name was `SAP_1(1).circ`; the supplied circuit was named `SAP_1.circ`. It was copied without changes to the organized simulation path; the redundant root copy was then removed after a byte comparison.
- The lower gate-matrix region is headed `4 to 5 decoder`, duplicating the decoder heading above it. Its gates and output labels are consistent with the reported Control Matrix region; the heading was preserved. TODO: confirm the intended heading with Badreddine before any circuit edit.
- The original MAR annotation spells “Adress”; documentation uses “Address”. The original annotation is unchanged.
- The canvas title `8 Bit Computer` does not imply a complete integrated computer.

XML inspection establishes structure, not functional correctness. Codex did not independently reproduce the reported tests. Logisim Evolution is installed, but its startup failed because the environment could not connect to the X11 display; GUI opening was not verified.

## Pending interfaces

TODO: add an annotated datapath diagram, trace bus bit ordering, record control polarities and clock edges, document reset/start behavior, and agree on interfaces with Ihab. These are documentation and integration tasks, not claims that Badreddine's completed section is unfinished.

The advanced computer architecture is undecided. Its instruction encoding, register set, memory sizes, datapath, and control approach must be agreed before implementation; see the [roadmap](roadmap.md).
