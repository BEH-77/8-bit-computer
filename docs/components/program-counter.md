# Program Counter (PC)

Badreddine El Habra implemented the PC to hold the next instruction address. Its four-bit output is intended to reach MAR through the low four bits of the W-Bus during fetch.

In [Badreddine's circuit](../../simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ), the PC uses four J-K flip-flops near the top left of `main`, with gates for counting and controlled buffers for bus output. It is built from primitives rather than Logisim's Counter component. Nearby controls are labeled `Cp`, `Ep`, and `CLR`.

| Control | Intended role |
| --- | --- |
| `Cp` | Advance the instruction address |
| `Ep` | Enable the address output onto the bus |
| `CLR` | Clear the counter for startup |

The surrounding circuit includes automatic/manual clock selection, single-step control, and halt logic. The effective PC clock edge, reset sequence, control polarities, and wrap from address 15 to 0 still need a recorded operating procedure; the labels alone do not define those details.

Badreddine reports successful individual PC tests and tests with his memory/control subsystem. Exact inputs and observed counts are not recorded. See [testing](../testing.md) for the evidence still needed.
