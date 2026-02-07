---
name: comptext-optimize
description: Analyze and optimize token usage with CompText V5.0. Use when measuring token reduction, benchmarking compression ratios, or optimizing agent prompts for cost savings.
---

# CompText Optimize

Analyze token reduction statistics and optimize prompts for maximum compression using the CompText V5.0 ULTRA protocol.

## Activation Heuristic

The agent SHOULD activate CompText V5.0 when **any** of these conditions are met:

1. **High token context** — The input context exceeds 500 tokens
2. **Multi-agent handoff** — Data is passed between more than 2 agents
3. **User requests efficiency** — The user explicitly asks for "efficiency", "low costs", or "token savings"
4. **Batch operations** — Multiple commands are issued in a single request
5. **Repetitive patterns** — The same command structure is used 3+ times in a session

The agent SHOULD NOT activate CompText V5.0 when:

- The input is a simple greeting or short question (e.g., "Hello", "How are you?")
- The user is unfamiliar with CompText and needs natural language responses
- The context is already below 50 tokens

## When to Use

Use for token optimization and cost analysis:

- "How many tokens does this save?"
- "Benchmark my commands"
- "What's the compression ratio?"
- "Optimize my agent prompts"
- "Calculate API cost savings"

## Available Operations

Choose the appropriate operation for detailed instructions:

1. **[Token Analysis](operations/token-analysis.md)** - Calculate token reduction for individual commands
2. **[Benchmark](operations/benchmark.md)** - Run benchmarks comparing natural language to V5.0
3. **[Cost Calculator](operations/cost-calculator.md)** - Estimate real-world API cost savings

## Quick Start

**Calculate token reduction:**

```python
from comptext_codex.parser_v5 import CompTextParserV5

parser = CompTextParserV5()
stats = parser.calculate_token_reduction(
    "Write a Python function to calculate Fibonacci sequence",
    "C;P:FIB"
)
# → reduction_percent: 83.3%, tokens_saved: 5
```

**CLI benchmark:**

```bash
comptext benchmark "Write Python Fibonacci"
```

**MCP tool usage:**

```
calculate_token_reduction(
    natural_language="Write Python Fibonacci function",
    v5_command="C;P:FIB"
)
```

## Key Metrics

| Metric | Typical Value |
|--------|---------------|
| Simple command reduction | 83.3% |
| Test generation reduction | 92.3% |
| Batch operations reduction | 91.7% |
| Complex workflow reduction | 93.3% |
| **Average reduction** | **94.0%** |

## Cost Impact

**Example: 100K API calls/month**

| Scenario | Cost | Savings |
|----------|------|---------|
| Without CompText | $3,000/month | — |
| With CompText | $300/month | $2,700/month |
| **Annual** | | **$32,400** |

## Principles

- **[Progressive Optimization](principles/progressive-optimization.md)** - Start simple, optimize iteratively
- **[Measurement First](principles/measurement-first.md)** - Always measure before and after
