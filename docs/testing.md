# Testing

Functional results currently come from Badreddine's and Ihab's manual Logisim Evolution reports. They have not been independently reproduced. No automated circuit test suite, waveform captures, or screenshots are included.

## Reported component tests

Badreddine reports that all seven components below passed individual manual tests. Detailed stimuli and expected/observed values were not supplied.

| Component | Reported result |
| --- | --- |
| Program Counter | Passed |
| MAR | Passed |
| RAM | Passed |
| Instruction Register | Passed |
| Ring Counter | Passed |
| Instruction decoder | Passed |
| Control matrix | Passed |

Ihab's existing contribution notes record a narrower test scope:

| Component | Reported result and limits |
| --- | --- |
| Accumulator A | Storage and bus output passed: `A_HIGH=0x3`, `A_LOW=0x5`, `EA=1`; expected and observed W-Bus value `0x35`. The exact loading/clock sequence is missing. |
| Adder/subtractor | Basic arithmetic worked after correcting low/high nibble wiring. Operand vectors and boundary results were not supplied. |
| B register | Basic operation tested with the ALU; no standalone load/hold result recorded. |
| Output register | Implemented; final capture/hold verification pending confirmation. |
| Binary LEDs | Implemented; final observed output patterns pending confirmation. |
| Signed decimal display | Implemented; comprehensive positive, negative, zero, and boundary checks pending. |

The [decimal-display examples](components/registers-and-displays.md#decimal-display) are expected outputs, not observed results. Missing evidence does not invalidate a reported pass, but it limits reproducibility.

## Subsystems and complete computer

| Scope | Status |
| --- | --- |
| Badreddine's seven components together | Passed manual combined simulation, reported by Badreddine |
| Ihab's B-register/ALU path | Basic combined operation passed, reported by Ihab |
| All of Ihab's components together | Complete pass not established by the supplied report |
| Assembled control and datapath | Both sections are present in Badreddine's current file; control and clock interfaces remain incomplete |
| Complete instruction/program execution | Pending; no complete SAP-1 pass reported |

The reports do not identify the exact circuit revision or Logisim version used for each test. In particular, Badreddine's earlier subsystem result must not be extended to the current assembled canvas without a new run. The files' saved source versions are recorded in [simulation notes](../simulations/sap-1/README.md).

## Static review

Both current `.circ` files were parsed as XML. The review checked circuit/library inventories, explicit register widths, RAM settings, annotations, and selected wire connections. Version-matched Logisim source definitions were used where attributes were omitted. Checksums confirmed that the documentation edits did not change either supplied circuit.

No Logisim GUI execution or functional simulation was performed during this review. XML parsing and wire inspection establish structure, not correct execution.

## Next verification work

1. Record the PC/memory operating procedure: startup, manual/automatic clock selection, memory programming and readback, and register load/hold behavior. Account for the two files' different RAM trigger settings.
2. Transcribe the decoder truth table and control matrix's timing-state table. Check reset initialization, timing order, and halt behavior.
3. Connect and verify datapath controls, clock, and reset. Check active levels and ensure only the selected source drives the W-Bus.
4. Record A/B load/hold and ALU operand cases, including nibble carry, subtraction, and eight-bit wraparound.
5. Check OUT retention, LED bit order, and all expected signed-display cases.
6. Run complete `LDA`, `ADD`, `SUB`, `OUT`, and `HLT` sequences, then small programs with stated memory images and expected final values.

For each run, record the circuit path and commit, Logisim version, initial state or memory contents, input/clock sequence, expected values, observed values, and pass/fail result. Keep proposed cases separate from executed results. Add screenshots or traces alongside the corresponding record when available; there are no evidence artifacts to link yet.
