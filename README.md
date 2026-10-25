# Neutral Cognitive Architecture Framework (NCAF)
### Mechanism-Grounded Evaluation Task Battery for Artificial General Intelligence

[![Specification](https://img.shields.io/badge/Spec-NCAF_1.0-blue.svg)](ncaf-specification.md)
[![Status](https://img.shields.io/badge/Status-Archived_Research_Spec-lightgrey.svg)](#)
[![Domain](https://img.shields.io/badge/Domain-Cognitive_Architecture_&_AGI_Evaluation-darkgreen.svg)](#)

> **Note on Origins**  
> This specification began as an AI-assisted exploratory exercise inspired by Kaggle-related benchmark initiatives and cognitive science literature. It was developed as a theoretical thought experiment and architecture framework rather than an official competition entry.

---

## Executive Overview

The **Neutral Cognitive Architecture Framework (NCAF)** is an evaluation task battery designed to test whether an artificial intelligence system genuinely instantiates core cognitive faculties or merely simulates their outward products through surface shortcuts.

Most modern AI benchmarks evaluate static input-output pairs or zero-shot prompt completions. NCAF complements behavioral taxonomies (such as DeepMind's cognitive taxonomy) by grounding every evaluation task in the **necessary architectural mechanism** the task is designed to probe. 

If a task only measures output, it cannot distinguish a system that possesses an internal cognitive mechanism from one that mimics its product via pattern-matching or external lookup. NCAF isolates target faculties using tasks structurally unsolvable via known computational shortcuts.

```mermaid
graph TD
    subgraph Entropy & Persistence [Track 1: Learning]
        A[Trace Encoded S₀] -->|Exponential Decay τ| B[Trace S_t]
        B -->|Spaced Retrieval Probe| C{Threshold θ}
        C -->|Renewal Operator η| A
        C -->|Below θ| D[Trace Extinction]
    end

    subgraph Capacity Limits [Track 4: Executive Functions]
        E[Active Working Memory Nodes] -->|Load < ω| F[High-Fidelity Manipulation]
        E -->|Load ≥ ω+1| G[Destructive Interference Break Point]
    end
