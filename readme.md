# COL331 — Operating Systems Labs

Three assignments from an undergraduate Operating Systems course
(IIT Delhi, COL331), all built on the [xv6](https://pdos.csail.mit.edu/6.828/2020/xv6.html)
teaching operating system.

| Lab | Topic |
|---|---|
| [lab-01-xv6-syscalls](lab-01-xv6-syscalls) | New system calls: process history, login auth, syscall block/unblock, chmod |
| [lab-02-xv6-signals-scheduling](lab-02-xv6-signals-scheduling) | Keyboard-interrupt signal handling + priority-based scheduling |
| [lab-03-xv6-memory-management](lab-03-xv6-memory-management) | Physical memory management |

## A note on what's recoverable

The actual modified xv6 source for all three assignments is **not**
present in this repository's history. Each assignment folder originally
had its own clone of the xv6 base as a nested directory; committing it
with plain `git add` (with no `.gitmodules` entry) made git record it as
an empty submodule reference instead of adding its files — so every clone
of this repo, including the one these labs were rebuilt from, got empty
folders where the real kernel changes should be.

What survived and is preserved in each lab folder:
- The unmodified xv6 base each assignment started from (`xv6/` in each lab).
- Whatever original artifacts happened to survive outside the broken
  folders — for lab-01, four screenshots of real code; for lab-03, one
  real source file (`memtest.c`).
- Every assignment brief PDF.

`Slides/` also lost most of its content — the lecture decks were iCloud
placeholder files that were never actually synced before being committed;
only one real slide deck survived.
