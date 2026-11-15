# Ihab Mahiaoui's SAP-1 section

Ihab Mahiaoui completed the accumulator A, B register, adder/subtractor, output register, binary LED output, and signed decimal conversion/display. See [arithmetic documentation](../../../docs/components/alu.md), [registers and displays](../../../docs/components/other-components.md), and the scoped [testing record](../../../docs/testing.md).

## Documentation reference

Ihab supplied `Our_8Bit_Computer.circ` for read-only documentation inspection, alongside his technical/testing notes. It is not copied into this repository by the documentation update and is not asserted to be the final combined simulation.

- Saved source version: Logisim Evolution **5.0.0**, XML project format `1.0`.
- One circuit named `main`, with 165 components and 731 wire records; built-in library references only.
- Inspected file size: **55,977 bytes**.
- SHA-256 of the supplied reference:

```text
11119d2d4bb87c23867f6d5499267852155a6aa951cb88727f38f72a6376e546
```

This checksum identifies the inspected reference; it is not a checksum for a future final submission. The file was not changed. XML parsing and selected wire tracing do not constitute functional verification.

The reference contains PC/MAR/RAM/IR regions alongside Ihab's confirmed six components. Those regions do not change Badreddine's attribution. The complete control matrix, ring counter, and instruction decoder are not present in this reference; a single canvas and manual controls do not establish complete SAP-1 integration.

## Testing and later submission

Ihab reports a successful accumulator storage/bus-output test and basic arithmetic/B-register–ALU operation. Final output/LED evidence and comprehensive signed-display verification remain pending. His decimal display is an additional visualization feature beyond textbook SAP-1.

Ihab reports handing his section to Badreddine for integration. Successful integration and complete program execution are not yet confirmed. The final combined `.circ` file will be supplied separately.

Place the later submission in `simulations/sap-1/ihab-mahiaoui/` for inspection when the simulation phase is explicitly requested. At that stage, confirm its actual scope, select the appropriate final location under `simulations/sap-1/`, and update these notes without creating unnecessary duplicate circuits or replacing either contributor's original work. No final filename, integration result, or successful execution is assumed here.
