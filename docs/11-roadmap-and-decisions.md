# 11 — Roadmap and decision register

## Roadmap
A. Charter and terminology.  
B. Freeze register/group semantics, instruction encoding, arithmetic, address model, reset, privilege, and traps.  
C. Build deterministic Threadglass emulator.  
D. Add assembler, disassembler, executable format, and linker.  
E. Boot a minimal Duskloom kernel.  
F. Measure context-save size, arithmetic cost, code density, and memory transfer behaviour.

## Open decisions
- Register count and group topology.
- Whether group views alias or represent independent state.
- Partial-write and atomicity rules.
- Instruction encoding and immediate formats.
- Pointer, virtual-address, and physical-address widths.
- Endianness, alignment, and memory ordering.
- Privilege levels, interrupts, and ABI.

## Decision policy
Each accepted decision needs context, alternatives, rationale, consequences, affected specifications, and conformance tests. Features move from proposed to accepted, implemented, and verified only with evidence.
