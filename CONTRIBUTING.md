# Contributing

Badreddine El Habra and Ihab Mahiaoui maintain this project together.

1. Start a focused branch from `main`, such as `docs/test-evidence` or `feat/sap1-integration`.
2. Make a small, reviewable change with a meaningful commit message. Keep `.circ` sources in version control; avoid unrelated XML rewrites and generated backups.
3. Open changed circuits in the appropriate Logisim Evolution version and run relevant manual checks. Record stimuli, expected and observed behavior, and evidence in [testing.md](docs/testing.md). Distinguish reported results from independently reproduced tests.
4. Update affected documentation and the `Unreleased` changelog. Credit the actual contributors; ask before assigning undocumented work to someone.
5. Open a pull request for the other contributor to review. Resolve circuit/interface concerns and verify the change before merging to `main`.

Use [the organized simulation](simulations/sap-1/badreddine-el-habra/sap1-pc-memory-control.circ) for development. Coordinate circuit edits to avoid simultaneous XML changes; inspect diffs carefully rather than automatically resolving circuit conflicts.

For integration, first agree on bus widths, signal names and polarities, clocking, reset, and ownership of shared wiring. Complete SAP-1 integration and verification remain pending. Add future assembler or Arduino directories only when development begins.

Licensing is undecided; both contributors should agree before replacing the [license placeholder](LICENSE).
