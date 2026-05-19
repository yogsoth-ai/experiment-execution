---
name: experiment-execution
description: "Four-Campaign Experiment Execution Engine — designs experiments, analyzes constraints, plans scenarios, and executes with result collection"
version: 1.0.0
category: experiment-execution
type: entry
dependencies:
  skills:
    - web-browsing
    - literature-engine
    - context-management
    - subagent-spawning
  mcp:
    - brave-search
    - apify
    - alphaxiv
    - semantic-scholar
    - wiki-vault
---

# Experiment Execution

Four-Campaign Experiment Execution Engine — starting from validated research hypotheses/approaches, completes the full pipeline of experiment design, constraint analysis, scenario planning, implementation planning, and execution.

## Positioning

**Prerequisites**:
- north-star-crystallization completed (research intent is clear)
- hypothesis-formation or convergence/validation has produced validated approaches/hypotheses

**Execution boundary**: Full pipeline — from experiment design to actual execution to result collection and analysis.

**Outputs**:
- Experiment design report (variables, controls, metrics, statistical methods)
- Constraint analysis report (bottlenecks, dependencies, conflict resolution plans)
- Scenario analysis report (multiple future scenarios + robustness assessment)
- Executable plan (bite-sized task format)
- Experiment results report (metrics + statistical tests + reproducibility statement)

## Campaigns

| Campaign | Core Question | Input | Output |
|----------|--------------|-------|--------|
| experiment-design | "What experiment to run?" | Validated hypotheses/approaches | Complete experiment design |
| constraint-analysis | "What limits us?" | Experiment design + real-world constraints | Constraint analysis report + resolution plans |
| scenario-planning | "What might the future look like?" | Research approach + uncertainties | Multi-scenario analysis + robustness assessment |
| implementation-planning | "How to do it + do it" | Design + constraints + scenarios | Executable plan + execution results |

## Campaign Routing

| Signal | Campaign |
|--------|----------|
| experiment design, factors, variables, ablation, baseline comparison, statistical methods | → experiment-design |
| bottleneck, constraint, insufficient resources, dependencies, conflicts | → constraint-analysis |
| scenarios, future, robustness, worst case, competitors, timeline | → scenario-planning |
| planning, execution, implementation, running experiments, result analysis, reproducibility | → implementation-planning |

## Multi-Campaign Orchestration

The four campaigns can be flexibly combined; CC autonomously decides how many to use and in what order:
- Typical serial: experiment-design → constraint-analysis → scenario-planning → implementation-planning
- Parallel: constraint-analysis ∥ scenario-planning (can execute in parallel)
- Skip: CC may skip campaigns that are not needed (e.g., skip constraint-analysis if constraints are already clear)
- Backtrack: CC may backtrack from later campaigns (e.g., return to experiment-design if execution reveals design flaws)

## Context Management

- **Campaign start**: invoke context-init (load/create campaign context file)
- **After each strategy completes**: invoke context-checkpoint (hard constraint, cannot be skipped)
- **One context file per campaign**: all strategy outputs accumulate in a single campaign-scoped file

## Design Philosophy

Art of War mode — CC internalizes the principles after reading, then autonomously constructs its approach for each specific research task.

**Only four hard constraints**:
1. Budget Gate — quantitative floor, cannot exit without meeting it
2. Minimum Yield — minimum output requirement per execution
3. HARD-GATE — prerequisite check, cannot start without satisfying it
4. context-checkpoint — must be triggered after each strategy completes

**CC has autonomous decision authority over**:
- Simplifying tactics to use only a subset of SOPs
- Deciding iteration count
- Deciding campaign combination and ordering
- Skipping inapplicable strategies
