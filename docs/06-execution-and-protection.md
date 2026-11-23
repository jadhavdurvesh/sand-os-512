# 06 — Execution and protection

Define fetch, decode, validation, execution, retirement, and precise exception behaviour. Reset must initialise all architectural state deterministically.

At minimum, the OS experiment needs unprivileged application and privileged kernel domains. Specify privileged instructions, control-register access, system entry, return validation, and memory permissions.

Distinguish synchronous exceptions from asynchronous interrupts. Define saved state, cause reporting, priority, masking, nesting, and return semantics.

The architecture must define how wide and grouped register state is preserved across traps and context switches. The emulator should support deterministic single-step traces and event injection.
