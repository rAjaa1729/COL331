# Lab 03 — xv6 Memory Management

An assignment on xv6's physical memory management (from
`docs/assignment-brief.pdf`).

## What's here

The actual modified xv6 source was lost — see
[lab-01](../lab-01-xv6-syscalls)'s README for how. One real file survived:

- `memtest.c` — a user-space test program: allocates pages (via `malloc`)
  until a target byte count is reached, linking each page to the next,
  then walks the list back to verify every page's tag matches, printing
  `Memtest Passed`/`Memtest Failed`. Uses only standard xv6 library calls
  (no custom syscalls), so it builds against the plain base as-is —
  whether it actually *passes* depends on the kernel-side memory-management
  change this assignment required, which wasn't recovered.
- `xv6/` — the plain, unmodified xv6 base this assignment started from.
- `docs/assignment-brief.pdf` — the original spec.

A third-party study-notes repo on xv6 memory internals was also in the
original repository (not this project's own work) — removed rather than
hosted here; worth re-linking if you recall the source.

## Build/run

```bash
cp memtest.c xv6/memtest.c
# add "_memtest\" to UPROGS in xv6/Makefile
cd xv6
make          # needs an i386 cross-toolchain (see xv6/Makefile)
make qemu     # boots it in QEMU; run `memtest` at the shell
```
