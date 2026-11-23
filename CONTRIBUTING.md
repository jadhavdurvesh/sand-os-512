# Contributing to SAND-512

Work specification-first. Read the relevant docs, check the decision register, record alternatives, update the specification, then add tests and implementation.

Do not copy another ISA's encodings, ABI, or exception rules and merely rename them. Existing designs may be studied and cited. Keep this repository independent from other SAND architecture repositories.

The emulator must be deterministic and independent of host overflow or undefined behaviour. Include boundary, malformed-input, and negative tests. Mark work accurately as proposed, accepted, implemented, or verified.

Coined names are provisional until checked for collisions. Technical precision takes priority over decorative terminology.
