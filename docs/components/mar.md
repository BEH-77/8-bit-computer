# Memory Address Register (MAR)

## Purpose and SAP-1 role

Holds the address used to access RAM. Implemented by Badreddine El Habra.

## Implementation and width

The Register at `(390,470)` is labeled `MAR` and explicitly configured to **4 bits**. A nearby multiplexer at `(550,550)` is explicitly 4 bits, with a four-switch bank in the same memory-address region. The original heading spells “Memory Adress Register”; the source is preserved.

## Inputs, outputs, and controls

- Address input: four-bit address value to be retained.
- Address output: stored four-bit value for memory addressing.
- Nearby annotations: `Lm`, `CLK`, and `CLR`.

Architectural intent: latch an address under load control and retain it between transfers. TODO: record the actual input path, `Lm` polarity, active clock edge, and reset behavior from wiring/test evidence.

## Connections and operation

SAP-1 uses MAR between the address transfer path and RAM. The surrounding circuit also includes address selection and a `Run/Program` annotation. TODO: trace the multiplexer selection and distinguish run-mode addressing from manual programming before publishing operating instructions. RAM's explicit address width is also four bits.

## Testing status

**Implemented and manually tested successfully by Badreddine El Habra**, both individually and as part of his combined subsystem in Logisim Evolution, according to his report. Codex did not independently reproduce these functional tests. Detailed evidence is pending; see [testing](../testing.md).

## Known limitations and documentation TODOs

Integration with Ihab Mahiaoui's section and full SAP-1 verification remain pending. These integration and documentation tasks do not change the reported successful status of this component.

TODO: add an annotated diagram, reproducible input/expected-output procedure, and supporting test evidence. Confirm interface details listed above before integration.
