# Architecture

## Scope and status

The current design is inspired by SAP-1 from *Digital Computer Electronics*, Third Edition. Badreddine El Habra's PC, MAR, RAM, IR, Control Matrix, Ring Counter, and 4-to-5 Decoder are implemented and manually tested successfully, both individually and together, according to his report. Ihab Mahiaoui confirms completing the accumulator A, B register, adder/subtractor, output register, binary display, and signed decimal display. He reports successful accumulator storage/bus-output and basic arithmetic/B-register–ALU manual tests. His reference circuit was supplied for documentation inspection; adding the final simulation to Git is a later step. Full integration, final output/display verification, and complete SAP-1 execution remain pending confirmation.

The conceptual SAP-1 flow is: PC supplies an instruction address, MAR holds a memory address, RAM supplies instruction/data values, IR retains an instruction, and control logic coordinates transfers using instruction decoding and timing states. This describes architectural roles; the complete connection map and timing contract still need documentation from the simulation before integration.

## Source inspection

### Badreddine's committed section

Inspected source: [Badreddine's simulation](../simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ), imported unchanged from the supplied `SAP_1.circ`.

- XML project `source="4.1.0"`, format `version="1.0"`; the file explicitly identifies Logisim Evolution v4.1.0.
- Exactly one circuit, `main`. The components are regions of that canvas, not separately named subcircuits.
- Built-in libraries are referenced; no external circuit-library file references were found.
- Present primitives: 13 J-K flip-flops, three explicitly 4-bit registers, one RAM with explicit 4-bit address width, one 4-bit multiplexer, six controlled buffers, 13 splitters, 26 AND gates, seven OR gates, ten NOT gates, one clock, switches, buttons, and LED displays.
- PC region: four J-K flip-flops. MAR: register labeled `MAR`, explicitly width 4. IR region: two registers, each explicitly width 4.
- RAM data width is not explicitly serialized. Adjacent 8-bit splitters and an 8-bit buffer support an 8-bit data path; confirm the RAM's effective Data Bits setting in Logisim before publishing a definitive memory specification.
- CU region includes a six-way timing splitter/display, a labeled Ring Counter, a four-input/five-output gate decoder, and a subsequent AND/OR matrix with control labels.
- Source labels include `W Bus`, `Cp`, `Ep`, `Lm`, `CE`, `Li`, `Ei`, `CLR`, `CLK`, `Lo`, `Lb`, `Eu`, `Su`, `Ea`, `La`, and decoder labels `LDA`, `ADD`, `SUB`, `OUT`, `HLT`. Text annotations alone do not establish pin direction, polarity, or electrical connectivity.

### Ihab's documentation reference

Inspected reference: `Our_8Bit_Computer.circ`, supplied by Ihab outside the repository. Its checksum and submission status are recorded in [Ihab's source notes](../simulations/sap-1/ihab-mahiaoui/README.md); no link to an uncommitted circuit is presented as an available repository file.

- XML `source="5.0.0"`, format `version="1.0"`; exactly one `main` circuit, with 165 components and 731 wire records. Only built-in libraries are referenced.
- A, B, and OUT each use two explicitly four-bit registers: `A_LOW`/`A_HIGH`, `B_LOW`/`B_HIGH`, and `OUT_LOW`/`OUT_HIGH`.
- The arithmetic path contains two explicitly four-bit Adders, a carry-chain connection, eight XOR gates for conditional B inversion, and eight controlled result buffers. A has its own bank of eight controlled buffers.
- Labeled pins are `LA_N`, `LB_N`, `LO_N`, `CLK`, `EA`, `EU`, and `SU`. Wire tracing establishes load-request inversion and a common clock for A/B/OUT; it does not establish synchronization with the PC/memory section.
- Output circuitry includes eight binary LEDs, sign/absolute-value logic, two divide-by-10 stages, three digit displays, and a sign display. See [registers and displays](components/other-components.md) for verified structure and remaining routing checks.
- PC/MAR/RAM/IR regions are also present. Ihab's confirmed contribution is the six-component datapath/display list above; these additional regions do not change Badreddine's attribution.
- No ring-counter, instruction-decoder, or control-matrix region was found in this reference. Partial datapath/memory wiring does not establish a complete control-driven SAP-1 or successful instruction execution.

This update combines Ihab's technical/test report with static XML/wire inspection and version-matched primitive definitions where noted on the component pages. No Logisim functional execution was performed during documentation preparation. The signed decimal display is an additional visualization feature; it interprets OUT as two's complement without changing the stored byte, arithmetic, or textbook instruction set.

## Architectural relationships and integration

| Relationship | Architectural role | Current boundary |
| --- | --- | --- |
| PC → MAR → RAM → IR | Address and fetch an instruction | Badreddine's reported tested subsystem; exact interface contract still needs documentation |
| W-Bus → A and B → adder/subtractor | Load operands and compute an eight-bit result | Ihab documents low bits 0–3/high bits 4–7 and reports basic operation; complete transfer coverage remains to be recorded |
| A or arithmetic result → transfer bus | Select the value available for register transfers | `EA` and `EU` buffer banks are present; shared-bus ownership must be verified |
| W-Bus → OUT → binary/decimal displays | Capture and present a retained output value | Ihab's output storage and displays are implemented; final evidence and comprehensive signed-display verification remain pending |
| Decoder/timing/control matrix → datapath controls | Sequence fetch, arithmetic, and output operations | Complete cross-section control wiring and timing are pending |

These relationships describe the intended SAP-1 organization, not a verified complete connection diagram. Badreddine's `La`, `Ea`, `Lb`, `Su`, `Eu`, and `Lo` annotations are candidate counterparts to Ihab's `LA_N`, `EA`, `LB_N`, `SU`, `EU`, and `LO_N`. Confirm active levels and receiving inversions before connecting them. A/B/OUT currently have grounded clear inputs; a shared reset/start strategy must be agreed.

Ihab reports handing his section to Badreddine for integration. The final combined file will be supplied separately. Manual controls in the reference must not be described as a finished automatic control interface. Ihab's arithmetic wraps modulo 256, leaves the final carry unused, and has no dedicated carry/overflow-status register; see [design decisions](design-decisions.md).

## Discrepancies and limits

- The requested input name was `SAP_1(1).circ`; the supplied circuit was named `SAP_1.circ`. It was copied without changes to the organized simulation path; the redundant root copy was then removed after a byte comparison.
- The lower gate-matrix region is headed `4 to 5 decoder`, duplicating the decoder heading above it. Its gates and output labels are consistent with the reported Control Matrix region; the heading was preserved. TODO: confirm the intended heading with Badreddine before any circuit edit.
- The original MAR annotation spells “Adress”; documentation uses “Address”. The original annotation is unchanged.
- The canvas title `8 Bit Computer` does not imply a complete integrated computer.

XML inspection establishes structure, not functional correctness. Codex did not independently reproduce the reported tests. During the initial repository preparation, Logisim Evolution startup failed because that environment could not connect to the X11 display; GUI opening was not verified. That historical limitation is separate from this documentation update's static inspection of Ihab's file.

## Pending interfaces

TODO: add an annotated datapath diagram, finish tracing bus bit ordering, confirm the control-matrix output polarities and timing against Ihab's receiving signals, document shared reset/start behavior, and agree on a compatible Logisim version (the two source files identify 4.1.0 and 5.0.0). These are documentation and integration tasks, not claims that either contributor's completed component implementation is unfinished.

The advanced computer architecture is undecided. Its instruction encoding, register set, memory sizes, datapath, and control approach must be agreed before implementation; see the [roadmap](roadmap.md).
