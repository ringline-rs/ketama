# CLAUDE.md

## Build & Test Commands

```bash
# Build
cargo build

# Lint
cargo fmt --all -- --check
cargo clippy --all-targets -- -D warnings

# Test
cargo test --all
cargo test --all --release

# Docs
RUSTDOCFLAGS="-D warnings" cargo doc --no-deps
```

## Architecture

Ketama consistent hash ring implementation. Zero external dependencies.

### Key Types

- `Ring` — immutable consistent hash ring, routes keys to shard indices
- `RingBuilder` — builder pattern for constructing rings with weighted nodes
