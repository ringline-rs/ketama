# ketama

Ketama consistent hash ring compatible with libmemcached/twemproxy.

A zero-dependency implementation of the ketama consistent hashing algorithm.
Adding or removing a server remaps only ~1/N of keys instead of all keys.

## Features

- MD5-based virtual nodes (160 per server at weight 1)
- Weighted node support
- Compatible with libmemcached/twemproxy ketama algorithm
- Zero external dependencies

## Usage

```toml
[dependencies]
ketama = "0.0.1"
```

```rust
use ketama::Ring;

// Build a ring with 3 servers
let ring = Ring::build(&["server1:11211", "server2:11211", "server3:11211"]);

// Route a key to a server index
let shard = ring.route(b"my-cache-key");
```

## License

Licensed under either of [Apache License, Version 2.0](LICENSE-APACHE) or
[MIT License](LICENSE-MIT) at your option.
