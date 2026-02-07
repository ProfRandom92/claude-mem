# Token Analysis

Calculate token reduction statistics for individual commands.

## When to Use

- Measuring compression ratio for a specific command
- Comparing natural language vs CompText representation
- Understanding token savings per command type

## Methods

### Python API

```python
from comptext_codex.parser_v5 import CompTextParserV5

parser = CompTextParserV5()

stats = parser.calculate_token_reduction(
    "Write a Python function to calculate Fibonacci sequence",
    "C;P:FIB"
)

print(f"Natural tokens: {stats['natural_tokens']}")
print(f"V5 tokens: {stats['v5_tokens']}")
print(f"Tokens saved: {stats['tokens_saved']}")
print(f"Reduction: {stats['reduction_percent']}%")
print(f"Char reduction: {stats['char_reduction']}%")
```

### MCP Tool

```
calculate_token_reduction(
    natural_language="Write a Python function to calculate Fibonacci",
    v5_command="C;P:FIB"
)
```

**Response:**
```json
{
  "success": true,
  "statistics": {
    "natural_language": "Write a Python function to calculate Fibonacci",
    "natural_tokens": 7,
    "v5_command": "C;P:FIB",
    "v5_tokens": 1,
    "tokens_saved": 6,
    "reduction_percent": 85.7,
    "chars_natural": 47,
    "chars_v5": 7,
    "char_reduction": 85.1
  }
}
```

## Statistics Explained

| Field | Description |
|-------|-------------|
| `natural_tokens` | Estimated tokens in natural language (word count) |
| `v5_tokens` | Estimated tokens in V5 command (word count) |
| `tokens_saved` | Absolute token savings |
| `reduction_percent` | Percentage of tokens saved |
| `chars_natural` | Character count of natural language |
| `chars_v5` | Character count of V5 command |
| `char_reduction` | Percentage of characters saved |

## Tips

1. Token estimation uses word count (≈1 token per word)
2. Actual LLM tokenization may vary by model
3. Character reduction is more precise than token estimation
4. Use batch benchmarks for aggregate statistics
