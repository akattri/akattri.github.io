---
title: "Curriculum Vitae"
description: "Academic background, coursework, systems engineering experience, and technical foundations."
---

<div style="display: flex; justify-content: space-between; align-items: baseline; margin-bottom: 2rem; border-bottom: 1px solid var(--border); padding-bottom: 1rem;">
  <div>
    <span style="font-family: var(--font-mono); font-size: 0.85rem; font-weight: 500; color: var(--text-faint);">Online Resume · Academic Record</span>
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
*C, Linux System Calls, Process Management* · `In Progress / Experimental` · [Repository ↗](https://github.com/akattri/seashell)
- Implemented a command-line shell from scratch in C to understand process creation and inter-process communication.
- Implemented command parsing, execution loop, child process spawning via `fork()` and `execvp()`, and process lifecycle reaping with `waitpid()`.
- Built I/O redirection (`<`, `>`) and inter-process pipelines using `pipe()` and `dup2()`.
- Implemented signal handling for `SIGINT` (Ctrl+C) and `SIGTSTP` (Ctrl+Z) to prevent shell termination.

### Thread-Safe Concurrent Queue
*C, POSIX Threads (pthreads), Concurrency* · `In Progress / Experimental` · [Repository ↗](https://github.com/akattri/thread-safe-queue)
- Developed a thread-safe First-In-First-Out (FIFO) queue in C supporting concurrent multi-producer, multi-consumer access.
- Synchronized enqueue and dequeue operations using POSIX mutual exclusion locks (`pthread_mutex_t`) and condition variables (`pthread_cond_t`).
- Validated under ThreadSanitizer with zero data races across 200,000 operations and ~3.5M ops/sec throughput.

### LLM Resource Monitor
*Python, Systems / ML Metrics, Linux Diagnostics* · `Experimental` · [Repository ↗](https://github.com/akattri/llm-resource-mon)
- Developed a lightweight system utility to track on-chip GPU utilization, VRAM allocation, power draw, and host CPU usage during local LLM inference.
- Profiled memory allocation scaling and execution latency between cold start (weight loading into VRAM) and cached warm start generation.

### GitHub Issue Security Classifier
*Python, Natural Language Processing, Machine Learning* · `Prototype` · [Repository ↗](https://github.com/akattri/github-issue-classifier)
- Built an automated NLP pipeline using NLTK and scikit-learn to classify open-source repository issues as security-related or non-security.
- Evaluated TF-IDF vectorization and Multinomial Naive Bayes on a stratified 200-issue dataset, achieving 87.5% test accuracy with documented lexical bias analysis.

### Archon — Browser Productivity Environment
*JavaScript, Chrome Extensions API, Manifest V3, OAuth 2.0* · `Prototype` · [Repository ↗](https://github.com/akattri/Archon)
- Developed a modular browser new-tab dashboard integrating Google Calendar, local task queues, and Chrome bookmarks.
- Implemented client-side OAuth 2.0 flows via `chrome.identity`, least-privilege scoping (`calendar.readonly`), and local state caching via `chrome.storage.local`.

### Veto — Video Access Control & Embed Filter
*JavaScript, Manifest V3, declarativeNetRequest, PBKDF2* · `Active Prototype` · [Edge Add-on ↗](https://microsoftedge.microsoft.com/addons/detail/veto-youtube-video-ac/mgenhkdhpgjfpdclndfnbaieojcikiol) · [Case Study ↗](/projects/veto/)
- Built a Manifest V3 browser extension for Edge and Chromium enforcing origin embed filtering, channel allowlists, and media element access controls.
- Implemented multi-world content script interception (main-world inspection and isolated-world policy engine), disjunctive channel/video decision logic, and time-delayed cooling-off rule modifications.

### Cogleaf — Cognitive Exercise Suite
*React 19, TypeScript, Three.js, Capacitor, Web Audio API* · `Prototype` · [Live Demo ↗](https://cogleaf.vercel.app/) · [Case Study ↗](/projects/cogleaf/)
- Engineered an offline-first cognitive wellness application implementing classic psychological task paradigms (visual attention tracking, Stroop interference, N-Back working memory updating).
- Designed procedural Web Audio sound synthesis, Three.js environmental rendering, and neuro-inclusive sensory accessibility controls (reduced motion, pacing adjustments).

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

