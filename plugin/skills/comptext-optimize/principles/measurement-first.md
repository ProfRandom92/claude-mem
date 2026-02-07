# Measurement First

Always measure before and after optimization.

## Principle

Token reduction claims are only valid when measured. Use the built-in tools to quantify savings before committing to CompText for a workflow.

## Workflow

1. **Capture baseline** — Record your natural language prompts and their token counts
2. **Encode to CompText** — Convert prompts to V5 format
3. **Measure reduction** — Use `calculate_token_reduction` to get exact numbers
4. **Decide** — Only adopt CompText for commands with >50% reduction
5. **Track over time** — Use benchmarks to monitor ongoing savings

## Tools for Measurement

### Single Command

```python
parser.calculate_token_reduction(
    "Write a Python function for Fibonacci",
    "C;P:FIB"
)
```

### Batch Benchmark

```
benchmark_v5(examples=[...])
# Returns aggregate statistics
```

### CLI Quick Check

```bash
comptext benchmark "Your natural language prompt here"
```

## Red Flags

- Reduction below 50% — may not be worth the learning curve
- Task names longer than 5 chars — consider abbreviating
- Batch with only 1 command — no batch benefit, use single format
