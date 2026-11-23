# 03 — Register and numeric model

**Register:** Syr · **Register organisation:** Syrrack (provisional).

A 512-bit scalar contains 64 octets and has 2^512 bit patterns.
- Unsigned range: 0 to 2^512−1.
- Signed two's-complement range: −2^511 to 2^511−1.
- Up to 155 decimal digits or 128 hexadecimal digits.

## Grouping model
Investigate whether the architectural register is monolithic or composed of smaller named fields. If groups are visible, specify group count, widths, ordering, overlap, aliasing, partial writes, atomicity, and read-after-write behaviour.

## Arithmetic
Define wrap/trap/saturate behaviour, carry/borrow, signed and unsigned comparisons, division-by-zero, signed division edge cases, shifts, and aliasing.

## State preservation
A 512-bit register bank can make context save/restore expensive. Quantify state size only after register count and extension state are chosen. Specify which state is mandatory to preserve.

Binary is the underlying representation. Decimal, octal, and hexadecimal are not separate machine architectures.
