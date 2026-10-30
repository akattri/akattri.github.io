---
title: "LLM Resource Monitor"
date: 2026-01-15
date_display: "2026"
description: "A systems diagnostics utility for tracking VRAM footprint, memory fragmentation, and inference throughput during local model execution."
status: "experimental"
domain: "Systems for Machine Learning"
technologies:
  - "Python"
  - "Linux Diagnostics"
  - "VRAM / CUDA Telemetry"
  - "Profiling"
  - "CLI Utilities"
github: "https://github.com/akattri/llm-resource-mon"
demo: ""
featured: true
weight: 40
---

## Overview

A telemetry and profiling tool designed to observe how local large language models consume memory and compute resources during inference. It inspects GPU VRAM allocation, context window KV-cache expansion, token generation velocity, and system memory swapping.

---

## Why I Built It

As models are deployed locally on constrained hardware, system-level resource bottlenecks often dominate performance:
- How much VRAM does the KV-cache consume as the context window scales?
- When does CPU-offloading cause severe PCIe bus latency?
- How does quantization (e.g., 4-bit vs. 8-bit weights) affect memory bandwidth and computational throughput?

Rather than treating local inference as a black box, this utility provides real-time visibility into the memory lifecycle of model executions.

---

## What I Learned & Engineering Takeaways

- **KV-Cache Scaling**: The memory footprint of the autoregressive key-value cache scales linearly with batch size, context sequence length, and model layers, often outstripping weight memory during long context runs.
- **Memory Fragmentation**: Frequent tensor allocations and deallocations lead to virtual memory fragmentation if memory pools are not managed carefully.
- **PCIe Transfer Latency**: Offloading model layers between CPU RAM and GPU VRAM introduces massive latency stalls that dwarf the actual compute time of matrix operations.

---

## Technical Architecture & Implementation

```
[Inference Process / Model] ──> [Hardware Telemetry Probe] ──> [Event Aggregator]
                                           │                          │
                                           ▼                          ▼
                                 [VRAM / PCIe / CPU Stats]    [Terminal UI / Log]
```

### Metrics Monitored
- Peak and instantaneous VRAM usage
- Tokens per second (prompt processing phase vs. token generation phase)
- System RAM page faults and swap I/O
- Thermal throttling triggers

---

## Future Directions & Open Questions

- **Unified Memory Profiling**: Extending metrics to inspect memory pressure on unified memory architectures.
- **Automated Context Pruning Analysis**: Measuring latency impacts when implementing sliding-window attention or token evictions.

