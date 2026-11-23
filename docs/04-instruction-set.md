# 04 — Instruction-set architecture

Decoded operations are provisionally **Vael**; instruction sequences are **Vaelchain**.

Candidate families: data movement, group composition/decomposition, 512-bit arithmetic, comparisons, loads/stores, control transfer, system entry, privileged control, and optional atomic operations.

Fixed, variable, and hybrid instruction encodings remain open. Evaluate decode complexity, code density, immediate range, extension space, alignment, and compiler cost. No opcode values are stable.

Every instruction must specify encoding, operands, exact result, state effects, partial-write behaviour, exceptions, privilege, examples, and boundary tests. Group operations must not rely on undocumented register aliasing.
