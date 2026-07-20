# Quantum Error Mitigation via Post-Processing

**Research Experience for Undergraduates (REU)**
**Department of Electrical and Computer Engineering, North Carolina State University**

📄 [View the research poster (PDF)](./poster.pdf)

---

## Overview

This project investigated whether structured **post-processing** correcting quantum computing errors after a circuit has already run can meaningfully improve output accuracy on today's noisy quantum hardware, without requiring any changes to the hardware itself. The work compared two error-mitigation techniques, HAMMER and Q-BEEP, evaluated through large-scale noisy-vs-noise-free circuit simulation on an HPC cluster.

**Team:** Khushi Chaturvedi, Kelly Mae Allen, Christopher Mori, Kausthubh Prabha Chandramouli — advised by Dr. Dror Baron, Department of Electrical and Computer Engineering, NC State University

## My Role

Primarily responsible for the HPC and data pipeline: automating batch submission of simulation jobs to the Hazel HPC cluster, managing multi-core compute node runs, and structuring the collected output-distribution data (from both noise-free and noisy simulation modes) into a clean, reusable format for downstream error-mitigation analysis.

## The Problem

Modern small-scale quantum computers (NISQ devices — Noisy Intermediate-Scale Quantum) are powerful enough to tackle interesting problems, but their outputs are corrupted by hardware noise, making raw results difficult to trust. Waiting for hardware to mature enough to eliminate this noise isn't a near-term option — so the alternative is correcting for it computationally, after the fact.

**Key insight motivating the approach:** incorrect outputs aren't random — they cluster at a small Hamming distance (a small number of bit flips) from the correct answer, which makes them statistically recoverable through post-processing.

## Method

**Simulation setup:**
- Circuits built and transpiled in **Qiskit** (Python)
- **Quiet (noise-free) simulation** via Qiskit's Aer simulator to establish the true output distribution, P_true(x)
- **Noisy simulation** using Qiskit noise models built from real IBM device calibration data, to produce a realistic noisy output distribution, P_noisy(x)
- Batch jobs (~10,000 shots per circuit) automated and submitted to the **Hazel HPC cluster**, with results collected into CSV files for downstream processing

**Error-mitigation techniques evaluated:**

- **HAMMER (Hamming Reconstruction):** For each candidate output, builds a "Hamming spectrum" — counts of nearby outputs at increasing bit-flip distance — computes a neighborhood clustering score, and selects the most likely true output based on combined observed and neighborhood-weighted likelihood.
- **Q-BEEP (Bayesian Poisson Error Model):** Models error counts at each Hamming distance as following a Poisson process, initialized from device calibration data and updated via Bayesian inference over an undirected graph of bitstrings connected by single-bit-flip edges, to select the highest-posterior-probability output.

## Results & Discussion

- **HAMMER** is straightforward and computationally cheap, and performs well for small, simple error patterns.
- **Q-BEEP** captures more complex error structure that HAMMER misses at larger Hamming distances, at the cost of requiring more data and computation.
- **Shared limitation:** both methods assume a constant error rate and do not yet account for dynamic drift in real device behavior over time.

## Conclusion & Next Steps

A structured post-processing approach can meaningfully reduce NISQ-era quantum computing errors without any hardware changes. Planned next directions include:

- Extending the model to phase-flip and combined error channels (beyond bit-flip errors)
- Moving toward real-time, on-the-fly calibration that adapts priors as device conditions change
- Exploring on-controller implementation to enable in-flight error correction during circuit execution

## Skills Demonstrated

`Qiskit / Quantum Circuit Simulation` · `HPC Batch Job Automation` (Hazel cluster) · `Python` · `Data Pipeline Design` · `Noise Modeling` · `Bayesian Inference` · `Scientific Research & Documentation`

## References

Tannu, S., Stein, S., Wiebe, N., & Su, Y. (2022). HAMMER: Boosting fidelity via Hamming reconstruction. In *Proceedings of the 27th ACM International Conference on Architectural Support for Programming Languages and Operating Systems (ASPLOS '22)* (pp. 123–136). ACM.

Stein, S., Wiebe, N., & Lee, G. (2023). Q-BEEP: Bayesian Poisson error mitigation for quantum computing.
---
*NC State University REU — Department of Electrical and Computer Engineering
