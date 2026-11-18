# Analog Circuit Reasoning Benchmark

**Dataset Evaluation & Research Overview**  
**Format:** JSON | **Domain:** Analog Circuit Design | **Tasks:** 28

## Overview

The **Analog Circuit Reasoning Benchmark** is a simulation-verified dataset for evaluating how well AI models reason about analog circuits. It includes fully specified SPICE circuits, numerical prediction and parameter optimization tasks, ngspice reference results, and baseline answers from GPT Astra and Claude Opus.

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

| Recorded evaluation status | GPT Astra | Claude Opus |
|---|---:|---:|
| Fully correct | 1 (3.6%) | 2 (7.1%) |
| Partially correct | 18 (64.3%) | 22 (78.6%) |
| Incorrect | 9 (32.1%) | 4 (14.3%) |

### Evaluation Status Explained

A task is counted as **fully correct** only when the model meets the evaluation criteria for **every required parameter** (typically 4–5, depending on the task).

- **Fully correct:** All required parameters pass their respective checks.
- **Partially correct:** At least one parameter passes, but the complete task does not. In many cases, this meant only **1 of 4** parameters was correct.
- **Incorrect:** No required parameters pass the evaluation checks.

**Partially correct tasks are not counted as successful solutions** in the full-task success rate. The exact checks may differ between numerical prediction and parameter-optimization tasks.

Neither baseline fully solved any of the nine VCO prediction tasks. These results suggest the benchmark is challenging for the evaluated models.

## Task Descriptions

The benchmark presents realistic SPICE netlists and asks models to apply transistor-level circuit analysis rather than run a simulator. Tasks specify component values, MOSFET models, operating conditions, measurement procedures, and required output units.

- **Ring oscillator prediction (9 tasks):** Estimate oscillation frequency, control-voltage tuning gain (KVCO), supply-voltage pushing, and power consumption for three-stage current-starved oscillators.
- **Delta-sigma modulator prediction (7 tasks):** Predict the behavior of fixed first-order modulators, including signal quality and power consumption, from their circuit parameters and sampling conditions.
- **Delta-sigma modulator optimization (7 tasks):** Select allowed transistor and circuit parameters within a fixed topology to satisfy performance constraints, including SNDR and power requirements.
- **Source-follower buffer prediction (5 tasks):** Estimate quiescent current, output swing, and total harmonic distortion for NMOS voltage buffers driven by a sinusoidal input.

Each task is paired with a simulator-derived reference and recorded model predictions, enabling quantitative comparison and detailed error analysis.

## Potential Research Applications

The dataset is intended for research and experimentation in:

- **Reinforcement Learning with Verifiable Rewards (RLVR):** Score numerical predictions against ngspice-derived reference values using deterministic reward functions.
- **Engineering Reasoning Evaluation:** Assess how models estimate circuit behavior from transistor-level specifications, including where analytical approximations diverge from simulation.
- **Domain-Specific Training:** Investigate whether training on circuit-analysis and parameter-optimization tasks improves quantitative reasoning on held-out engineering problems.
- **Model Failure Analysis:** Identify errors in physical assumptions, numerical estimation, circuit interpretation, and design-constraint satisfaction.

The current release provides static tasks, simulator-verified reference measurements, and baseline evaluations from **GPT Astra** and **Claude Opus**. It is **not** a fully interactive circuit-simulation environment.
