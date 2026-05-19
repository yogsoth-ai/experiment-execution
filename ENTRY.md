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

Four-Campaign Experiment Execution Engine — 从验证过的研究假设/方案出发，完成实验设计、约束分析、场景规划、实现规划与执行的全链路。

## Positioning

**前置条件**:
- north-star-crystallization 已完成（研究意图明确）
- hypothesis-formation 或 convergence/validation 已产出经过验证的方案/假设

**执行边界**: 全链路——从实验设计到实际执行到结果收集分析。

**产出**:
- 实验设计报告（变量、控制、指标、统计方法）
- 约束分析报告（瓶颈、依赖、冲突消解方案）
- 场景分析报告（多未来场景 + 鲁棒性评估）
- 可执行 plan（bite-sized task 格式）
- 实验结果报告（metrics + 统计检验 + 可复现性声明）

## Campaigns

| Campaign | 核心问题 | 输入 | 产出 |
|----------|---------|------|------|
| experiment-design | "做什么实验？" | 验证过的假设/方案 | 完整实验设计方案 |
| constraint-analysis | "什么限制了我们？" | 实验设计方案 + 现实约束 | 约束分析报告 + 消解方案 |
| scenario-planning | "未来可能怎样？" | 研究方案 + 不确定性 | 多场景分析 + 鲁棒性评估 |
| implementation-planning | "怎么做 + 做" | 设计 + 约束 + 场景 | 可执行 plan + 执行结果 |

## Campaign Routing

| Signal | Campaign |
|--------|----------|
| 实验设计、因子、变量、ablation、baseline 对比、统计方法 | → experiment-design |
| 瓶颈、约束、资源不足、依赖关系、冲突 | → constraint-analysis |
| 场景、未来、鲁棒性、最坏情况、竞争对手、时间线 | → scenario-planning |
| 规划、执行、实现、跑实验、结果分析、可复现性 | → implementation-planning |

## Multi-Campaign Orchestration

四个 campaign 完全灵活组合，CC 自主决定用几个、什么顺序：
- 典型串行: experiment-design → constraint-analysis → scenario-planning → implementation-planning
- 并联: constraint-analysis ∥ scenario-planning（可并行执行）
- 跳过: CC 有权跳过不需要的 campaign（如约束已明确则跳过 constraint-analysis）
- 回溯: CC 有权从后续 campaign 回溯（如执行中发现设计缺陷，回到 experiment-design）

## Context Management

- **Campaign start**: 调用 context-init（加载/创建 campaign context file）
- **每个 strategy 完成后**: 调用 context-checkpoint（硬性约束，不可跳过）
- **一个 context file per campaign**: 所有 strategy 产出累积在单个 campaign-scoped file

## Design Philosophy

兵法书模式 — CC 读完后内化原则，面对具体研究任务自行构建打法。

**硬约束仅四种**:
1. Budget Gate — 量化地板，不达标不能退出
2. Minimum Yield — 每次执行的最低产出要求
3. HARD-GATE — 前置条件检查，不满足不能开始
4. context-checkpoint — strategy 完成后必须触发

**CC 有权自主决策**:
- 简化 tactic 为只使用一批 SOP
- 决定迭代次数
- 决定 campaign 组合顺序
- 跳过不适用的 strategy
