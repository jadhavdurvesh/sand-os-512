# 01 — Vision and scope

**Codename:** Thryvane · **Scalar target:** 512 bits · **Status:** Research proposal

SAND-512 investigates grouped wide-state computing. Its first research question is how a 512-bit scalar can be represented, composed, split, transferred, and preserved efficiently without ambiguous register aliasing.

## Goals
- Define an original ISA and machine contract.
- Specify register, arithmetic, pointer, virtual-address, physical-address, and instruction widths separately.
- Define group and partial-write semantics.
- Make observable behaviour deterministic and testable.
- Build an emulator before considering hardware.

## Non-goals
No commercial processor, compatibility promise, performance claim, or assumption that 512-bit registers require 512-bit addressing.

| Property | Initial direction |
|---|---|
| General scalar register | 512 bits, proposed |
| Native integer arithmetic | At least 512 bits, proposed |
| Pointer width | Open |
| Virtual / physical address widths | Open |
| Instruction encoding | Open |

Success means a reviewed specification and conformance-tested emulator, not a boot screen.
