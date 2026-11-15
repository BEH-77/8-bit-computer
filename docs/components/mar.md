# Memory Address Register (MAR)

Badreddine El Habra implemented MAR as one explicitly four-bit Register labeled `MAR`. It holds the address while memory is accessed, allowing the W-Bus to carry another value.

In [Badreddine's circuit](../../simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ), MAR is below the PC. The neighboring four-bit multiplexer selects an address path for RAM; a four-switch bank provides a manual address source. The area is labeled `Lm`, `CLK`, `CLR`, and `Run/Program`.

The intended run-mode transfer is W-Bus → MAR → RAM address. MAR's width matches RAM's four address bits. The Register has no serialized trigger override, so Logisim 4.1.0 supplies its rising-edge default. See the [versioned Register definition](https://github.com/logisim-evolution/logisim-evolution/blob/v4.1.0/src/main/java/com/cburch/logisim/std/memory/Register.java).

The load request's polarity, reset sequence, and `Run/Program` switch positions still need a reproducible procedure. In particular, the primitive's clock default does not establish the phase relationship of the surrounding clock/control wiring.

Badreddine reports successful individual MAR tests and combined subsystem tests. A recorded load/hold sequence and an address-selection check remain to be added to [testing](../testing.md).
