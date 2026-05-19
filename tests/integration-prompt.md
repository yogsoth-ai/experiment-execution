# Integration Test Prompt

Use this prompt to validate the experiment-execution skill repo works end-to-end.

## Setup

1. Ensure all dependency skills are available:
   - web-browsing
   - literature-engine
   - context-management
   - subagent-spawning

2. Ensure MCP servers are connected:
   - brave-search
   - apify
   - alphaxiv
   - semantic-scholar
   - wiki-vault

## Test Scenario

**Input**: A validated research hypothesis from hypothesis-formation:

> "Hypothesis: Adding retrieval-augmented generation (RAG) to a 7B parameter language model will improve factual accuracy on closed-book QA tasks by at least 15% (measured by exact match score on TriviaQA), compared to the base model without retrieval, while increasing inference latency by no more than 2x."

## Expected Behavior

### Phase 1: Campaign Routing

The system should route this to `experiment-design` campaign based on signals: "experiment", "baseline comparison", "statistical method".

### Phase 2: Experiment Design Campaign

Expected flow:
1. HARD-GATE check passes (hypothesis exists, is falsifiable, scope is bounded)
2. Strategy selection: `comparison-design` (primary) + `factor-level-design` (secondary)
3. SOPs invoked:
   - `factor-identification` → IV: RAG (on/off), DV: exact match score + latency
   - `baseline-selection` → base 7B model, SOTA RAG system, simple BM25 retrieval
   - `metric-specification` → primary: EM score; secondary: F1, latency
   - `sample-size-estimation` → power analysis for 15% effect size
4. Context checkpoint after each strategy

### Phase 3: Constraint Analysis Campaign

Expected:
1. Resource constraints identified (GPU hours, dataset access, model weights)
2. Dependency graph (data prep → model setup → retrieval index → evaluation)
3. Bottleneck: retrieval index construction time

### Phase 4: Implementation Planning Campaign

Expected:
1. Critical path calculated
2. Plan formatted as bite-sized tasks
3. Execution dispatched via subagent-execution-loop

## Validation Criteria

| Criterion | Pass Condition |
|-----------|---------------|
| Routing correct | experiment-design selected as first campaign |
| HARD-GATE works | Preconditions checked before campaign entry |
| Strategy selection | comparison-design chosen for hypothesis type |
| SOP execution | At least 3 SOPs produce non-empty output |
| Context management | context-checkpoint called after each strategy |
| Budget gate | Output meets minimum tier S requirements |
| Cross-campaign flow | At least 2 campaigns execute in sequence |
| Statistical method | Paired bootstrap or Bayesian ROPE selected |
| Reproducibility | Seed protocol included in design |
| Final report | Synthesis SOP produces coherent report |

## Running the Test

```
1. Load ENTRY.md into CC context
2. Present the test hypothesis above
3. Observe campaign routing and execution
4. Verify each criterion in the table above
5. Check context files are created and checkpointed
```

## Known Limitations

- GPU/remote execution is not yet implemented (planned for future iteration)
- Actual experiment running requires compute resources beyond what this test validates
- This test validates the planning and design chain, not actual execution results
