# 05 — Memory and address model

Register width, group width, pointer width, virtual address width, physical address width, and transfer width are independent.

Specify supported loads/stores, alignment, byte order, extension, effective-address formation, valid virtual ranges, page tables, permissions, translation invalidation, fault reporting, atomicity, and memory ordering.

A theoretical 2^512-byte address space is not an implementation target. Real capacity depends on implemented address bits, memory devices, buses, controllers, translation structures, and platform constraints.

The first profile must select practical address widths independently of 512-bit scalar registers.
