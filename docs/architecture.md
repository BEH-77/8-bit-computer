# Architecture

The design follows SAP-1: an eight-bit shared transfer bus, four-bit memory addresses, separate instruction and operand storage, and a gate-based control unit. Ihab's signed decimal display extends the output presentation without adding CPU instructions.

## Circuit organization

Both files contain a single `main` circuit and use built-in Logisim libraries. Component names in this documentation refer to regions on those canvases.

| File | Saved version | Contents |
| --- | --- | --- |
| [Badreddine's circuit](../simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ) | 4.1.0 | PC, MAR, RAM, IR, clock logic, ring counter, decoder, control matrix, plus Ihab's datapath and displays |
| [Ihab's circuit](../simulations/sap-1/ihab-mahiaoui/Our_8Bit_Computer.circ) | 5.0.0 | A, B, ALU, OUT, binary/signed displays, and PC/MAR/RAM/IR regions; no ring counter, instruction decoder, or control matrix |

Badreddine's current file has 254 component records and 1,117 wire records; Ihab's has 165 and 731. These are structural observations, not test results. The files overlap but contain distinct work, so both are retained. Directory names identify their development context rather than exclusive authorship of everything on the canvas.

## Datapath

| Component | Storage or width | Role |
| --- | --- | --- |
| Program Counter | Four J-K flip-flops | Supplies the next instruction address |
| MAR | One four-bit register | Holds the memory address |
| RAM | 16 × 8 bits | Stores instructions and data |
| IR | Two four-bit registers | Holds the instruction's operation and address fields |
| Accumulator A | Two four-bit registers | Holds the first operand or arithmetic result; can drive the W-Bus |
| B register | Two four-bit registers | Holds the second arithmetic operand |
| Adder/subtractor | Two four-bit adders with XOR conditioning | Computes an eight-bit sum or difference; can drive the W-Bus |
| OUT | Two four-bit registers | Holds the value shown by the binary and signed decimal displays |

The RAM address width is explicit in both files. Its eight-bit data width comes from the matching Logisim defaults; see [RAM](components/ram.md). A, B, and OUT use active-low load requests and a shared datapath clock. A and the ALU have separately enabled bus drivers; B and OUT do not drive the bus.

The intended instruction flow is PC → MAR → RAM → IR for fetch. Memory operands then travel through the W-Bus into A or B. The ALU uses A and B continuously, and its result can return through the bus to A. `OUT` transfers A to the output register. This describes the intended sequencing; complete instruction execution has not been demonstrated.

## Control integration

The ring counter supplies a six-line timing interface. The instruction decoder has five labeled outputs: `LDA`, `ADD`, `SUB`, `OUT`, and `HLT`. The control matrix combines timing and instruction selection to generate transfer controls.

The current assembled canvas is not yet an automatically controlled CPU:

- Datapath inputs `LA_N`, `LB_N`, `LO_N`, `EA`, `EU`, and `SU` remain manual pins. Wire inspection finds no connection from the corresponding matrix outputs to these pins.
- A, B, and OUT share the datapath `CLK` pin, separate from the PC/control clock network. Their clear inputs are grounded in both files.
- Matrix labels `La`, `Lb`, `Lo`, `Ea`, `Eu`, and `Su` suggest the corresponding functions, but load polarity and timing must be reconciled before wiring the interfaces.

Badreddine is responsible for integration following Ihab's reported handoff. The next work is to connect the control interfaces, agree on clock/reset behavior, check bus ownership, and run complete programs. Existing subsystem reports are preserved in [testing](testing.md); they do not establish a pass for this assembled version.

## Source details to keep in mind

The control matrix is mistakenly headed `4 to 5 decoder`, duplicating the actual decoder's heading. The MAR heading spells “Adress”. These annotations are unchanged in the circuits; the documentation uses the intended component names.

The ALU wraps at eight bits and has no carry/overflow flag register. The signed display interprets OUT as two's complement, from -128 to +127. Its divide-by-10 components are display conversion logic, not a division instruction.
