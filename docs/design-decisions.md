# Design decisions

These decisions describe the initial repository arrangement, without inventing historical design dates.

| Decision | Reason |
| --- | --- |
| Keep SAP-1 as the current documented scope | It is the supplied design; the advanced architecture is undecided. |
| Store simulations under contributor names | Preserve provenance before the two sections are integrated. |
| Copy the supplied circuit without rewriting XML | Preserve Badreddine's existing implementation and manual-test baseline. |
| Keep one circuit source under the contributor directory | Remove the byte-identical root duplicate; retain its import checksum in the simulation notes. |
| Distinguish reported manual tests from inspection | XML presence cannot demonstrate functional behavior. |
| Defer assembler and Arduino directories | Their requirements depend on future architecture decisions. |
| Leave licensing undecided | No license choice has been authorized by the contributors. |

TODO: record integration decisions about signal polarity, bus ordering, clock/reset interfaces, and the combined circuit location when agreed. See [source observations](architecture.md) for label discrepancies that require confirmation rather than silent edits.

## Ihab's implemented datapath and display decisions

These choices are described in Ihab's technical report and supported by the supplied reference where noted on the component pages. They are previously completed design work, not newly implemented circuits in this documentation update.

| Decision | Implemented effect |
| --- | --- |
| Use two four-bit registers for each eight-bit A, B, and OUT register | Low/high nibbles share clock and load control. |
| Invert `LA_N`, `LB_N`, and `LO_N` before Register enables | Active-low load requests drive Logisim's active-high enable inputs. |
| Share the W-Bus through controlled buffers | A uses `EA`; the ALU uses `EU`. Only one bus-driving source should be enabled at a time. B and OUT do not drive the bus. |
| Connect A and B directly to arithmetic inputs | The ALU receives stored operands continuously, independent of W-Bus output enabling. |
| Use `SU` for XOR conditioning and initial carry | One adder chain performs both addition and two's-complement subtraction; the final carry is unused. |
| Keep arithmetic at eight bits without a status register | Results wrap modulo 256; signed overflow is not reported by a dedicated flag. |
| Add signed decimal conversion after OUT | D7 selects sign/magnitude presentation; raw stored bits and arithmetic are unchanged. This is a visualization extension with an intended range of -128 through +127. |
| Separate manual tests from automatic execution | Reported accumulator/basic arithmetic results do not establish full instruction or program execution. |
| Document now and add the final simulation separately | Preserve both contributors' circuits and keep this change focused on documentation. |

Badreddine is responsible for integration, according to Ihab's handoff report. Shared reset, final control wiring, retained manual controls, source-version compatibility, and the final combined circuit organization still require confirmation. See [architecture](architecture.md) and [testing](testing.md).
