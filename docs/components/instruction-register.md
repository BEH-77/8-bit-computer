# Instruction Register (IR)

## Purpose and SAP-1 role

Retains an instruction so that its operation and address fields can be used by the control and memory paths. Implemented by Badreddine El Habra.

## Implementation and width

The IR-labeled region contains Register components at `(310,980)` and `(450,980)`, each explicitly **4 bits**: eight bits of register storage across the pair. Nearby splitters are explicitly four bits, and the controlled buffer at `(550,1010)` is explicitly four bits. This is a two-register implementation rather than a single named eight-bit IR component.

## Inputs, outputs, and controls

- Architectural input: an instruction from the memory/bus transfer path.
- Architectural outputs: an operation field for decoding and an address/operand field for transfers.
- Nearby annotations: `Li`, `Ei`, `CLK`, and `CLR`.

Architectural intent: load and retain an instruction, present an operation field to the decoder, and permit address-field transfer under control. TODO: document the actual mapping of each four-bit register to the fields, input/output bit order, `Li`/`Ei` polarity, clock edge, and clear behavior. These details are not inferred solely from text labels.

## Connections

The source places IR below RAM and above the CU. The four-to-five decoder region has a four-bit splitter. TODO: diagram the precise memory/bus-to-IR and IR-to-decoder/transfer connections and confirm the instruction encoding against the [instruction-set record](../instruction-set.md).

## Testing status

**Implemented and manually tested successfully by Badreddine El Habra**, both individually and as part of his combined subsystem in Logisim Evolution, according to his report. Codex did not independently reproduce these functional tests. Detailed evidence is pending; see [testing](../testing.md).

## Known limitations and documentation TODOs

Integration with Ihab Mahiaoui's section and full SAP-1 verification remain pending. These integration and documentation tasks do not change the reported successful status of this component.

TODO: add an annotated diagram, reproducible input/expected-output procedure, and supporting test evidence. Confirm interface details listed above before integration.
