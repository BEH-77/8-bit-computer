# Contributing

Badreddine El Habra and Ihab Mahiaoui maintain this project together.

Use a focused branch from `main` and open a pull request for the other contributor to review. Describe the change and the checks performed. Update affected documentation; use the [changelog](CHANGELOG.md) for meaningful changes.

Coordinate circuit edits before working on the same `.circ` file. Keep the existing [simulation paths](simulations/sap-1/README.md), inspect XML diffs for unintended changes, and do not commit editor backups or autosaves. Resolve circuit conflicts by checking the design in Logisim rather than accepting XML changes blindly.

For a circuit change, record the Logisim version, initial state, inputs, expected behavior, and observed result using the guidance in [testing](docs/testing.md). Distinguish component/subsystem tests from complete program execution. For documentation changes, check links and compare technical claims with the relevant circuit.

Both contributors should agree before replacing the [license notice](LICENSE).
