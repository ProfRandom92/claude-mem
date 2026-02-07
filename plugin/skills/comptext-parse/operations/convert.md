# Convert Formats

Convert between CompText V5.0 ULTRA and V4.0 formats for backward compatibility.

## When to Use

- Working with systems that only support V4.0 format
- Migrating from V4.0 to V5.0
- Debugging by seeing the verbose V4 equivalent

## Methods

### Python API

```python
from comptext_codex.parser_v5 import CompTextParserV5

parser = CompTextParserV5()

# Parse V5 command
cmds = parser.parse("C;P:FIB")

# Convert to V4
v4_format = parser.to_v4_format(cmds[0])
# → 'CMD:CODE; LNG:PYTHON; TSK:FIB'
```

### MCP Tool

```
convert_v5_to_v4(v5_command="C;P:FIB")
```

**Response:**
```json
{
  "success": true,
  "v5_input": "C;P:FIB",
  "v4_output": ["CMD:CODE; LNG:PYTHON; TSK:FIB"],
  "count": 1
}
```

## Format Comparison

| Element | V5.0 | V4.0 |
|---------|------|------|
| Command | `C` | `CMD:CODE` |
| Language | `P` | `LNG:PYTHON` |
| Modifier | `R` | `STY:ROBUST` |
| Task | `:FIB` | `TSK:FIB` |
| Separator | `;` | `; ` |
| **Full** | `C;P:FIB` | `CMD:CODE; LNG:PYTHON; TSK:FIB` |

## Token Comparison

| Command | V5 Tokens | V4 Tokens | Savings |
|---------|-----------|-----------|---------|
| `C;P:FIB` | 1 | 5 | 80% |
| `T;P;R:FIB` | 1 | 7 | 86% |
| Batch of 3 | 1 | 15+ | 93%+ |

## Tips

1. Use V5 format for production (maximum compression)
2. Use V4 format for debugging (human-readable)
3. Conversion is lossless — all information is preserved
