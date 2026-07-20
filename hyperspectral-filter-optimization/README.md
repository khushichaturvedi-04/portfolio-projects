# Hyperspectral Filter Array Optimization via Genetic Algorithms

**Undergraduate Research — Dr. Dror Baron's Lab, North Carolina State University**

---

## Overview

This project investigates the optimization of spectral filter arrays for compressive hyperspectral imaging using genetic algorithms (GA). The goal is to identify an optimal 8×8 filter configuration — selected from a library of 10,000 real spectral filters spanning 400–700nm across 31 channels — that minimizes reconstruction error on PRISMA satellite imagery.

## Method

- **Filter search:** Genetic algorithm search over an 8×8 filter array configuration, drawn from a library of 10,000 real spectral filters (400–700nm, 31 channels)
- **Reconstruction & evaluation:** Candidate filter configurations are evaluated by reconstructing hyperspectral imagery using Approximate Message Passing (AMP) paired with an adaptive 3D Wiener denoiser operating jointly across the wavelet and DCT spectral domains
- **Optimization pipeline:** Implemented in Python using the DEAP evolutionary computation framework with true multiprocessing for parallel fitness evaluation
- **Efficiency optimization:** Achieved a 24% reduction in total fitness evaluations by selectively re-evaluating only mutated individuals each generation, rather than the full population

## Results

Across 25 experimental runs totaling over 600 continuous generations, the GA-optimized filter configuration:

- Achieves a **21.5% improvement in Mean Squared Error (MSE)** over a random filter baseline
- Achieves a **20.1% improvement in Spectral Angle Mapper (SAM)** over a random filter baseline
- **Outperforms the existing domain-optimized baseline filter** on both metrics

## Skills Demonstrated

`Python` · `Genetic Algorithms` (DEAP) · `Evolutionary Computation` · `Parallel/Multiprocessing Optimization` · `Compressive Sensing` · `Approximate Message Passing (AMP)` · `Signal Processing` (Wavelet & DCT domains, Wiener denoising) · `Hyperspectral Imaging` · `Satellite Imagery Analysis` (PRISMA) · `Research Experimentation & Benchmarking`

## Status

Ongoing research.
