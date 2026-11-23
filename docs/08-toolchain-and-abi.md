# 08 — Toolchain and ABI

**Toolchain:** Rhuneforge (provisional).

Build sequence: freeze the initial ISA subset; implement assembler and disassembler; define a versioned object and executable format; add a linker/image builder; add compiler support after the ABI stabilises.

The ABI must define pointer width, argument and return locations, register preservation, stack alignment, aggregate layout, system-call entry, error representation, relocation types, and extension-state rules.

A 512-bit scalar may be passed in a scalar register, a register group, or memory. The ABI must choose explicitly and define alignment. 512-bit registers do not force 512-bit pointers.

Round-trip, relocation, malformed-image, and ABI conformance tests are required.
