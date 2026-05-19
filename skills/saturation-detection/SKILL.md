---
name: saturation-detection
description: "Shared SOP: detect information saturation — know when to stop searching/analyzing"
version: 1.0.0
category: experiment-execution
type: sop
execution: subagent
prompt: ./prompt.md
used-by: all-campaigns
input: "Current information set + last N rounds of new additions"
output: "Saturation verdict (saturated/not-saturated) + evidence"
---

# Saturation Detection

Detect information saturation — know when to stop searching or analyzing.

## Execution

Subagent — spawned via subagent-spawning/spawn-agent skill.

## Why Subagent

Saturation assessment requires independent evaluation of marginal information gain, avoiding confirmation bias from the main flow.

## Saturation Criteria

- New information no longer changes conclusions
- New sources repeat existing findings
- Coverage reaches preset threshold
- Marginal information gain falls below threshold
