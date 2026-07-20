# Parallel Programming & Computer Architecture Simulation

---

## Overview

Two projects from a graduate-level parallel/computer-architecture course, covering shared-memory parallel programming with OpenMP and cache coherence protocol design using the Structural Simulation Toolkit (SST). Together they span performance-oriented parallel software engineering and low-level hardware coherence protocol implementation.

---

## Project 1: Parallel Ocean Temperature Simulation (OpenMP)

Implemented a shared-memory parallel C program that iteratively simulates ocean surface temperature on a 2D grid, using a stencil computation where each interior point is updated as the average of its neighbors from the previous time step.

**Implementation:**
- Wrote `ocean.c` from a provided specification, using a double-buffered (read/write) grid to correctly handle the time-step dependency between neighboring points
- Parallelized the core update loop with OpenMP, driven entirely by the `OMP_NUM_THREADS` environment variable rather than hardcoded thread counts
- Handled command-line-driven configuration: grid size, number of time steps, input file, and output file, with correct row-major floating-point I/O

**Performance analysis:**
- Benchmarked the parallel implementation across 1, 2, 4, 8, and 16 threads on the university's HPC cluster (fixed processor model, exclusive-access allocation)
- Evaluated three work-sharing (OpenMP scheduling) strategies: static scheduling with chunk count equal to thread count, static scheduling with fixed chunk size (32), and dynamic scheduling
- Collected mean, standard deviation, and 95% confidence intervals across repeated runs (10 per configuration) to characterize performance and variability across strategies and thread counts

## Project 2: Cache Coherence Protocol Instrumentation & Optimization (SST)

Worked directly inside the L1 cache coherence manager of the Structural Simulation Toolkit (SST), a parallel simulation framework used for modeling HPC system components such as processors, memory hierarchies, and coherence protocols.

**Part 1 — Coherence event instrumentation:**
- Instrumented the `MESI_L1` coherence manager to increment defined counters at the correct points whenever specific MESI protocol events and state transitions occurred, without altering the protocol's functional behavior
- Traced through protocol state-transition logic to precisely identify where requests are issued and where coherence state changes actually happen
- Validated instrumentation against provided test cases run through SST's Miranda-based bus coherence test suite

**Part 2 — Coherence protocol optimization (MESI → MOESI extension):**
- Extended the existing MESI coherence protocol implementation to MOESI by introducing the Owned state, allowing dirty cache lines to be shared directly between caches without a costly write-back to memory on every read by another core
- Modified coherence logic in `MESI_L1` to correctly handle the new state's transitions, gated behind a runtime-configurable optimization flag so the base and optimized protocols could be tested side-by-side without rebuilding
- Built a directed test case using the Prospero CPU trace-driven model to force repeated ownership/sharing transitions across cores, demonstrating the reduction in unnecessary memory write-backs enabled by the Owned state

## Skills Demonstrated

`C` · `OpenMP` · `Shared-Memory Parallel Programming` · `Performance Benchmarking & Statistical Analysis` · `HPC Cluster Job Execution` · `Computer Architecture` · `Cache Coherence Protocols (MESI/MOESI)` · `C++` (SST/`MESI_L1.cc`) · `Discrete-Event Architecture Simulation (SST)` · `Low-Level Systems Debugging`

## Result

Delivered a working parallel ocean-simulation implementation benchmarked across all required thread counts and work-sharing strategies, and a working MESI-to-MOESI coherence protocol extension in SST, validated with a directed multi-core test case demonstrating the intended reduction in coherence traffic.
