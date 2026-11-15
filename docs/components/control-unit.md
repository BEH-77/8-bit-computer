# Control unit

Badreddine El Habra implemented the ring counter, instruction decoder, and control matrix in the lower part of [his circuit](../../simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ). Together they select which transfers occur at each instruction step.

## Ring counter

The timing region uses J-K flip-flops, a six-way splitter, and a six-column LED bar. A second six-bit splitter feeds the matrix region. This establishes a six-line timing interface; the initialized state, state order, one-hot behavior, and effective clock edge still need a recorded trace.

The surrounding clock circuitry has `Clear/Start`, `HLT`, `manual/auto`, and `single step` annotations. Their operating sequence and relationship to timing reset are not yet documented as a runnable procedure.

## Instruction decoder

A four-bit splitter, four NOT gates, and five four-input AND gates form the decoder. The outputs are labeled `LDA`, `ADD`, `SUB`, `OUT`, and `HLT`. Decoder output wires reach the lower control matrix; the `HLT` output also routes toward the clock logic.

The actual opcode truth table and input bit order remain to be transcribed. The five labels identify supported targets, but do not establish complete instruction execution or behavior for the other opcode combinations. See [instruction set](../instruction-set.md).

## Control matrix

The lower gate network contains 19 AND gates and six OR gates. Its heading incorrectly repeats `4 to 5 decoder`; it is the control matrix, distinct from the decoder above it.

| Output annotations | Intended receivers/functions |
| --- | --- |
| `Cp`, `Ep` | PC count and bus output |
| `Lm`, `CE`, `Li`, `Ei` | MAR load, memory output, IR load and address-field output |
| `La`, `Ea` | Accumulator load and bus output |
| `Lb`, `Su`, `Eu` | B load, subtract selection, ALU bus output |
| `Lo` | Output-register load |

These names describe intended functions. The Boolean equations, active levels, and timing-state mapping still need to be recorded before this table can serve as an electrical interface specification.

## Connection status

Some matrix outputs route back toward the PC/memory section. The outputs labeled `Lo`, `Lb`, `Eu`, `Su`, `Ea`, and `La` end on local wire stubs; they do not reach the separate datapath pins `LO_N`, `LB_N`, `EU`, `SU`, `EA`, and `LA_N`. The datapath also retains its own manual `CLK` input.

The `_N` load inputs are active-low and are inverted before the register enables. Matching their names to matrix labels is not enough: receiving polarity, timing, bus ownership, and shared reset must be checked during integration.

Badreddine reports successful individual tests of all three control components and combined tests with his PC/memory section. No timing trace or complete program result is supplied. The [testing record](../testing.md) retains those results and lists the remaining integration checks.
