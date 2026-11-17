# Analog Circuit Reasoning Benchmark

**Dataset Evaluation & Commercial Overview**  
**Format:** JSON | **Domain:** Analog Circuit Design | **Tasks:** 28

## Overview

The **Analog Circuit Reasoning Benchmark** is a simulation-verified dataset for evaluating how well AI models reason about analog circuits. It includes fully specified SPICE circuits, numerical prediction and parameter optimization tasks, ngspice reference results, and baseline answers from ChatGPT and Claude.

The benchmark is designed to test quantitative engineering reasoning, including cases where the model is instructed to work without running a circuit simulator.

## Dataset Specifications

| Property | Value |
|---|---|
| Total tasks | 28 |
| Circuit families | 3 |
| Task types | Numerical prediction; parameter optimization |
| Reference simulator | ngspice 47 |
| Verified reference results | 28/28 |
| Evaluation | Tolerance-based, with task-specific evaluation fields |
| Numerical accuracy criterion | Symmetric prediction/reference ratio ≥ 0.90 where specified |
| Format | Structured JSON |
| Split | Test |
| Difficulty label | `candidate_medium` |

## Task Distribution

| Circuit / Task | Count |
|---|---:|
| Voltage-controlled ring oscillator — prediction | 9 |
| First-order delta-sigma modulator — prediction | 7 |
| First-order delta-sigma modulator — optimization | 7 |
| Source-follower voltage buffer — prediction | 5 |
| **Total** | **28** |

## Verification and Dataset Quality

Each record contains a task description, circuit parameters or design constraints, reference measurements, baseline model responses, and evaluation results. The reference values are marked as verified against ngspice.

**Key strengths:**
- Reproducible circuit definitions and numerical ground truth.
- Quantitative scoring rather than subjective answer grading alone.
- Both prediction and design-optimization challenges.
- Baseline outputs and error information for comparative analysis.
- Structured records suitable for automated evaluation pipelines.

## Baseline Evaluation

| Recorded evaluation status | ChatGPT | Claude |
|---|---:|---:|
| Fully correct | 1 (3.6%) | 2 (7.1%) |
| Partially correct | 18 (64.3%) | 22 (78.6%) |
| Incorrect | 9 (32.1%) | 4 (14.3%) |

Neither baseline fully solved any of the nine VCO prediction tasks. These results suggest the benchmark is challenging for the evaluated models, but 28 tasks are insufficient for broad statistical claims about model rankings.

## Commercial Positioning

The dataset is suitable as a **focused evaluation benchmark** for AI labs, model developers, and researchers investigating analog circuit reasoning. Its main value is the combination of simulator-verified numerical answers, transparent circuit specifications, and baseline performance evidence.

**Current limitations:** The dataset contains only 28 tasks across three circuit families, all labeled `candidate_medium`. Broader circuit coverage, additional difficulty levels, independent reference audits, and more model baselines would strengthen a larger commercial release.

## Overall Assessment

**A technically grounded, compact benchmark for quantitative analog circuit reasoning.** Its verified references and challenging baseline results make it useful as a pilot benchmark or specialized evaluation set. It should not yet be presented as a comprehensive measure of analog electronics expertise.
