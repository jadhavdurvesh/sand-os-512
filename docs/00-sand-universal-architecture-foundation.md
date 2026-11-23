# SAND Universal Architecture Foundation (SUAF)

**Document class:** Family-level architectural foundation  
**Applies to:** SAND-128, SAND-256, SAND-512, and SAND-1024  
**Status:** Foundational guidance; individual architecture specifications take precedence for machine behaviour

## 1. Purpose

SUAF defines the shared engineering principles and vocabulary used across the SAND Architecture Research Family. It provides a common way to describe, specify, implement, and verify computer architectures without requiring the family members to share one instruction set or processor design.

SUAF is not an ISA, ABI, hardware specification, or promise of binary compatibility. Each architecture must publish its own normative machine specification.

## 2. Family design principles

1. **Explicit machine contracts:** architecturally observable behaviour must be specified, not left to compiler or emulator assumptions.
2. **Independent architecture design:** each family member owns its register model, instruction encodings, execution semantics, memory rules, privilege model, and ABI.
3. **Width separation:** register width, arithmetic width, instruction width, pointer width, virtual-address width, physical-address width, and memory-transfer width are separate parameters.
4. **Deterministic reference model:** every architecture should have an executable reference model whose state transitions can be tested and traced.
5. **Specification before implementation:** unresolved design choices remain labelled open or proposed until formally decided.
6. **Measured claims:** distinguish mathematical limits, architectural limits, emulator behaviour, and measured hardware capabilities.
7. **Traceable decisions:** architectural decisions record context, alternatives, rationale, consequences, and verification requirements.
8. **Originality with technical clarity:** custom design must be demonstrated by actual semantics and specifications, not only by renamed terminology.

## 3. Architectural layers

Each architecture should document the following layers, even if some are intentionally small in its first version:

| Layer | Responsibility |
|---|---|
| Data and value model | Bit-vectors, integer interpretation, floating-point or packed formats |
| Register architecture | Visible state, register classes, special state, reset and preservation |
| Instruction-set architecture | Encodings, operands, instruction semantics and exceptions |
| Execution model | Fetch, decode, execution, retirement and observable ordering |
| Memory architecture | Loads, stores, alignment, ordering, translation and protection |
| Privilege and events | Privilege domains, traps, interrupts, reset and return behaviour |
| Platform and boot | Reset contract, memory map, loader handoff and device discovery |
| Software interface | ABI, executable format, system-call interface and runtime conventions |
| Verification | Conformance tests, reference emulator, traces and implementation evidence |

The layers are related, but their contracts must remain separately identifiable.

## 4. Width taxonomy

The phrase “N-bit architecture” is insufficient to describe a machine. Every SAND architecture must publish a width profile.

| Parameter | Meaning |
|---|---|
| Scalar register width | Number of bits in a specified general-purpose scalar register |
| Arithmetic width | Width at which an operation produces or consumes a value |
| Instruction encoding width | Bits used by an encoded instruction; may be fixed or variable |
| Pointer width | Width and representation of software pointers |
| Virtual-address width | Number of virtual address bits implemented by the architecture |
| Physical-address width | Number of physical address bits implemented by the platform |
| Memory-transfer width | Width of a defined load, store, or bus transfer |
| Vector or block width | Width of a packed, vector, or grouped data object |

These parameters may be equal, but equality must be a deliberate specification decision. A 1024-bit scalar register does not imply 1024-bit pointers, a 1024-bit physical address bus, or an installed memory capacity of 2^1024 bytes.

## 5. Numeric representation

A register is a bit-vector. Its interpretation depends on the instruction and data type.

Every architecture must define:
- Unsigned integer interpretation.
- Signed integer representation, if supported.
- Overflow, carry, and borrow behaviour.
- Shift-count and sign-extension rules.
- Division-by-zero and signed-division corner cases.
- Byte ordering for memory representation.
- Any fixed-point, floating-point, vector, or packed formats.

Binary is the underlying bit representation. Decimal, octal, and hexadecimal are not separate processor architectures; they are notational systems used to display values.

### Reference scalar ranges

The following are mathematical limits for an unsigned N-bit value, not claims about addressability or installed memory.

| Scalar width | Bit patterns | Maximum unsigned decimal digits | Hex digits |
|---:|---:|---:|---:|
| 128 | 2^128 | 39 | 32 |
| 256 | 2^256 | 78 | 64 |
| 512 | 2^512 | 155 | 128 |
| 1024 | 2^1024 | 309 | 256 |

For unsigned interpretation, the range is 0 through 2^N−1. For N-bit two's-complement signed interpretation, the range is −2^(N−1) through 2^(N−1)−1.

## 6. Memory and address terminology

SAND documents must distinguish:

- **Virtual address space:** addresses generated by software and translated under an address-space context.
- **Physical address space:** locations the platform's physical memory system can identify.
- **Installed memory:** actual RAM devices present in a particular machine.
- **Storage capacity:** persistent storage available to the system.
- **Memory bandwidth:** rate at which data can be transferred.
- **Cache capacity:** storage available in a particular cache level.

A theoretical N-bit byte address space contains 2^N byte locations only if all N bits are implemented as byte-address bits. This mathematical statement does not establish that such a platform can be built, populated with RAM, or used efficiently.

Each architecture must specify address formation, valid ranges, translation, page sizes, permissions, alignment, faults, and memory ordering independently of scalar register width.

## 7. Instruction and execution contracts

Each instruction definition should specify:
1. Encoding and decode rules.
2. Operand types and constraints.
3. Exact result and state transition.
4. Reads and writes to architectural state.
5. Overflow, status, and flag effects.
6. Memory effects and ordering.
7. Privilege requirements.
8. Fault conditions and exception priority.
9. Examples and boundary tests.

The reference execution model should define deterministic instruction boundaries and precise exception behaviour. If an instruction faults, the architecture must state which effects have or have not committed.

## 8. Privilege, protection, and events

Every architecture intended to host an operating system must specify its privilege domains and protected transitions.

At minimum, document:
- Reset state and reset entry.
- Privileged and unprivileged operations.
- Kernel entry and return.
- Memory access permissions.
- Synchronous exceptions and asynchronous interrupts.
- Saved architectural state and event-return rules.
- Address-space isolation requirements.

A privilege design alone does not prove a kernel secure. Security claims require implementation and testing of the full machine, boot path, toolchain, and operating system.

## 9. Software contracts

The ABI is a separate specification from the ISA. It defines how compiled programs and the operating system exchange values and control.

Each architecture must define pointer representation, argument and return conventions, register preservation, stack layout and alignment, aggregate layout, executable format, relocations, system-call entry, and error reporting.

No SAND architecture inherits another member's ABI by default.

## 10. Reference implementation and verification

The recommended implementation order is:

1. Write a precise base architecture specification.
2. Create a machine-readable description where practical.
3. Implement a deterministic reference emulator.
4. Add arithmetic, decoder, memory, exception, and privilege tests.
5. Implement assembler and disassembler.
6. Define executable and object formats.
7. Build a minimal virtual platform.
8. Boot a small experimental kernel.
9. Measure performance and resource costs only after a working implementation exists.

Test suites must include normal cases, boundary values, malformed inputs, invalid encodings, permission faults, and deterministic replay. Host-language overflow or undefined behaviour must never silently define guest architecture semantics.

## 11. Specification status vocabulary

Use these labels consistently:

- **Open:** no decision has been selected.
- **Proposed:** a candidate design exists but is not accepted.
- **Accepted:** selected for the current specification revision.
- **Implemented:** code exists for the feature.
- **Verified:** tests demonstrate conformance to the documented behaviour.
- **Deferred:** intentionally postponed.
- **Superseded:** replaced by a later decision.

A feature must not be described as implemented or verified merely because it appears in a roadmap or document.

## 12. Family independence and compatibility

The SAND family shares this foundation, engineering practices, and research discipline. It does not require shared instruction encodings, register names, pointer widths, page tables, executable formats, ABIs, or binary compatibility.

A common tool may support multiple architectures only when each architecture's semantics remain explicit and independently testable.

## 13. Per-architecture obligations

Each family repository must maintain:
- A versioned architecture overview.
- A width profile.
- A register and data model.
- A complete base ISA specification before claiming implementation.
- Memory, privilege, event, boot, and ABI specifications.
- A decision register.
- A reference emulator and conformance tests before claiming a verified implementation.

## 14. Change control

SUAF changes should be reviewed as family-level changes. A change to this document does not silently change an architecture's normative specification. Each repository must explicitly adopt relevant revisions and record any local deviations.

Architecture-specific specifications always define the actual machine behaviour. Where a family principle conflicts with a deliberate architecture-specific design, the repository must document the exception and its rationale.
