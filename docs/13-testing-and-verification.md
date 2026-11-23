# 13 — Testing and verification

## Verification levels
Arithmetic helpers; register and group-view state; decoder; instruction semantics; memory translation and permissions; traps and privilege; assembler/disassembler round trips; ABI programs; kernel boot; deterministic replay.

## Wide-state cases
Test carry and borrow across all eight 64-bit limbs, signed boundaries, maximum values, shifts around 512 bits, division corner cases, group aliasing, partial writes, and serialization.

## Status labels
Proposed, accepted, implemented, verified, deferred. A feature is verified only when tests demonstrate the specified behaviour.
