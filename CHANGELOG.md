# Changelog

## Unreleased

- Retained the updated PC/memory/control canvas and added Ihab's datapath/display circuit. Automatic control integration and full-system verification remain pending.
- Updated architecture and component documentation against both current circuit files, including manual control/clock boundaries, RAM defaults, and differing RAM trigger settings.
- Consolidated test-record guidance into `docs/testing.md` and renamed the register/display page for easier navigation.
- Shortened the README, contributor records, roadmap, and review templates; removed obsolete submission instructions and empty artifact directories.

## Initial repository work

- Imported Badreddine's PC, MAR, RAM, IR, ring counter, decoder, and control matrix, preserving his reported individual and combined manual test results.
- Documented Ihab's accumulator, B register, ALU, output register, binary LEDs, and signed decimal display, along with his reported accumulator and basic arithmetic tests.
- Added architecture/component notes, contribution guidance, and an undecided-license notice. Removed the byte-identical root circuit copy after the initial import.
