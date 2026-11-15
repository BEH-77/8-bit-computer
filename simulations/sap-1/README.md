# SAP-1 simulations

Badreddine El Habra and Ihab Mahiaoui developed separate Logisim Evolution sections. Badreddine reports that his components passed individual and combined subsystem manual tests. Ihab reports successful accumulator storage/bus-output and basic arithmetic/B-register–ALU tests, with final output/display verification still pending. He reports handing his section to Badreddine for integration; successful full integration and complete SAP-1 execution remain unconfirmed.

- [Badreddine's simulation](badreddine-el-habra/sap1-pc-memory-control.circ): PC, MAR, RAM, IR, Control Matrix, Ring Counter, and 4-to-5 Decoder on a single `main` canvas.
- [Ihab's contribution and reference notes](ihab-mahiaoui/README.md): accumulator A, B register, adder/subtractor, output register, binary LEDs, and signed decimal display are documented; the final circuit addition is deferred to the simulation phase.

## Opening and provenance

Open Badreddine's committed `.circ` file through File → Open in Logisim Evolution, preferably 4.1.0, the version identified in its XML. Use the `main` circuit and scroll to the component regions. Controls include annotations for `Clear/Start`, `manual/auto`, and `single step`; TODO: document a precise manual test procedure before treating these labels as an operating guide. Ihab's separately supplied documentation reference identifies 5.0.0; compatibility between the versions has not been tested.

The supplied source was named `SAP_1.circ`. It was compared byte for byte with the organized copy before the redundant root file was removed. The retained circuit is unchanged: 44,851 bytes with SHA-256:

```text
9b6d15d2ae4f78b0b37e1a8fb19cd7821abec97d35e2370b1d0f37ce3b90dfef
```

Make reviewed future changes in the organized simulation path. This checksum records the initial import, not a requirement that future development remain unchanged.

XML parsing and byte comparison were performed during initial repository preparation. In that environment, Logisim Evolution was installed, but GUI startup failed because it could not connect to X11. Codex did not independently verify opening or reproduce the manual functional tests. The later Ihab documentation update used static inspection and his attributed manual test report; it did not execute either simulation or modify a circuit.

See [architecture inspection](../../docs/architecture.md), [control unit](../../docs/components/control-unit.md), and [testing](../../docs/testing.md) for observations, reported results, and evidence TODOs.
