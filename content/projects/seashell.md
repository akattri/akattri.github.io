---
title: "Seashell"
date: 2026-02-01
date_display: "2026"
description: "A Unix shell implemented from scratch in C to understand process lifecycles, POSIX system calls, and inter-process communication."
status: "in progress"
domain: "Systems Programming & Operating Systems"
technologies:
  - "C"
  - "POSIX System Calls"
  - "Process Management"
  - "Linux"
  - "Make"
github: "https://github.com/akattri"
demo: ""
featured: true
weight: 10
---

## Overview

**Seashell** is an in-progress Unix command-line interpreter written in pure C. The goal of the project is not to replace mature shells like Bash or Zsh, but to demystify how the operating system coordinates process execution, input/output streams, signal handling, and environment isolation.

By building a shell without external runtime abstractions, every command executed exercises core POSIX kernel interfaces.

---

## Why I Built It

After completing Harvard's CS50x and spending years using Linux as my primary operating system, I wanted to transition from using CLI tools to understanding the kernel mechanisms that power them. 

A shell is one of the most pedagogical systems programming projects because it directly confronts the fundamental building blocks of Unix:
- How does an operating system create a new execution context?
- How are file descriptors redirected before a binary begins execution?
- How do pipelines (`|`) connect distinct processes without intermediate disk writes?
- How does a shell maintain control of the terminal when child processes are interrupted or suspended?

Building Seashell in C forces me to deal directly with manual memory allocation, pointer manipulation, system call return codes, and POSIX signal semantics.

---

## What I Learned & Engineering Takeaways

- **Process Lifecycle Mechanics**: Spawning child processes using `fork()` creates a duplicate address space (leveraging copy-on-write at the OS level), followed by `execvp()` replacing the memory image with the target binary.
- **Zombie and Orphan Prevention**: Managing process cleanup with `waitpid()` and understanding how parent processes must reap deceased children to prevent kernel process table exhaustion.
- **File Descriptor Manipulation**: Implementing I/O redirection (`<`, `>`, `>>`) by manipulating file descriptors using `open()`, `dup2()`, and `close()`.
- **Pipeline Synchronization**: Creating unidirectional data channels with `pipe()`, connecting the write-end of one child's `stdout` to the read-end of the next child's `stdin`, and closing unused pipe ends to ensure proper `EOF` propagation.
- **Signal Masking & Terminal Control**: Handling `SIGINT` (Ctrl+C) and `SIGTSTP` (Ctrl+Z) so that interrupts terminate or suspend child processes without killing the shell loop itself.

---

## Technical Architecture & Implementation

The shell operates through a standard **Read-Eval-Print Loop (REPL)**:

```
[User Input] ──> [Lexer / Tokenizer] ──> [Command AST / Struct]
                                                   │
                                                   ▼
                                         [Builtin Dispatcher]
                                           ├── Builtin (cd, exit, help)
                                           └── External Binary (fork/execvp)
                                                   │
                                                   ├── [I/O Redirection (dup2)]
                                                   └── [Pipeline Coordination (pipe)]
```

### Core Data Structures
```c
/* Representation of a parsed command invocation */
struct command_t {
    char **argv;          /* Array of argument strings */
    int argc;             /* Argument count */
    char *input_file;     /* Redirected stdin (<) */
    char *output_file;    /* Redirected stdout (>) */
    int append;           /* Append mode flag (>>) */
    struct command_t *next; /* Pointer to chained pipeline command */
};
```

### Implementation Milestones
- [x] Continuous prompt loop displaying current working directory
- [x] Dynamic string buffer reading line input of arbitrary length
- [x] Argument tokenization with whitespace delimiter handling
- [x] Process creation via `fork()` and binary execution via `execvp()`
- [x] Process synchronization via `waitpid()` with exit status reporting
- [x] Shell builtins (`cd`, `exit`, `pwd`, `help`) executed in the parent process
- [ ] Multi-stage pipeline coordination (`cmd1 | cmd2 | cmd3`)
- [ ] Background job control (`&`) and job table management

---

## Future Improvements & Open Questions

- **Job Control & Process Groups**: Implementing `tcsetpgrp()` to properly arbitrate foreground and background terminal ownership.
- **Path Resolution Optimization**: Exploring how command hash tables minimize repeated linear searches across `$PATH`.
- [Add technical details here]

