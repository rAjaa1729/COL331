# Lab 01 — xv6 System Calls

An assignment to add new system calls to the [xv6](https://pdos.csail.mit.edu/6.828/2020/xv6.html)
teaching operating system: process-history tracking, a login/authentication
gate, per-syscall blocking (`block`/`unblock`), and a `chmod` syscall for
setting file permission bits.

## What's here

The actual modified xv6 source was lost — `git add` was originally run on
a cloned repo folder, which git silently recorded as an empty submodule
reference instead of adding its files. Only four screenshots of the real
code survived (`docs/screenshots/`).

- `xv6/` — the plain, unmodified xv6 base this assignment started from
  (recovered from a zip that was sitting alongside the broken reference).
  Builds and boots as-is; it just doesn't contain this assignment's changes.
- `docs/assignment-brief.pdf` — the original assignment spec.
- `docs/screenshots/` — the four surviving screenshots of the real
  implementation.
- `docs/recovered-code-excerpts.md` — the code from those screenshots,
  transcribed as-is (not modified, not wired into `xv6/`).

## Build/run the base

```bash
cd xv6
make          # needs an i386 cross-toolchain (see xv6/Makefile)
make qemu     # boots it in QEMU
```
