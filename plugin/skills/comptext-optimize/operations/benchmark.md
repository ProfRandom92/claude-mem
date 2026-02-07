# Benchmark

Run benchmarks comparing natural language to V5.0 ULTRA encoding.

## When to Use

- Evaluating compression across multiple command types
- Generating aggregate token reduction statistics
- Demonstrating CompText value to stakeholders

## Methods

### CLI

```bash
comptext benchmark "Write Python Fibonacci"
```

### MCP Tool

```
benchmark_v5(examples=[
    {"natural": "Write a Python function for Fibonacci", "v5": "C;P:FIB"},
    {"natural": "Generate unit tests for the Fibonacci function", "v5": "T;P:FIB"},
    {"natural": "Document the Fibonacci module", "v5": "D:FIB"},
    {"natural": "Optimize the SQL query for performance", "v5": "O;S:Q"},
    {"natural": "Analyze the project structure", "v5": "A:STRUCT"}
])
```

**Response:**
```json
{
  "success": true,
  "examples": [
    {"natural_tokens": 7, "v5_tokens": 1, "reduction_percent": 85.7},
    {"natural_tokens": 8, "v5_tokens": 1, "reduction_percent": 87.5},
    {"natural_tokens": 5, "v5_tokens": 1, "reduction_percent": 80.0},
    {"natural_tokens": 7, "v5_tokens": 1, "reduction_percent": 85.7},
    {"natural_tokens": 4, "v5_tokens": 1, "reduction_percent": 75.0}
  ],
  "aggregate": {
    "total_natural_tokens": 31,
    "total_v5_tokens": 5,
    "total_saved": 26,
    "average_reduction_percent": 83.9
  }
}
```

## Standard Benchmark Suite

Use these canonical examples for consistent benchmarking:

| Task | Natural Language | CompText V5 | Reduction |
|------|-----------------|-------------|-----------|
| Simple code | "Write Python Fibonacci" | `C;P:FIB` | 83.3% |
| Test generation | "Generate unit tests for Fibonacci" | `T;P:FIB` | 92.3% |
| Batch workflow | "Code, test, and document Fibonacci" | See below | 91.7% |
| Complex pipeline | "Analyze, fix memory, optimize SQL, document API" | See below | 93.3% |

**Batch workflow:** `B:[C;P:FIB]|[T;P:FIB]|[D:FIB]`

**Complex pipeline:** `B:[A:STRUCT]|[F;T:MEM]|[O;S:Q]|[D:API]`

## Tips

1. Include diverse command types for representative benchmarks
2. Use the aggregate statistics for cost projections
3. Run benchmarks before and after optimization for comparison
4. Store benchmark results for historical tracking
