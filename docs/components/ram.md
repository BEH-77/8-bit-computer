# RAM

Badreddine El Habra implemented the memory section using one Logisim RAM component. It provides 16 eight-bit locations for instructions and data.

Both circuit files explicitly set `addrWidth=4` and omit the data-width attribute. The matching [4.1.0 RAM defaults](https://github.com/logisim-evolution/logisim-evolution/blob/v4.1.0/src/main/java/com/cburch/logisim/std/memory/RamAttributes.java) and [5.0.0 RAM defaults](https://github.com/logisim-evolution/logisim-evolution/blob/v5.0.0/src/main/java/com/cburch/logisim/std/memory/RamAttributes.java) set data width to eight bits. Nearby eight-bit splitters and the memory output buffer agree with that geometry.

## Address and data paths

MAR and a manual four-switch address source feed the address-selection area. An eight-bit switch bank supplies programming data. A controlled eight-bit output path connects memory data toward the W-Bus and instruction register. The visible annotations include `Run/Program`, `CE`, and `CLK`.

The RAM configuration differs between files: Badreddine's current RAM explicitly uses `trigger="high"` (high-level triggering), while Ihab's file omits that attribute and uses the 5.0.0 rising-edge default. Do not apply one memory-loading sequence to both files without checking their effective settings.

## Testing and remaining work

Badreddine reports successful individual RAM tests and combined memory/control tests. No memory image or complete load/readback procedure is included. Record the mode-switch positions, address/data bit order, write controls, `CE` polarity, and expected readback before using this section as a programming guide. Startup contents and persistence between simulation sessions have not been documented.

See [testing](../testing.md) for the distinction between these reported results and pending program execution.
