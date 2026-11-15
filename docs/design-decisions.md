# Design decisions

## Build SAP-1 before extending the architecture

SAP-1 gives us a defined set of register transfers and five instruction targets to implement and test. The more advanced computer is still a future design; its register set, memory organization, instruction encoding, and control approach are undecided.

## Use paired four-bit datapath registers and adders

Ihab built each of A, B, and OUT from two four-bit registers. Two four-bit adders form the eight-bit arithmetic path, with a carry connection between them. XOR gates on B and the initial carry input let the same path perform addition and subtraction. The final carry is unused, and no status register is implemented.

## Separate bus access from storage and computation

A and the ALU have controlled W-Bus outputs. A and B feed the arithmetic path continuously, while OUT retains the displayed value independently of the working registers. B and OUT do not drive the bus. The active-low register load requests are inverted before Logisim's active-high enable inputs.

## Add signed output as a display extension

The binary LEDs show OUT's raw bits. The decimal path interprets the same byte as two's complement and converts its magnitude into decimal digits. This adds a readable signed display without changing the instruction set or arithmetic storage.

## Keep both development circuits

The files share some PC/memory and datapath content, but neither is a duplicate of the other. Ihab's file retains his datapath/display development context; Badreddine's also contains the timing and control logic. Both remain under their existing paths while automatic integration is completed.

The integration decisions still to settle are load-signal polarity at the matrix boundary, clock phases, shared reset, bus ownership, and the Logisim version used for the combined circuit. See [architecture](architecture.md) for the current connection gaps.
