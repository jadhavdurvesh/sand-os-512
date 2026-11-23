# 07 — Emulator design

**Reference emulator:** Threadglass (provisional).

Threadglass is intended as a deterministic executable specification, not a speed-first simulator.

## Components
Image validation, instruction fetch/decode, 512-bit arithmetic helpers, architectural state, grouped-register view logic, memory, executor, exception engine, trace writer, and conformance harness.

## Wide values
A portable implementation may represent a 512-bit value as eight 64-bit limbs. Define limb ordering, carry and borrow propagation, signed interpretation, shifts, multiplication, division, and byte serialization explicitly. Never depend on host overflow.

## Group semantics
Test aliasing and partial writes exhaustively. A write through one view must have exactly the specified effect on every overlapping view.

## Tests
Zero and maximum values; signed boundaries; carry across all limbs; shifts at 0, 511, 512 and larger; division corner cases; group aliasing; memory faults; invalid encodings; deterministic replay.
