# 12 — ABI specification

**Status:** Not yet specified.

The ABI is independent of the register-width headline. It must define pointer representation, argument and return locations, register preservation, stack layout and alignment, aggregate layout, system-call entry, error reporting, relocation types, symbol conventions, and extension-state handling.

A 512-bit value may be passed in one scalar register, a group, or memory. Specify the choice and alignment. Do not assume pointer width equals scalar width.

ABI compatibility requires stable documented rules and conformance tests.
