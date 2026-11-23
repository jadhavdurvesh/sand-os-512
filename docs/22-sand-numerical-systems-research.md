# SAND Numerical Systems Research (SNSR)

**Family research specification — shared foundation, independently adopted by each architecture.**

Status: Research framework. This document does not declare every format or operation implemented, mandatory, or part of any frozen ISA.

## 1. Purpose

SAND Numerical Systems Research (SNSR) studies how SAND machines represent, convert, compare, store, and calculate with numbers. The goal is to investigate more than the conventional binary integer and binary floating-point model while preserving clear, testable machine semantics.

SNSR is a research layer shared by SAND-128 (Veylith), SAND-256 (Caelvyr), SAND-512 (Thryvane), and SAND-1024 (Orryxen). Each architecture may adopt different formats, widths, instructions, and implementation strategies. A shared research vocabulary does not create binary or ABI compatibility.

## 2. A necessary distinction: bases, encodings, and arithmetic formats

These categories are related but not interchangeable.

- **Radix / base** defines positional place values. Examples include binary (base 2), ternary (base 3), decimal (base 10), hexadecimal (base 16), and sexagesimal (base 60).
- **Digit encoding** defines how symbols or digits are stored as bits. Examples include packed BCD and other binary encodings of decimal digits.
- **Signed-number representation** defines how negative values are represented. Examples include two's complement, sign-magnitude, ones' complement, and balanced ternary.
- **Floating-point or real-number format** defines sign, scale/exponent, precision, rounding, and exceptional values. IEEE-style binary floating point, decimal floating point, and posit-like proposals belong here.
- **Arithmetic system** defines how operations are performed. Examples include fixed-width modular arithmetic, arbitrary precision, multi-precision arithmetic, and residue number systems.
- **Display notation** defines how values are written for people. It need not match the machine's internal representation.

A format must be classified accurately. For example, Gray code is a bit encoding with adjacent-code properties, not a positional base. Roman numerals are non-positional notation, not a conventional radix representation. BCD encodes decimal digits in binary; it is not itself a base-10 physical processor.

## 3. Positional radix systems

For a positional radix b, a value is represented as:

N = sum(d[i] * b^i)

where each digit d[i] is in the permitted digit set for that radix. For ordinary unsigned positional notation, digits range from 0 through b-1.

Research radices may include:

| Radix | Name | Example digit alphabet / notes |
|---:|---|---|
| 2 | Binary | 0–1 |
| 3 | Ternary | 0–2 |
| 4 | Quaternary | 0–3 |
| 5 | Quinary | 0–4 |
| 8 | Octal | 0–7 |
| 10 | Decimal | 0–9 |
| 12 | Duodecimal | 0–9 plus two additional digit symbols |
| 16 | Hexadecimal | 0–9, A–F |
| 20 | Vigesimal | 20 distinct digit values |
| 32 | Base-32 | Alphabet depends on the chosen standard |
| 36 | Base-36 | Commonly 0–9 and A–Z |
| 60 | Sexagesimal | 60 digit values; a notation convention must define their symbols |
| 62 | Base-62 | Alphabet and case-sensitivity must be specified |

The table is a research catalogue, not a list of supported SAND hardware modes. A radix may be used for human-readable input/output, a software library, a data format, or native arithmetic. Those are separate levels of support.

## 4. Sexagesimal (base-60) research profile

Sexagesimal is explicitly included in SNSR.

### 4.1 Why investigate base-60?

Base-60 has a rich history and remains familiar in time and angular measurement:

- One hour is 60 minutes; one minute is 60 seconds.
- A full circle is conventionally divided into 360 degrees, with angular subdivisions using minutes and seconds.
- 60 has many integer divisors, making fractions such as 1/2, 1/3, 1/4, 1/5, 1/6, 1/10, 1/12, 1/15, and 1/20 terminate after one sexagesimal place.

This makes base-60 interesting for clocks, angles, navigation, astronomy, geometry, and fractional quantities. It does not make every fraction finite, nor does it prove that base-60 hardware is faster or more efficient.

### 4.2 Place values and notation

Sexagesimal positional places represent powers of 60. To avoid confusion with decimal punctuation, the SAND research notation will use colon-separated integer groups and a semicolon to introduce fractional groups:

- `1:00` means 1×60 + 0 = 60 (decimal).
- `2:30` means 2×60 + 30 = 150 (decimal).
- `1;30` means 1 + 30/60 = 1.5 (decimal).
- `0;30` means 30/60 = 0.5 (decimal).
- `1:02:03` means 1×60² + 2×60 + 3 = 3723 (decimal).

These are SNSR explanatory conventions, not yet an assembler syntax or a frozen wire format. Every digit group must be in the range 0–59. A parser must reject invalid groups rather than silently normalize them unless a separate normalization operation is explicitly requested.

A production format must specify sign handling, leading-zero rules, fractional precision, rounding, separators/escaping, and how values are distinguished from clock or angle notation.

### 4.3 Conversion and arithmetic

Initial software research should provide:

1. Decimal integer to sexagesimal conversion.
2. Sexagesimal integer to decimal conversion.
3. Fractional sexagesimal parsing and formatting with explicit precision.
4. Addition, subtraction, multiplication, and division with documented carry/borrow behaviour.
5. Comparison and normalization.
6. Checked overflow and divide-by-zero handling.
7. Round-trip tests and boundary tests around 0, 59, 60, 359, 360, and powers of 60.

For integer conversion, repeated division by 60 produces the sexagesimal digits. Reconstruction uses positional powers of 60. Fractional conversion repeatedly multiplies the fractional remainder by 60; the implementation must stop at a specified precision and apply a specified rounding rule.

The first reference implementation should use a wider exact integer or rational representation where practical. It must not use binary floating point as an invisible substitute for exact sexagesimal fractions.

### 4.4 Time and angle are domain types, not merely radix choices

A clock value such as 02:30:00 and an angle such as 02°30′00″ use related subdivision conventions, but they are not interchangeable quantities. Time-of-day, elapsed duration, angular measure, and generic base-60 numbers should have distinct software types or metadata.

The architecture and runtime must not infer units solely from colon separators. Calendar rules, time zones, leap seconds, and angle normalization belong to higher-level specifications and libraries, not to a bare radix conversion routine.

### 4.5 Hardware questions

SNSR will compare three implementation levels:

- **Level A — software format:** values are stored in ordinary binary registers and converted by libraries.
- **Level B — optional instruction extension:** dedicated conversion or packed-digit operations are considered only if workload measurements justify them.
- **Level C — native arithmetic model:** a processor exposes base-60 arithmetic semantics directly. This is the most disruptive option and requires strong evidence, precise exception rules, and a compelling workload.

No SAND architecture currently commits to Level B or C merely by including sexagesimal in this research programme. A binary machine can support sexagesimal values very well through software.

## 5. Other numerical systems to investigate

### 5.1 Balanced ternary

Digits have values -1, 0, and +1. Research its signed representation properties, negation, carry propagation, conversion cost, and possible hardware complexity. A textual alphabet must be selected before defining a concrete encoding.

### 5.2 Negative-base systems

Negative radix systems (for example, base -2) can represent positive and negative integers without a separate sign symbol in the positional representation. Study conversion complexity, arithmetic rules, and practical software use before considering ISA support.

### 5.3 Decimal and BCD

Investigate packed and unpacked BCD, decimal integer arithmetic, decimal rounding, and decimal floating-point requirements. Specify invalid digit handling and decimal exception behaviour. Distinguish decimal data formats from the binary encoding used to store them.

### 5.4 Signed binary representations

Compare two's complement, sign-magnitude, and ones' complement, including zero representations, overflow, comparisons, shifts, and compatibility costs. Two's complement remains a baseline for conventional binary integer operations unless an architecture decision says otherwise.

### 5.5 Gray code and other bit encodings

Study Gray code for counters, encoders, and transitions where adjacent values differ by one bit. It should not be described as a radix arithmetic system. Conversion and arithmetic normally occur through a decoded numeric value.

### 5.6 Fixed-point, floating-point, and posit-like formats

Compare precision, dynamic range, rounding modes, subnormal/exceptional values, determinism, and implementation cost. Any proposal must define exact bit fields and observable arithmetic behaviour before claiming conformance.

### 5.7 Residue number systems (RNS)

Represent values using residues modulo a set of pairwise-coprime moduli. Research parallel arithmetic, range limits, signed interpretation, comparison, division, conversion overhead, and error detection. RNS is an arithmetic representation, not simply another positional radix.

### 5.8 Arbitrary-precision and multi-precision arithmetic

Study limb size, carry chains, allocation, constant-time behaviour, compiler lowering, and the cost of operating on values larger than a machine register. This is especially relevant to wide-register architectures but should not be conflated with native register width.

## 6. Shared SAND implementation model

Each architecture should document numerical support at four levels:

1. **Representation:** how a value is encoded in memory and registers.
2. **Language/runtime:** how source code, libraries, and APIs expose it.
3. **Instruction support:** which operations, if any, are directly specified by the ISA.
4. **Verification:** how exact results, rounding, overflow, and exceptional cases are tested.

A format may be supported at one level without support at the others. For example, a sexagesimal library can run on a binary-only ISA.

Every adopted format must specify:
- value domain and permitted range;
- bit-level or textual encoding;
- endianness where relevant;
- signedness and zero behaviour;
- precision and rounding;
- overflow, underflow, and invalid-input behaviour;
- arithmetic and comparison semantics;
- conversion rules;
- ABI and calling-convention impact, if any;
- deterministic test vectors.

## 7. Architecture-specific research emphasis

These are investigation priorities, not frozen architectural decisions.

| Architecture | Research emphasis |
|---|---|
| SAND-128 / Veylith | Balanced ternary, signed representations, exact radix conversion, and a practical software sexagesimal library using the implemented 128-bit machine as a test platform. |
| SAND-256 / Caelvyr | Packed decimal, wide integer arithmetic, paired-field operations, and experiments comparing full-scalar versus subfield conversion and arithmetic. |
| SAND-512 / Thryvane | Grouped numeric representations, multi-precision limbs, explicit partial-write semantics, and grouped operations on decimal or sexagesimal data. |
| SAND-1024 / Orryxen | Block arithmetic, residue number systems, extreme-precision workloads, and the cost of moving, saving, and operating on very wide numeric state. |

Sexagesimal should be implemented first as a portable reference library and conformance test suite. Results can then be compared across all four emulators or future implementations. Dedicated instructions should be proposed only after benchmarks show a meaningful benefit over software.

## 8. Conformance test plan

The shared test corpus should include:

- radix conversion round trips for every supported radix;
- sexagesimal examples: `0`, `59`, `1:00`, `2:30`, `1:02:03`, `0;30`, and `1;30`;
- invalid sexagesimal groups such as `1:60` and `60:00`;
- carry and borrow across a base-60 boundary;
- exact fractions and repeating fractions;
- explicit rounding-mode tests;
- overflow, underflow, divide-by-zero, and invalid-input tests;
- cross-implementation tests to ensure identical results;
- serialization tests to ensure a value's unit and format are not confused.

A test passing in a host-language library does not by itself prove ISA or emulator support. Test reports must state which layer was tested.

## 9. Research status vocabulary

Use these labels consistently:

- **Proposed:** an idea under discussion.
- **Specified:** behaviour is written precisely enough to implement.
- **Implemented:** code exists.
- **Tested:** named tests have run.
- **Verified:** evidence supports the stated conformance claim.
- **Deferred:** intentionally postponed.
- **Rejected:** considered and not adopted, with rationale recorded.

Do not label a radix or format “supported” without stating the support layer and implementation status.

## 10. Decision policy

Before adding any numerical format to an ISA, create a decision record containing:

1. Target workloads and motivating problem.
2. Candidate formats and alternatives.
3. Exact semantics and encodings.
4. Software-only baseline.
5. Hardware area, latency, power, and complexity estimates where available.
6. Compiler, ABI, and operating-system impact.
7. Conformance tests and measurable acceptance criteria.
8. Compatibility and migration implications.

## 11. Non-goals and cautions

- SNSR does not require every SAND architecture to implement every radix.
- A larger register does not automatically make a numerical format more accurate.
- Base-60 support does not require a base-60 processor.
- Do not conflate sexagesimal time/angle notation with generic integer arithmetic.
- Do not claim speed, precision, or efficiency improvements without reproducible measurements.
- Do not imply that the architecture's pointer width, address width, or physical memory capacity follows from its scalar register width.

## 12. Next milestone

The first practical milestone is a language-neutral sexagesimal specification and a small reference implementation with deterministic test vectors. Once that is stable, each architecture can evaluate how the library maps to its own register model, ABI, emulator, and toolchain.
