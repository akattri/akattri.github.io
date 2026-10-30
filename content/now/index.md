---
title: "Now"
description: "A living dispatch on current coursework, low-level engineering experiments, and foundational research exploration."
---

*A snapshot of current priorities, coursework, and systems investigations. (Inspired by Derek Sivers' [/now page movement](https://nownownow.com/about)).*

---

## What I Am Working On This Month

### 1. Low-Level Systems & POSIX Primitives
- **[Seashell](/projects/seashell/)**: Implementing robust foreground process group management and terminal access arbitration via `tcsetpgrp()`. Handling signals (`SIGINT`, `SIGTSTP`, `SIGCHLD`) cleanly without creating zombie processes or breaking interactive command loops.
- **[Thread-Safe Concurrent Queue](/projects/thread-safe-queue/)**: Running stress benchmarks under Clang's `ThreadSanitizer` (`-fsanitize=thread`) across varying producer-consumer thread counts to evaluate lock contention patterns and condition variable broadcast overhead under heavy saturation.

### 2. Product Architecture & Offline-First Engineering
- **[Cogleaf](/projects/cogleaf/)** ([Live Application ↗](https://cogleaf.vercel.app/)): Refining the offline-first sensory architecture for cognitive tasks. Tuning Web Audio procedural synthesis to minimize audio latency on mobile WebViews, and refining Butterfly Safari's distractor suppression algorithms.
- **[Veto](/projects/veto/)**: Testing multi-world content script isolation on modern Chromium builds to ensure zero keyboard event interference during accelerated video playback while enforcing strict embed origin policies.

---

## Active Coursework & Foundations

- **University of Helsinki — Java Programming I & II**:  
  Working through memory semantics, class hierarchies, reference types, and JUnit unit testing to build disciplined object-oriented modeling habits alongside my procedural C work.
- **Princeton University — Algorithms (Sedgewick & Wayne)**:  
  Focusing on algorithmic problem-solving: binary search tree invariants, red-black trees, union-find implementations, and asymptotic analysis of graph search traversals.
- **Computer Organization & Memory Hierarchy**:  
  Studying how cache lines, memory page tables, and TLB misses impact systems performance, following up on Harvard's CS50x.

---

## Intellectual & Research Exploration

- **Systems for Machine Learning**:  
  Investigating the memory bandwidth bottlenecks of local large language model inference. Studying how KV-cache growth in autoregressive decoders correlates with Linux VRAM telemetry and system paging behavior.
- **Kernel & User Space Boundaries**:  
  Reading about the mechanics of Linux context switching, system call overhead, and zero-copy I/O mechanisms (`splice`, `sendfile`, `io_uring`).
- **Research Preparation**:  
  Systematically documenting project benchmarks, testing suites, and reproducible build scripts to prepare for competitive undergraduate research opportunities (Mitacs Globalink Research Internship 2027) and open-source systems fellowships.

---

## Current Academic Standing

- **Degree**: B.Tech in Computer Science and Engineering (Specialization: AI &amp; ML)
- **Institution**: SRM Institute of Science and Technology (SRM IST), Kattankulathur
- **Timeline**: 2nd Year / 3rd Semester &middot; Class of 2029
- **Cumulative GPA**: 8.05 / 10.0
