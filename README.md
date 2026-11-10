# FrontierQA Core

Shared Rust engine, standalone CLI, and native bindings for [FrontierQA](https://frontierqa.dev) —
AI-native test reporting and failure triage for Playwright, Pytest and Jest.

**Status:** repository bootstrap. The first working release (`v0.1.0`) will parse JUnit XML and
Playwright JSON, redact secrets, print a pass/fail summary, and write a standardized
`frontierqa-report.json`.

## Crates and packages

| Artifact | Registry | Purpose |
| --- | --- | --- |
| `frontierqa` | crates.io | Standalone CLI |
| `frontierqa-core` | crates.io | Engine library used by the CLI, the API and bindings |
| `@frontierqa/core` | npm | napi-rs bindings with OS-specific `optionalDependencies` |
| `frontierqa-core` | PyPI | PyO3 + maturin wheels (`abi3-py311`) |

## Planned CLI

```bash
frontierqa report ./junit.xml --out frontierqa-report.json
frontierqa report ./playwright-report.json --format playwright --out frontierqa-report.json
```

The report shape is the shared v1 contract documented in the workspace `REASONIX.md`; secrets are
redacted by default (`Bearer …`, `API_KEY=…`, `Authorization:`, tokens, credential URLs).

## Toolchain

- Rust `1.99+`, Edition 2024, MSRV `1.88`
- `cargo-nextest` for tests, `cargo-dist` for releases, `cargo-binstall` for binary installs,
  `sccache` in CI

## Development

```bash
cargo fmt --all --check
cargo clippy --workspace --all-targets -- -D warnings
cargo test --workspace
cargo publish --dry-run -p frontierqa
```

## Repository layout

```text
core/
├── crates/
│   ├── frontierqa/          # CLI binary
│   └── frontierqa-core/     # shared engine library
├── bindings/                # napi-rs and PyO3 crates (v0.2.0)
└── schema/                  # frontierqa-report.json schema copy
```

## License

Licensed under either of

- Apache License, Version 2.0 ([LICENSE-APACHE](LICENSE-APACHE))
- MIT license ([LICENSE-MIT](LICENSE-MIT))

at your option.

Unless you explicitly state otherwise, any contribution intentionally submitted for inclusion in
this project by you, as defined in the Apache-2.0 license, shall be dual licensed as above,
without any additional terms or conditions.

Copyright (c) 2026 FrontierQA.
