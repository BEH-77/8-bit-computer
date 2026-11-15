# Registers and displays

**Ihab Mahiaoui confirmed that he implemented the accumulator A, B register, output register, binary display, and signed decimal display**, as well as the [adder/subtractor](alu.md). All six are completed implementation work. The signed decimal display is an additional Logisim visualization feature, not a required component of the original textbook SAP-1.

Implementation details below combine Ihab's supplied technical report with static inspection of `Our_8Bit_Computer.circ`, identifying Logisim Evolution 5.0.0. It is a documentation reference supplied outside the repository, with one `main` circuit; these sections are canvas regions, not named subcircuits. See [provenance](../../simulations/sap-1/ihab-mahiaoui/README.md).

## Common register behavior

A, B, and OUT each use two explicitly four-bit, classic-appearance Register primitives. Their six clock inputs share the pin labeled `CLK`. Their clear inputs are wired to Ground, so these registers have no externally driven clear in this reference circuit. A power-on value or full-system reset sequence has not been verified.

The load signals `LA_N`, `LB_N`, and `LO_N` each pass through a NOT gate before reaching their register pair's active-high enable inputs. Ihab confirms rising-edge loading from the shared eight-bit W-Bus: a low load request captures the bus value; a high request retains the stored value. No trigger attribute is serialized; the [Logisim Evolution 5.0.0 Register definition](https://github.com/logisim-evolution/logisim-evolution/blob/v5.0.0/src/main/java/com/cburch/logisim/std/memory/Register.java) supplies the same rising-edge default. This is the documented operating contract, not an exhaustive timing test.

## Accumulator A

**Purpose and width:** retain the eight-bit working value and arithmetic result. In SAP-1 it supplies one arithmetic operand and can place its value on the transfer bus.

**Implementation:** `A_LOW` at `(1090,350)` stores A0–A3; `A_HIGH` at `(1260,360)` stores A4–A7. The pair receives the W-Bus through four-bit splitter groups and shares `LA_N` and `CLK`. Its outputs feed the low/high adder inputs directly and splitters leading to eight one-bit controlled buffers.

**Operation and connections:** loading is independent of output enabling. `EA` drives the eight buffer control pins, providing an active-high output enable. A's stored value remains available to the arithmetic path when its bus output is disabled. The wider SAP-1 design will use memory/bus transfers to load A and the ALU result path to update it.

**Design and testing:** the two-nibble storage and separate direct-ALU/buffered-bus paths are Ihab's documented choices. He manually tested storage and bus output: with `A_HIGH=0x3`, `A_LOW=0x5`, and `EA=1`, the expected and observed W-Bus value was `0x35` (`00110101`). This reported success does not establish every load/hold or bus-sharing case. TODO: capture the exact loading/clock procedure and verify memory/ALU transfers and the agreed reset interface during integration.

## B register

**Purpose and width:** retain the eight-bit second operand while A holds the first operand or result.

**Implementation:** `B_LOW` at `(1340,760)` stores B0–B3; `B_HIGH` at `(1340,870)` stores B4–B7. Their four-bit data inputs come from the W-Bus, with shared `LB_N` and `CLK`. Output splitters feed the eight `XOR_B0` through `XOR_B7` gates in the arithmetic section.

**Operation and connections:** B loads from the transfer path on an enabled clock edge and otherwise retains its operand. `SU` controls the downstream XOR logic; it does not change the stored B value. B supplies the [adder/subtractor](alu.md), rather than a separately enabled B-to-bus output.

**Design and testing:** operand storage is separate from the conditional complement logic, and B does not directly drive the W-Bus. Ihab reports successful basic combined B-register/ALU operation after connecting these paths. A standalone B-register load/hold test report was not supplied. TODO: record its actual stimuli/results and broader operand coverage.

## Output register

**Purpose and width:** retain an eight-bit output value so the displays can remain stable while the working datapath changes.

**Implementation:** `OUT_LOW` at `(1410,1330)` stores output bits 0–3; `OUT_HIGH` at `(1410,1420)` stores bits 4–7. Their four-bit inputs come from the W-Bus, with shared `LO_N`/`CLK` controls.

**Operation and connections:** the pair captures the transfer-path value on an enabled clock edge. Its outputs feed the binary LED splitters and the decimal-conversion section. The intended SAP-1 `OUT` transfer places A on the bus and loads OUT; that complete instruction sequence has not been verified.

**Design and testing:** the display value has its own storage rather than following the live arithmetic result, and OUT does not drive the W-Bus. Implementation is complete; detailed final test evidence is still needed before declaring output capture and retention passed. TODO: record actual capture/hold results, including retention while A changes and startup behavior.

## Binary display

**Purpose and width:** present the output register's eight stored bits directly as visible binary indicators.

**Implementation and operation:** eight LED primitives are placed at x=1810 through 2020, y=1950. Two four-bit splitters connect the output-register paths to the display wiring. There is no separate display load signal; the upstream output register supplies the retained value.

**Connections and testing:** Ihab describes the LEDs as D7 through D0, with ON representing 1 and OFF representing 0. They show OUT's raw bit pattern independently of signed interpretation: `00001000` represents 8; `11111110` represents -2 when interpreted as two's complement. These examples explain representation, not completed test cases. Detailed final LED test evidence remains pending; TODO: record observed patterns and an annotated display-bit map.

## Decimal display

**Purpose and width:** render the output byte as a signed two's-complement decimal value, from -128 through +127. This display extension leaves the underlying stored byte and arithmetic logic unchanged; it does not simultaneously display the full unsigned range 0–255.

**Internal logic:** the output-register paths feed an eight-bit recombination splitter, a Negator, and an explicitly eight-bit Multiplexer. The conversion section contains two Dividers, two eight-bit constants equal to decimal 10, two eight-bit zero constants, and three Bit Extenders with four-bit outputs. The [5.0.0 Negator](https://github.com/logisim-evolution/logisim-evolution/blob/v5.0.0/src/main/java/com/cburch/logisim/std/arith/Negator.java) defaults to eight bits; the [Divider](https://github.com/logisim-evolution/logisim-evolution/blob/v5.0.0/src/main/java/com/cburch/logisim/std/arith/Divider.java) defaults to eight-bit unsigned division where these attributes are omitted.

**Operation and outputs:** Ihab confirms that D7 selects the original byte when clear and the negated byte when set. The selected magnitude is interpreted as unsigned for decimal extraction. The first divide-by-10 stage supplies the units remainder; its quotient feeds the second stage, whose remainder is tens and quotient is hundreds. Bit Extenders reduce these values to four-bit inputs for three Hex Digit Displays. The intended digit values are 0–9, so these primitives present decimal digits. D7 also drives segment `g` of a separate 7-Segment Display to show the minus sign.

**Controls and design:** this is combinational display logic driven by OUT, without a separate load or arithmetic-instruction control. Division is used for display conversion, not as a CPU instruction. For -128, the eight-bit negation yields `0x80`, which the unsigned magnitude path interprets as 128.

The following are **expected examples supplied by Ihab, not a record of passed tests**:

| Stored bits | Signed value | Expected display |
| --- | --- | --- |
| `00000000` | 0 | `000` |
| `00001000` | 8 | `008` |
| `01111111` | 127 | `127` |
| `11111111` | -1 | `-001` |
| `11111110` | -2 | `-002` |
| `10000000` | -128 | `-128` |

**Testing and limitations:** implementation is complete; comprehensive verification of positive, negative, zero, and boundary cases remains pending. TODO: run and record the cases above, including magnitude routing, sign-segment behavior, and displayed leading zeros, with expected/observed values and evidence.

## Testing status and integration

All five components on this page are implemented. A's storage/bus-output test and basic B-register/ALU combined operation were manually tested successfully according to Ihab. Final output/LED evidence and comprehensive decimal-display verification remain pending. No complete six-component test pass is inferred. These scopes, cross-section integration, and program execution are tracked separately in [testing](../testing.md); static inspection is not a functional test pass.

Badreddine's PC, MAR, RAM, IR, Control Matrix, Ring Counter, and 4-to-5 Decoder retain their existing attribution and reported successful individual/combined tests. Ihab reports sending his section to Badreddine, who is responsible for integration; successful integration has not been confirmed. TODO: agree on control-signal mapping, bus ownership, clocking, and reset; add reproducible test procedures and supporting diagrams. Manual stimulus controls must not be presented as the final automatic CPU interface without confirming the integrated design.
