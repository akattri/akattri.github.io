---
title: "Thread-Safe Concurrent Queue"
date: 2026-03-01
date_display: "2026"
description: "A multi-producer, multi-consumer bounded FIFO queue in C using POSIX threads, mutexes, and condition variables."
status: "in progress"
domain: "Concurrency & Systems Programming"
technologies:
  - "C"
  - "pthreads"
  - "Mutex Locks"
  - "Condition Variables"
  - "Memory Safety"
github: "https://github.com/akattri"
demo: ""
featured: true
weight: 20
---

## Overview

A lock-based concurrent First-In, First-Out (FIFO) queue implemented in C. The data structure safely coordinates data sharing across multiple producer and consumer threads without race conditions, memory corruption, or CPU-wasting busy waits.

---

## Why I Built It

Concurrent data structures form the backbone of modern operating systems, web servers, database engines, and asynchronous task runners. 

Writing a thread-safe queue in C forces a programmer to confront the edge cases of parallel execution:
- How to coordinate threads when a buffer is full or empty without polling loops?
- How to guarantee memory ordering and visibility across CPU cores?
- How to prevent spurious wakeups and avoid priority inversions or deadlocks?

This project was conceived as a hands-on exploration of POSIX threading primitives (`pthread_mutex_t`, `pthread_cond_t`) and low-level synchronization theory.

---

## What I Learned & Engineering Takeaways

- **Synchronization Overhead**: Uncontended mutex locks are fast on modern Linux (leveraging `futex` under the hood), but contention introduces thread descheduling and context switch overhead.
- **Spurious Wakeups**: Why condition variable waits (`pthread_cond_wait`) must always be wrapped in a `while` loop rather than an `if` statement, ensuring predicate re-evaluation upon regaining the lock.
- **Bounded Buffer Flow Control**: Balancing producers and consumers using two separate condition variables (`cond_not_empty` and `cond_not_full`) to prevent buffer starvation and overflow.
- **Clean Teardown & Cancellation**: Designing an orderly queue shutdown protocol where worker threads are gracefully awakened and joined without leaking memory or leaving unconsumed tasks in limbo.

---

## Technical Architecture & Implementation

The bounded queue relies on a circular buffer with head and tail pointers protected by a mutual exclusion lock:

```c
typedef struct {
    void **buffer;          /* Array of generic pointers */
    size_t capacity;        /* Maximum elements buffer can hold */
    size_t size;            /* Current count of elements */
    size_t head;            /* Index of next element to dequeue */
    size_t tail;            /* Index of next slot to enqueue */
    
    pthread_mutex_t lock;   /* Synchronizes critical sections */
    pthread_cond_t not_empty; /* Signaled when an item is enqueued */
    pthread_cond_t not_full;  /* Signaled when an item is dequeued */
    bool shutdown;          /* Flag to signal worker thread termination */
} concurrent_queue_t;
```

### Core Operations
- `queue_push(queue, item)`: Blocks if the queue has reached capacity until space becomes available, then enqueues the item and signals `not_empty`.
- `queue_pop(queue)`: Blocks if the queue is empty until an item is enqueued, then dequeues the item and signals `not_full`.
- `queue_destroy(queue)`: Signals shutdown to all waiting threads, frees internal allocations, and destroys POSIX synchronization objects.

---

## Future Directions & Open Questions

- **Lock-Free Exploration**: Investigating atomic compare-and-swap (`atomic_compare_exchange`) and Michael-Scott lock-free queue algorithms.
- **Benchmarking**: Measuring throughput across varying thread counts and assessing cache line false sharing.
- [Add technical details here]

