# Random Access Memory (RAM)

## Purpose and SAP-1 role

Stores values used as instructions and data for the SAP-1 datapath. Implemented by Badreddine El Habra.

## Implementation and width

One Logisim RAM component is present at `(380,640)`, with explicit `addrWidth=4`: **16 addressable locations**. Its data width is not explicitly serialized in this file. Nearby splitters have explicit width 8 and a controlled buffer at `(660,730)` has width 8, supporting an eight-bit transfer path. TODO: inspect the effective RAM Data Bits setting in Logisim before documenting the complete memory geometry as confirmed.

## Inputs, outputs, and controls

The memory region contains address selection, switches, a controlled output path, and annotations `Run/Program`, `CLK`, and `CE` (appearing twice). These annotations are observed text, not a verified port specification.

Architectural intent: accept an address and supply the selected stored value; manual programming controls support loading memory contents. TODO: document address/data pin mapping, read/write controls, mode selection, `CE` polarity, clock behavior, and data persistence. Do not infer effective settings from omitted XML attributes.

## Connections and operation

MAR and the adjacent address multiplexer occupy the address path region; the IR and `W Bus` are part of the surrounding transfer path. TODO: add a wiring diagram showing the actual address, programming-data, and memory-output routes. No reproducible program image or memory-loading procedure is supplied as test evidence.

## Testing status

**Implemented and manually tested successfully by Badreddine El Habra**, both individually and as part of his combined subsystem in Logisim Evolution, according to his report. Codex did not independently reproduce these functional tests. Detailed evidence is pending; see [testing](../testing.md).

## Known limitations and documentation TODOs

Integration with Ihab Mahiaoui's section and full SAP-1 verification remain pending. These integration and documentation tasks do not change the reported successful status of this component.

TODO: add an annotated diagram, reproducible input/expected-output procedure, and supporting test evidence. Confirm interface details listed above before integration.
