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
