# Recovered code excerpts

The actual xv6 source for this assignment is gone (see the main README) —
all that survives is four screenshots (`docs/screenshots/`) of code you
wrote: two new system calls (`chmod`, syscall `block`/`unblock`) and two
more features (process-history tracking, login auth). All four are kept
here exactly as transcribed from the screenshots, not modified or wired
into `xv6/` — doing that would mean writing new surrounding code (struct
definitions, syscall numbers, call sites) that was never photographed and
isn't yours to attribute. `xv6/` next to this file is the plain vanilla
base your assignment started from, kept so the excerpts below have context.

## chmod

```c
int sys_chmod(void)
{
  char *path;
  int mode;

  if(argstr(0, &path) < 0 || argint(1, &mode) < 0)
    return -1;

  struct inode *ip;
  begin_op();
  if((ip = namei(path)) == 0){
    end_op();
    return -1;
  }
  ilock(ip);

  ip->mode = (mode & 0x7) | 0x8;

  iupdate(ip);
  iunlock(ip);
  end_op();

  return 0;
}
```

(`ip->mode` implies a `mode` field was also added to xv6's inode structs —
not itself visible in the screenshot.)

## Syscall block / unblock

```c
int sys_block(void){
  int syscall_num;
  struct proc *p = myproc();

  if(argint(0, &syscall_num) < 0)
    return -1;

  if(syscall_num == 1 || syscall_num==2){
    cprintf("fork or exit cannot be blocked \n");
    return -1;
  }

  cprintf("syscall %d is blocked\n", syscall_num);
  p->parent->blocked_syscalls[syscall_num] = 1;
  return 0;
}

int sys_unblock(void ){
  int syscall_num;
  struct proc *p = myproc();

  if(argint(0, &syscall_num) < 0)
    return -1;

  p->parent->blocked_syscalls[syscall_num] = 0;
  return 0;
}
```

(References `p->parent->blocked_syscalls[...]` — a field that isn't part
of vanilla xv6's `struct proc`, so it must also have been added.)

## Process history tracking

From `docs/screenshots/history-syscall.png`:

```c
struct history process_history;

void add_history(struct proc *p){
  struct history_entry entry;
  if(process_history.count>=MAXHISTORY){
    cprintf("History is full\n");
    return;
  }
  safestrcpy(entry.name, p->name, sizeof(p->name));
  entry.pid = p->pid;
  entry.mem = p->sz;
  process_history.history[process_history.count++] = entry;
}

int get_history(){
  int i;
  for(i=0;i<process_history.count;i++){
    cprintf("%d %s %d\n", process_history.history[i].pid,
      process_history.history[i].name,
      process_history.history[i].mem);
  }
}
```

**Missing to make this build:** the `struct history_entry` / `struct
history` definitions (field types can be inferred from usage — `name` is
probably `char[16]` to match `p->name`, `pid` an `int`, `mem` a `uint` to
match `p->sz` — but `MAXHISTORY` has no known value), where `add_history()`
is actually called from (most likely `fork()` in `proc.c`, but not
confirmed), and how `get_history()` is exposed as a syscall (a `sys_`
wrapper plus the usual syscall-number/`user.h`/`usys.S` registration).

## Login authentication

From `docs/screenshots/login-auth-syscall.png`:

```c
int Authenticate_User(){
  char username[MAXLENGTH], password[MAXLENGTH];
  int attempts = 0;
  while(attempts < MAXATTEMPTS){
    printf(1,"Enter Username: ");
    gets(username, MAXLENGTH);
    trim_endline(username);

    if(strcmp(username, USERNAME) != 0){
      printf(1, "Invalid Username! Try again.\n");
      attempts++;
      continue;
    }
    else{
      printf(1, "Enter Password: ");
      gets(password, MAXLENGTH);
      trim_endline(password);
      if(strcmp(password, PASSWORD) != 0){
        // screenshot is cropped here
```

This reads as a **user-space** program (uses `gets`/`printf`/`strcmp`, all
existing xv6 library calls), not a kernel syscall — likely a custom login
gate run in place of/before the shell. **Missing:** the rest of the
function (screenshot is cropped mid-`if`), the `MAXLENGTH`/`MAXATTEMPTS`
constants, `trim_endline()`'s definition, and the actual `USERNAME`/
`PASSWORD` values — the last of which can't be recovered or guessed at
all, since inventing credentials would misrepresent what you actually set.
