# experiment-execution

Four-Campaign Experiment Execution Engine — designs experiments, analyzes constraints, plans scenarios, and executes with result collection across the full research lifecycle.

## What It Does

Starting from validated research hypotheses (output of hypothesis-formation or convergence/validation), this skill repo completes the full experiment pipeline:

1. **Experiment Design** — transforms hypotheses into rigorous experiment designs (variables, factors, design matrices, statistical methods, reproducibility protocols)
2. **Constraint Analysis** — identifies bottlenecks, quantifies resource constraints, analyzes dependencies, resolves conflicts using Theory of Constraints
3. **Scenario Planning** — constructs multiple future scenarios via morphological analysis, assesses robustness of the research approach
4. **Implementation Planning** — plans execution path, dispatches subagents, runs experiments, collects and analyzes results

## Architecture

```
ENTRY.md (routing + orchestration)
└── skills/
    ├── 4 campaigns (experiment-design, constraint-analysis, scenario-planning, implementation-planning)
    ├── 20 strategies (5 per campaign)
    ├── 13 tactics (3+3+3+4)
    ├── 41 subagent SOPs (SKILL.md + prompt.md)
    ├── 5 import SOPs (web-search, web-research, paper-overview, paper-search, paper-research)
    └── 2 shared SOPs (saturation-detection, quality-gate-check)
```

All files are flat in `skills/` — logical hierarchy is expressed through frontmatter `used-by` fields.

## Methodology

| Campaign | Core Methods |
|----------|-------------|
| experiment-design | Fisher DOE, Taguchi, ABLATOR, Benavoli 2017 Bayesian Comparison, Paired Bootstrap |
| constraint-analysis | Goldratt TOC, Current Reality Tree, Evaporating Cloud, Critical Chain |
| scenario-planning | Zwicky Morphological Analysis, Ritchey CCA, Shell Scenario Method, RAND Scenario Discovery |
| implementation-planning | CPM, TOC Prerequisite/Transition Tree, superpowers writing-plans, subagent-driven-development |

## Dependencies

| Skill | Provides |
|-------|----------|
| web-browsing | web-search, web-research |
| literature-engine | paper-overview, paper-search, paper-research |
| context-management | context-init, context-checkpoint |
| subagent-spawning | spawn-agent (runtime for all subagent SOPs) |

## MCP Servers

- **brave-search** — web search discovery
- **apify** — full-page content extraction
- **alphaxiv** — paper search and PDF reading
- **semantic-scholar** — paper metadata and citations
- **wiki-vault** — knowledge graph operations

## Usage

Load `ENTRY.md` into CC context. The routing table maps signal words to campaigns. CC autonomously decides campaign combination, ordering, and iteration depth.

## License

MIT
