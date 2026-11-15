# SAP-1 simulations

| Circuit | Saved version | What to inspect |
| --- | --- | --- |
| [sap1-pc-memory-control.circ](badreddine-el-habra/sap1-pc-memory-control.circ) | Logisim Evolution 4.1.0 | PC/memory at upper left, timing/decoder/matrix below, A/B/ALU/OUT to the right, displays below the datapath |
| [Our_8Bit_Computer.circ](ihab-mahiaoui/Our_8Bit_Computer.circ) | Logisim Evolution 5.0.0 | Ihab's registers, arithmetic, and displays alongside PC/memory regions; no instruction-control section |

Open either file with **File → Open**, select `main`, and zoom out to find the labels. Each has one large canvas and built-in libraries only. The source version identifies the version saved in the XML, not a cross-version compatibility guarantee.

## Operating limits

Badreddine's current file contains both contributors' sections, but the right-hand datapath still uses manual `LA_N`, `LB_N`, `LO_N`, `EA`, `EU`, `SU`, and `CLK` inputs. The clock/start area also has `Clear/Start`, `manual/auto`, and `single step` controls. A complete startup, programming, and execution procedure has not yet been recorded.

RAM triggering differs: Badreddine's file explicitly uses high-level triggering; Ihab's uses the default rising edge. Inspect the effective settings before attempting the same memory-loading sequence in both files.

For implementation details, read [architecture](../../docs/architecture.md). For reported manual results and checks still needed, read [testing](../../docs/testing.md). Neither file is documented as a verified automatically executing CPU.

## File history

Badreddine's initial repository import came from `SAP_1.circ`; the byte-identical root copy was removed at that time. The current file has since changed and now includes the datapath/display regions, so the original import checksum no longer describes it.

Ihab's [source notes](ihab-mahiaoui/README.md) describe his retained development file. Both current circuits were preserved byte for byte during the documentation review; Git records their versions.
