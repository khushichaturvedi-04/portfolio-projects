# City Transportation Planner

**ECE 309: Data Structures and Object-Oriented Programming for Electrical and Computer Engineers**
---

## Overview

A city transportation planner that answers shortest-path queries over a large graph of transit stops and routes. The system parses a real-world-scale dataset (~10,000 stops, ~30,000 undirected edges), builds an efficient in-memory graph representation, and computes shortest paths and estimated travel times using Dijkstra's algorithm — all under a strict per-query time limit with fully deterministic output.

## Problem

Given a city's transit network as a list of stops connected by weighted (distance) edges, answer queries of the form "what's the shortest route and travel time between stop A and stop B?" — reliably, deterministically, and efficiently enough to handle a large-scale graph within a 30-second per-query limit, with no network access and no external libraries.

## Architecture

| Component | Implementation |
|---|---|
| **Language** | C++17 (standard library only, no external dependencies) |
| **Graph representation** | Adjacency list — stop names (`std::string`) mapped to compact integer IDs via `std::unordered_map`, with a reverse `std::vector<std::string>` for ID → name lookup; edges stored as `std::vector<std::vector<std::pair<int,double>>>` |
| **Shortest-path algorithm** | Dijkstra's algorithm using a binary min-heap (`std::priority_queue`) keyed on tentative distance, with early exit once the destination is settled |
| **I/O contract** | Reads `src dst` queries from stdin; prints `ok <distance_m> <eta_s>` or `error no_path` to stdout (kept clean for autograding); prints the full resolved path to stderr for debugging without polluting graded output |
| **Build system** | Makefile (`g++ -std=c++17 -Wall -Wextra -O2`) |

## Features Implemented

**Required:**
- Adjacency-list graph construction from a UTF-8, space-separated edge-list file
- Dijkstra-based shortest-path computation for nonnegative edge weights
- Full path reconstruction and reporting (to stderr) for every successful query
- Deterministic behavior: identical inputs always produce identical outputs, with all data structures initialized in fixed order and no randomness or network I/O

**Bonus (both implemented, via a separate `planner_bonus` executable):**
- **Batch benchmarking mode** (`--benchmark`) — runs Dijkstra across many queries and writes a CSV (`src, dst, distance_m, eta_s, time_ms`) timed with `std::chrono::high_resolution_clock`
- **Path export mode** (`--export`) — writes each successful shortest path, as a space-separated stop-ID sequence, to `path.txt`

## Engineering Highlights

- **Scaled correctly** — verified functionally correct and within time limits against a hidden smoke-test graph roughly two orders of magnitude larger than the illustrative sample data (~10K nodes / ~30K edges).
- **Clean separation of graded vs. debug output** — successful/failed query results go to stdout in a strict, autograder-parseable format, while full path traces go to stderr, keeping both concerns satisfied without one interfering with the other.
- **Reusable core** — the `Graph` and `dijkstra` implementations are shared, unmodified, between the required planner and the bonus executable, rather than duplicated.
- **Reproducible builds** — separate Makefiles for the core planner and bonus executable, with documented build/run steps and expected output for each mode.

## Skills Demonstrated

`C++17` · `Object-Oriented Design` · `Graph Data Structures (Adjacency List)` · `Dijkstra's Algorithm` · `Priority Queue / Min-Heap` · `STL Containers` (`unordered_map`, `vector`, `priority_queue`) · `Makefile-based Build Systems` · `CLI Tool Design (stdin/stdout/stderr discipline)` · `Performance Benchmarking` · `Reproducible Engineering Documentation`

## Result

Completed all required functionality plus both optional bonus features (batch benchmarking and path export), verified against the course's large-scale hidden smoke test and documented with full build/run reproducibility instructions.
