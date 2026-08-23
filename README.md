# Rust Workspace Template

An intentionally empty stable Rust workspace with shared lint policy and guidance for agents.

## Start a project

Create the crates the project needs:

```bash
cargo new crates/my-crate
```

Cargo automatically adds workspace lint inheritance to the new crate. Keep this generated configuration:

```toml
[lints]
workspace = true
```

Add this attribute to each crate root and integration-test root:

```rust
#![cfg_attr(
    test,
    allow(
        clippy::missing_errors_doc,
        clippy::missing_panics_doc,
        reason = "tests report failures rather than document callable contracts"
    )
)]
```

## Verify

The workspace has no build targets until its first crate exists. After creating one, run:

```bash
cargo fmt
cargo clippy --workspace --all-targets
cargo test --workspace
```

Resolve every warning before considering work complete.
