# Control Unit (CU)

Implemented by Badreddine El Habra as a Control Matrix, Ring Counter, and 4-to-5 Decoder. All are regions of `main`, not separately named Logisim subcircuits.

## Purpose and SAP-1 role

The control unit coordinates register and bus actions by combining the current instruction selection with a timing state. It belongs to Badreddine's completed, manually tested subsystem. Signals intended for components outside that section do not demonstrate that those other components are present or integrated.

## 1. Control Matrix

The lower region contains 19 AND gates at x=250 and six OR gates at x=350. Output annotations read `Lo`, `Lb`, `Eu`, `Su`, `Ea`, `La`, `Ei`, `Li`, `CE`, `Lm`, `Ep`, and `Cp`.

These are observed annotation names. TODO: trace each output net, transcribe the Boolean equations, establish signal polarity, and record any inversion at the receiving component. Meanings and active levels must not be inferred from naming alone.

The matrix region's heading is also `4 to 5 decoder`, duplicating the heading above the actual decoder. The structure and output labels are consistent with Badreddine's reported Control Matrix, but the original heading remains unchanged. TODO: confirm the intended label before any circuit edit.

## 2. Ring Counter

The region labeled `Ring Counter` includes J-K flip-flops around y=1580–1590. A splitter at `(600,1480)` explicitly has six inputs/branches, and a nearby LED bar is configured with six columns. Another six-bit splitter appears at `(160,2200)` near the matrix input region. These observations support a six-line timing interface; they do not prove a particular timing sequence or one-hot invariant.

Purpose: supply successive timing states to coordinate operations. TODO: document the state labels, sequence, initialization/clear behavior, clock edge, and mapping from each timing line to the matrix. Do not treat the number of flip-flops or display columns as a measured cycle count.

## 3. 4-to-5 Decoder

The region headed `4 to 5 decoder` near y=1730 contains a four-bit splitter, four NOT gates near y=1830, and five AND gates explicitly configured with four inputs. The five outputs are annotated `LDA`, `ADD`, `SUB`, `OUT`, and `HLT`.

Purpose: select among five recognized instruction conditions from a four-bit operation field. TODO: trace the actual bit order and polarity to publish the opcode truth table, including behavior for unrecognized inputs. No opcode values are asserted in this documentation.

## 4. Control signal generation

Architecturally, decoded instruction conditions and timing states feed a gate matrix that generates transfer/load/operation controls. The supplied canvas contains the corresponding decoder, timing, and matrix regions; exact equations and end-to-end wiring must be recorded before they can serve as an integration contract.

| Interface | Observed structure or labels | Still to document |
| --- | --- | --- |
| Instruction selection | Four-bit splitter; five named decoder outputs | Input mapping and complete truth table |
| Timing | Six-way splitter and six-column timing display | State sequence, reset, edge, and line mapping |
| Matrix outputs | `Lo`, `Lb`, `Eu`, `Su`, `Ea`, `La`, `Ei`, `Li`, `CE`, `Lm`, `Ep`, `Cp` | Equations, polarity, receivers, and timing |
| Clock/start controls | `CLOCK`, `CLR`, `Clear/Start`, `HLT`, `manual/auto`, `single step` annotations elsewhere in `main` | Complete clock, halt, and reset connectivity |

The listed labels are not a finalized external pin specification. TODO: distinguish local manual stimulus controls from CU-driven nets and record how each is connected in the tested subsystem.

## 5. Timing states, opcodes, and controls

In the SAP-1 architectural model, the timing state identifies the current step, the decoded opcode identifies the instruction, and the matrix selects the controls needed for that combination. Badreddine reports that these components work correctly individually and together in his simulation.

TODO: add a table of timing state × decoded instruction → asserted controls derived from the actual circuit. Include common fetch operations and instruction-specific operations only after confirming the wiring. Attach the manual procedure and observed results rather than inventing state names, waveforms, or clock-cycle counts.

## Connections and limitations

The intended receivers include the PC, MAR, RAM, and IR, with further datapath interfaces to be agreed during integration with Ihab Mahiaoui. Ihab has confirmed implementing the accumulator A, B register, adder/subtractor, output register, binary display, and signed decimal display; see [arithmetic](alu.md) and [registers/displays](other-components.md). His reference was supplied for documentation, but the final simulation has not been added. CU output annotations alone do not establish polarity/timing compatibility with his controls or successful integration.

## Testing status

**Implemented and manually tested successfully by Badreddine El Habra**, both individually and as part of his combined subsystem in Logisim Evolution, according to his report. Codex did not independently reproduce these functional tests. Detailed evidence is pending; see [testing](../testing.md).

## Known limitations and documentation TODOs

Integration with Ihab Mahiaoui's section and full SAP-1 verification remain pending. These integration and documentation tasks do not change the reported successful status of this component.

TODO: add an annotated diagram, reproducible input/expected-output procedure, and supporting test evidence. Confirm interface details listed above before integration.
