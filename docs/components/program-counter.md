# Program Counter (PC)

## Purpose and SAP-1 role

Retains the instruction address and supplies it for memory addressing during instruction fetch. Implemented by Badreddine El Habra.

## Implementation and width

The PC-labeled region of `main` contains four J-K flip-flops at `(320,250)`, `(420,250)`, `(520,250)`, and `(620,250)`, with associated gates and controlled buffers. This provides four state bits; a nearby splitter explicitly has width 4. The PC is built from primitives rather than a named Counter component.

## Inputs, outputs, and controls

- Clock and clear/start wiring are present in the surrounding canvas.
- Local control annotations are `Cp`, `Ep`, and `CLR`.
- The four-bit address output is associated with controlled buffers toward the region labeled `W Bus`.

Architectural intent: advance the instruction address, clear it for startup, and place the address on the transfer path when enabled. TODO: trace exact `Cp`/`Ep` semantics and polarity, active clock edge, reset value, bit order, and wrap behavior from the wiring and test procedure; annotation names alone do not specify them.

## Connections

In SAP-1, the PC address is transferred to MAR through the shared bus. The current canvas contains PC, MAR, and the bus region; TODO: add a net-level diagram of that transfer and the CU control connections for integration.

## Testing status

**Implemented and manually tested successfully by Badreddine El Habra**, both individually and as part of his combined subsystem in Logisim Evolution, according to his report. Codex did not independently reproduce these functional tests. Detailed evidence is pending; see [testing](../testing.md).

## Known limitations and documentation TODOs

Integration with Ihab Mahiaoui's section and full SAP-1 verification remain pending. These integration and documentation tasks do not change the reported successful status of this component.

TODO: add an annotated diagram, reproducible input/expected-output procedure, and supporting test evidence. Confirm interface details listed above before integration.
