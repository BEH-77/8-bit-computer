# Ihab Mahiaoui's SAP-1 circuit

[Our_8Bit_Computer.circ](Our_8Bit_Computer.circ) contains Ihab's accumulator, B register, adder/subtractor, output register, binary LEDs, and signed decimal display. It also includes PC/MAR/RAM/IR regions from the shared design; these do not change the [division of responsibilities](../../../docs/contributors.md).

The file identifies Logisim Evolution 5.0.0 and has one `main` circuit using built-in libraries. It is the same 55,977-byte file previously inspected for Ihab's contribution documentation, with SHA-256:

```text
11119d2d4bb87c23867f6d5499267852155a6aa951cb88727f38f72a6376e546
```

A, B, and OUT share a manual `CLK` pin and active-low load controls. A and the ALU have separate bus enables. There is no ring counter, instruction decoder, or control matrix in this file. It is a development circuit, not the final automatically controlled computer.

Ihab reports successful accumulator storage/bus output and basic arithmetic/B-register–ALU operation. Final output/display verification remains pending. See [ALU](../../../docs/components/alu.md), [registers and displays](../../../docs/components/registers-and-displays.md), and [testing](../../../docs/testing.md).
