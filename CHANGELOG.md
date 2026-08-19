# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.0.2] - 2026-08-19

### Fixed

- `RingBuilder::build` validates the ring instead of producing one that fails
  later:
  - More than `u16::MAX` nodes is now rejected. Shard indices are stored as
    `u16`, so beyond that they wrapped: with 65538 nodes `Ring::node_count`
    reported 2 while `Ring::route` returned indices up to 65534, and a caller
    indexing by the returned shard read out of bounds.
  - A ring in which every node has weight 0 is now rejected at build time. It
    previously built successfully with zero virtual points and then panicked
    with an index-out-of-bounds inside `Ring::route`, deferring a configuration
    error to request time.
  - A node whose virtual-point count overflows `usize` is rejected rather than
    wrapping, which can happen on 32-bit targets for large weights.

  A weight-0 node alongside weighted nodes remains valid and simply takes no
  points.

## [0.0.1] - 2026-02-21

### Added

- Initial release extracted from ringline workspace
- Ketama consistent hash ring with MD5-based virtual nodes
- Compatible with libmemcached/twemproxy ketama algorithm
- Builder pattern with weighted node support
- Inline MD5 implementation (zero external dependencies)
