# SAND-512 — Thryvane

**Experimental 512-bit computing architecture research.**

SAND-512 is an independent clean-sheet architecture in the SAND Architecture Research Family. It shares family-wide engineering principles but defines its own register organisation, ISA, execution model, memory contract, toolchain, and ABI.

> **Status:** Design research only. No working processor, emulator, kernel, full-width address space, or performance advantage is claimed.

## Research direction

Investigate a grouped wide-state design: a 512-bit scalar may be composed, split, and transferred through explicitly specified register groups. The architecture must define group aliasing, partial writes, alignment, and context-save semantics before implementation.

## Provisional terminology

| Concept | Term |
|---|---|
| Architecture | Thryvane |
| 512-bit scalar register | Syr |
| Register organisation | Syrrack |
| Decoded instruction | Vael |
| Instruction sequence | Vaelchain |
| Kernel environment | Duskloom |
| Reference emulator | Threadglass |
| Toolchain | Rhuneforge |

Names are provisional and not claims of trademark uniqueness.

## Width discipline

512-bit scalar registers do not imply 512-bit pointers, virtual addresses, physical addresses, or installed RAM. These are separate design parameters.

## Documentation

The [docs](docs/) directory defines scope, architecture, register and numeric model, ISA, memory, execution, protection, emulator, toolchain, ABI, kernel, memory capabilities, verification, roadmap, and decisions.

## Planned structure

```text
specifications/  Machine-readable ISA definitions
emulator/        Threadglass reference emulator
assembler/       Assembler and disassembler
toolchain/       Linker, image builder, compiler experiments
boot/            Virtual platform boot contract
kernel/          Duskloom experimental kernel
tests/           Conformance tests
```

Directories will be created when implementation begins, not as empty placeholders.

## Current status

| Area | Status |
|---|---|
| Charter / terminology | Drafted / proposed |
| Register / numeric model | Proposed |
| ISA / encoding | Open |
| Address / memory model | Open |
| Emulator / toolchain / kernel | Not implemented |
| Hardware | Not implemented |

## License

No license has been selected. All rights are reserved unless and until a license is added.
