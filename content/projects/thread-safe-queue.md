---
title: "Thread-Safe Concurrent Queue"
date: 2026-03-01
date_display: "2026"
description: "A multi-producer, multi-consumer FIFO queue in C synchronized with POSIX mutexes and condition variables."
status: "in progress"
domain: "Concurrency & Systems Programming"
technologies:
  - "C"
  - "pthreads"
  - "Mutex Locks"
  - "Condition Variables"
  - "ThreadSanitizer"
github: "https://github.com/akattri/thread-safe-queue"
demo: ""
featured: true
weight: 30
---

## Overview

A thread-safe concurrent First-In, First-Out (FIFO) queue implemented in C. The data structure safely coordinates asynchronous data transfers across multiple concurrent producer and consumer threads without data races, memory corruption, or CPU-burning busy-waiting.

---

## Why I Built It

Concurrent data structures form the backbone of modern operating systems, web servers, asynchronous task pools, and pipeline runtimes.

Writing a thread-safe queue in pure C confronts core parallel programming challenges:
- How to coordinate threads when a queue is empty without polling loops?
- How to minimize critical section latency so threads do not serialize behind heap allocations?
- How to protect against spurious wakeups and guarantee clean shutdown signaling without dangling consumer threads or memory leaks?

---

## What I Learned & Engineering Takeaways

- **Heap Allocation Outside Critical Sections**: Allocating nodes before acquiring `pthread_mutex_t` minimizes lock hold time and prevents thread serialization on memory allocator locks.
- **Spurious Wakeup Handling**: Condition variable waits (`pthread_cond_wait`) must always execute in a `while` loop, ensuring predicate re-evaluation upon regaining the lock.
- **Signal vs. Broadcast Coordination**: Using `pthread_cond_signal()` for item enqueues avoids the "thundering herd" problem, while `pthread_cond_broadcast()` on queue shutdown ensures all sleeping consumers unblock and terminate cleanly.
- **Data Race Validation**: Validated under Clang/GCC `ThreadSanitizer` (`-fsanitize=thread`) with zero reported data races across 200,000 concurrent operations.

---

## Technical Architecture & Implementation

The queue is implemented as a singly-linked list of dynamically allocated `Node` elements protected by a mutex and condition variable:

```
[Producers] ──> queue_push() ──> [rear] -> [Node] -> [Node] -> [front] ──> queue_pop() ──> [Consumers]
                      │                                              │
                      ▼                                              ▼
               Acquires lock,                                 Acquires lock,
               links node,                                    waits on not_empty,
               signals cond                                   dequeues & frees
```

### Data Structures (`src/queue.h`)
```c
typedef struct Node {
    int data;
    struct Node *next;
} Node;

typedef struct Queue {
    Node *front;
    Node *rear;
    size_t size;
    pthread_mutex_t lock;
    pthread_cond_t not_empty;
    int shutdown; /* 0 = active, 1 = shutdown */
} Queue;
```

---

## Empirical Stress Testing & Performance

The implementation was evaluated using a dedicated multithreaded stress test harness (`tests/stress_test.c`):
- **Workload**: 8 concurrent producer threads and 8 consumer threads exchanging 200,000 items.
- **Throughput**: ~3.5 million operations/sec (push + pop) under release compilation (`-O2`).
- **Integrity Verification**: Verified via 64-bit mathematical checksums ($\sum_{i} \text{item}_i$). 100% data integrity with zero lost, duplicated, or corrupted items.
- **ThreadSanitizer Clean**: Zero data races reported under `-fsanitize=thread`.

---

## Current Limitations & Future Work

- **Unbounded Capacity**: The queue is dynamically sized and limited only by system RAM. It does not block producers when memory usage grows (no bounded backpressure).
- **Single Lock Contention**: A single coarse-grained mutex guards both `front` and `rear`, creating contention under high core counts. Future work includes exploring two-lock queues (e.g. Michael & Scott queue) or lock-free atomic queues.
