# 09 — Kernel and boot architecture

**Kernel environment:** Duskloom (provisional).

The first target is a virtual platform in the emulator. Specify reset state, memory map, reserved regions, image format, entry privilege, loader responsibilities, handoff data, and device discovery before implementing boot.

Initial kernel responsibilities:
- Boot handoff and processor initialisation.
- Exception and interrupt handling.
- Memory inventory and allocation.
- Virtual-memory setup.
- Basic task isolation.
- Minimal system-call interface.
- Emulator console output.

Wide register groups can increase context-save cost. The kernel must know which state is live, mandatory to preserve, or safely deferred. A minimal protected kernel is the first proof; GUI, networking, SMP, and broad device support are later.
