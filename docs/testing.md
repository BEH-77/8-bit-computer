# Testing

This record separates individual components, combined subsystems, integration between contributors, and complete program execution. Reported manual results are attributed to their contributor; static inspection does not establish functional correctness.

## 1. Individual component testing

### Badreddine's report

Badreddine El Habra reports successful manual testing of every component he implemented, both individually and together within his Logisim Evolution simulation. His completed section functions correctly as a combined simulation according to that report. These are simulation results, not physical hardware tests.

Codex did not independently reproduce these functional results. No detailed test vectors, waveforms, dates, measured cycle counts, or screenshots were supplied. The missing evidence is a documentation task, not a claim that the reported tests failed or the components remain unfinished.

### Badreddine's individual components — passed (reported)

| Component | Testing method | Reported result | Evidence | Notes |
| --- | --- | --- | --- | --- |
| Program Counter | Individual manual simulation in Logisim Evolution | Passed, reported by Badreddine | Manually verified in Logisim Evolution; detailed test evidence to be added | Stimuli and expected/observed outputs TODO |
| Memory Address Register | Individual manual simulation in Logisim Evolution | Passed, reported by Badreddine | Manually verified in Logisim Evolution; detailed test evidence to be added | Stimuli and expected/observed outputs TODO |
| Random Access Memory | Individual manual simulation in Logisim Evolution | Passed, reported by Badreddine | Manually verified in Logisim Evolution; detailed test evidence to be added | Stimuli and expected/observed outputs TODO |
| Instruction Register | Individual manual simulation in Logisim Evolution | Passed, reported by Badreddine | Manually verified in Logisim Evolution; detailed test evidence to be added | Stimuli and expected/observed outputs TODO |
| Control Matrix | Individual manual simulation in Logisim Evolution | Passed, reported by Badreddine | Manually verified in Logisim Evolution; detailed test evidence to be added | Stimuli and expected/observed outputs TODO |
| Ring Counter | Individual manual simulation in Logisim Evolution | Passed, reported by Badreddine | Manually verified in Logisim Evolution; detailed test evidence to be added | Stimuli and expected/observed outputs TODO |
| 4-to-5 Decoder | Individual manual simulation in Logisim Evolution | Passed, reported by Badreddine | Manually verified in Logisim Evolution; detailed test evidence to be added | Stimuli and expected/observed outputs TODO |

### Ihab's individual components — mixed verification status

All six components below are implemented, according to Ihab. The results are from his supplied technical report, not an independent rerun. Missing evidence is not a reported failure and does not establish that a test was never performed.

| Component | Reported activity/result | Evidence and remaining scope |
| --- | --- | --- |
| Accumulator A | Storage and W-Bus output manually tested successfully | `A_HIGH=0x3`, `A_LOW=0x5`, `EA=1`: expected and observed output `0x35` (`00110101`); exact loading/clock sequence and broader coverage TODO |
| Adder/subtractor | Basic arithmetic manually tested and reported working | Ihab corrected an erroneous low/high nibble connection during debugging, then reported working arithmetic; operand vectors, operation coverage, and boundary results TODO |
| B register | Basic operation tested with the ALU | Combined scope recorded below; standalone load/hold test results not supplied |
| Output register | Implementation complete | Detailed final capture/hold test evidence pending confirmation; no blanket pass claimed |
| Binary LED output | Implementation complete | Detailed final output-pattern evidence pending confirmation; no blanket pass claimed |
| Signed decimal display | Implementation complete; comprehensive verification pending | Positive, negative, zero, and boundary results not fully recorded; design expectations are not observed results |

#### Recorded accumulator example

Ihab reports manually storing a value and enabling the accumulator's W-Bus output. The supplied example gives high nibble `0x3`, low nibble `0x5`, and `EA=1`; both the expected and observed bus value were `0x35`. The report does not specify the complete stimulus sequence, other bus-driver states, clock transitions, or evidence artifacts. TODO: add those details before presenting this example as a fully reproducible procedure.

The [decimal-display examples](components/other-components.md#decimal-display) are expected outputs supplied by Ihab, not passed test cases. In particular, correct handling of -128, +127, zero, and the minus sign remains to be demonstrated in a complete report.

## 2. Combined subsystem testing

### Badreddine's subsystem — passed (reported)

| Component | Testing method | Reported result | Evidence | Notes |
| --- | --- | --- | --- | --- |
| Combined subsystem: Badreddine's seven components listed above | Combined manual simulation in Logisim Evolution | Passed, reported by Badreddine | Manually verified in Logisim Evolution; detailed test evidence to be added | Badreddine’s section only; complete SAP-1 integration pending |

### Ihab's subsystem — basic B-register/ALU operation reported

| Scope | Reported result | Limit |
| --- | --- | --- |
| B register connected to XOR gates and ALU | Basic combined operation manually tested, reported working by Ihab after completing these connections | Exact operands, control sequences, and observed values remain TODO |
| All six of Ihab's components together | Complete combined pass not established by the supplied report | Do not extend the basic arithmetic result to output-register capture, both displays, or every bus transfer |

Ihab's correction of low/high nibble wiring is reported development/debugging history. No historical commit, date, exhaustive regression suite, or precise defect location is inferred.

## Repository preparation checks

### Initial repository preparation

- Parsed the source XML and inspected its circuit inventory, explicit attributes, and annotations.
- Compared the organized simulation copy with the original byte for byte; initial sizes and SHA-256 are recorded in [simulation notes](../simulations/sap-1/README.md).
- Checked relative Markdown links and required repository paths.
- Logisim Evolution is installed, but startup failed because it could not connect to X11. GUI opening and simulation execution were not independently verified.

Structural and integrity checks do not establish circuit correctness.

### Ihab documentation update

- Parsed the supplied reference XML and inspected its explicit widths, component inventory, and selected wire connections without editing it.
- Compared omitted primitive settings and port positions with the Logisim Evolution 5.0.0 source where cited on the component pages.
- Reviewed attribution and test scope against Ihab's technical report.
- Checked Markdown references, the documentation diff, and preservation of the existing circuit.

No new functional simulation or automated circuit test was run for this update. The reference file's `source="5.0.0"` identifies its saved version; the exact version used for each historical manual test was not separately recorded.

## 3. Integration of both contributors' sections — pending confirmation

Ihab reports sending his right-hand section to Badreddine, who is responsible for integration with the PC, MAR, RAM, IR, and Control Unit. His documentation reference already contains PC/MAR/RAM/IR regions, but this does not establish complete control integration. No successful full-system integration result has been provided, and the final combined circuit has not been added to this repository.

- [ ] Add the final simulation in the separately authorized simulation phase and confirm interface definitions.
- [ ] Integrate both sections and check bus ownership, signal polarity, clocking, and reset.
- [ ] Record the actual integration result and supporting evidence from Badreddine and Ihab.

## 4. Complete SAP-1 program execution — pending confirmation

Full-system testing depends on integration of both sections.

- [ ] Define full-system test programs with expected behavior.
- [ ] Run complete instruction/program execution tests and document results.

## Evidence to add

For each reported component/subsystem test, add a reproducible initial state, input sequence, expected and observed outputs, Logisim version, and available supporting artifacts. Store procedures under [tests](../tests/README.md), screenshots under [screenshots](../assets/screenshots/), and diagrams under [diagrams](../assets/diagrams/). Do not invent missing historical observations. For Ihab's section, also record register hold/load behavior, arithmetic carry/overflow boundaries, single-source bus driving, output retention, and the expected signed-display cases; these are pending checks, not completed tests.

TODO: capture the effective RAM settings, decoder truth table, control polarities, and timing/control mapping while documenting the existing successful subsystem tests. Future reruns should be recorded separately from this original report.
