# Lab 02 — xv6 Signal Handling & Scheduling

A team assignment (from `docs/assignment-brief.pdf`) with two parts:

1. **Signal handling** — keyboard-interrupt signals (`SIGINT`/Ctrl+C,
   `SIGBG`/Ctrl+B, `SIGFG`/Ctrl+F, `SIGCUSTOM`/Ctrl+G) for killing,
   backgrounding, foregrounding, and custom-handling processes, plus a
   `signal(sighandler_t)` syscall to register a user-space handler.
2. **Scheduling** — replacing xv6's round-robin scheduler with a
   priority-based one, plus profiling.

## What's here

The actual modified xv6 source was lost — see
[lab-01](../lab-01-xv6-syscalls)'s README for how. Nothing survived for
this assignment beyond the brief itself: no screenshots, no leftover
source files.

- `xv6/` — the plain, unmodified xv6 base this assignment started from.
- `docs/assignment-brief.pdf` — the original spec.

## Build/run the base

```bash
cd xv6
make          # needs an i386 cross-toolchain (see xv6/Makefile)
make qemu     # boots it in QEMU
```
