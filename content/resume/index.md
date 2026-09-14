---
title: "Curriculum Vitae"
description: "Academic background, coursework, systems engineering experience, and technical foundations."
---

<div style="display: flex; justify-content: space-between; align-items: baseline; margin-bottom: 2rem; border-bottom: 1px solid var(--border); padding-bottom: 1rem;">
  <div>
    <span style="font-family: var(--font-mono); font-size: 0.85rem; color: var(--text-faint);">ONLINE RESUME · ACADEMIC RECORD</span>
  </div>
  <div>
    <a href="#" onclick="window.print(); return false;" style="font-family: var(--font-mono); font-size: 0.85rem;">Print / Save as PDF ↗</a>
  </div>
</div>

## Education

**SRM Institute of Science and Technology**, Kattankulathur, Tamil Nadu, India  
*Bachelor of Technology in Computer Science and Engineering (AI &amp; ML)*  
**Timeline**: 2025 – 2029 (Current Standing: 2nd Year / 3rd Semester)  
**Cumulative GPA**: 8.05 / 10.0  

---

## Technical Foundations

- **Languages**: C, Python, Java, SQL, Bash / POSIX Shell, HTML/CSS
- **Operating Systems & Systems**: Linux (Debian, Fedora, Ubuntu), Unix system calls (`fork`, `exec`, `pipe`, `waitpid`, `signals`), POSIX threads (`pthreads`, mutexes, condition variables)
- **Computer Science Core**: Data structures (arrays, linked lists, hash tables, trees, heaps), algorithms (sorting, search, recursion, asymptotic complexity), memory management (pointers, dynamic allocation, Valgrind)
- **Tools & Environments**: GCC, Clang, Make, Git, GitHub, GDB, Neovim, Vim, Linux CLI diagnostics

---

## Coursework & Certifications

- **Harvard University — CS50x**: Introduction to Computer Science  
  *Completed 2026*. Rigorous grounding in C, manual memory allocation, pointers, algorithms, data structures, SQL, and Python.
- **Linux Essentials Certification**: Linux Foundation / NDG  
  *Completed*. Command line proficiency, file permissions, shell scripting, Linux architecture, open source licensing.
- **University of Helsinki — Java Programming I & II**:  
  *In Progress*. Object-oriented programming, design patterns, testing with JUnit, collections, exception handling.
- **Princeton University — Algorithms Part I & II** (Robert Sedgewick):  
  *Upcoming*. Advanced graph algorithms, balanced search trees, geometric search, minimum spanning trees, network flow.

---

## Selected Technical Projects

### Seashell — Unix Shell Implementation
*C, Linux System Calls, Process Management* · `In Progress / Experimental`
- Implemented a command-line shell from scratch in C to understand process creation and inter-process communication.
- Implemented command parsing, execution loop, child process spawning via `fork()` and `execvp()`, and process lifecycle reaping with `waitpid()`.
- Built I/O redirection (`<`, `>`) and inter-process pipelines using `pipe()` and `dup2()`.
- Implemented signal handling for `SIGINT` (Ctrl+C) and `SIGTSTP` (Ctrl+Z) to prevent shell termination.

### Thread-Safe Concurrent Queue
*C, POSIX Threads (pthreads), Concurrency* · `In Progress / Experimental`
- Developed a thread-safe First-In-First-Out (FIFO) queue in C supporting concurrent multi-producer, multi-consumer access.
- Synchronized enqueue and dequeue operations using POSIX mutual exclusion locks (`pthread_mutex_t`) and condition variables (`pthread_cond_t`).
- Protected against race conditions, deadlock conditions, and priority inversions.

### LLM Resource Monitor
*Python, Systems / ML Metrics, Linux Diagnostics* · `Experimental`
- Developed a lightweight system utility to track VRAM allocation, GPU memory bandwidth, compute utilization, and inference latency during local model execution.
- Profiled bottlenecks in model loading, context window allocation, and token generation throughput.

### NLP GitHub Issue Classifier
*Python, Natural Language Processing, Machine Learning* · `Prototype`
- Built an automated classification pipeline to triage open-source repository issues into labels (bug, feature request, documentation, enhancement) based on issue body and title.
- Explored text preprocessing, tokenization, TF-IDF vectorization, and baseline classifier evaluation.

### Archon — Browser Productivity Environment
*JavaScript, Chrome Extensions API, OAuth 2.0* · `Prototype` · [Repository ↗](https://github.com/akattri/project-hackfest)
- Developed a modular browser homepage and productivity environment integrating Google Calendar, local task queues, and Chrome bookmarks.
- Explored browser extension sandboxing, OAuth authentication flows, asynchronous storage APIs, and local state management.

---

## Academic & Research Interests

- **Primary Focus**: Operating systems, systems programming, concurrency, high-performance computing, Linux kernel concepts.
- **Machine Learning**: Systems for ML, inference optimization, resource profiling, natural language processing.
- **Internship Aims**: Seeking undergraduate research positions and open-source contributions (Mitacs Globalink, Google Summer of Code, Linux Foundation Mentorship, university research labs).

---

## Contact & Profiles

- **Email**: [akashkattri@gmail.com](mailto:akashkattri@gmail.com)
- **GitHub**: [github.com/akattri](https://github.com/akattri)
- **LinkedIn**: [linkedin.com/in/akattri](https://www.linkedin.com/in/akattri)
- **Website**: [akattri.github.io](https://akattri.github.io)

