# 02 — Architecture overview

**Architecture:** Thryvane · **Status:** Proposed

Layers: value/register model, instruction encoding and semantics, execution and retirement, memory and translation, protection and events, platform reset/boot, executable format and ABI.

## Grouped-state investigation
A 512-bit value may be exposed as a monolithic scalar, as a group of narrower architectural elements, or through explicit views. The design must choose deliberately and specify aliasing, partial writes, ordering, and whether a write to one view changes another.

The first reference profile should be deterministic and single-core. Speculation, out-of-order execution, multicore, and cache coherence are deferred.

Register width does not dictate pointer or address width. Effective-address formation, valid ranges, translation, and faults are separate rules.

## Open areas
Register count and group topology; instruction encoding; endianness; condition state; address width; privilege transitions; context preservation; memory ordering.
