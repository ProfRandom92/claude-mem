# Encode Commands

Encode natural language or structured commands into CompText V5.0 ULTRA format.

## When to Use

- Converting verbose prompts to compressed format
- Building CompText commands programmatically
- Reducing token overhead in agent-to-agent communication

## Methods

### Python API

```python
from comptext_codex.parser_v5 import CompTextParserV5

parser = CompTextParserV5()

# Simple encoding
result = parser.encode('CODE', 'PYTHON', task='FIB')
# → 'C;P:FIB'

# With modifiers
result = parser.encode('TEST', 'PYTHON', ['ROBUST'], 'FIB')
# → 'T;P;R:FIB'

# Task only (no language)
result = parser.encode('DOCUMENT', task='SUM')
# → 'D:SUM'
```

### CLI

```bash
comptext encode --command CODE --language PYTHON --task FIB
# Output: C;P:FIB
```

### MCP Tool

```
encode_v5(command="CODE", language="PYTHON", task="FIB")
```

**Response:**
```json
{
  "success": true,
  "v5_command": "C;P:FIB",
  "input": {
    "command": "CODE",
    "language": "PYTHON",
    "task": "FIB"
  }
}
```

## Parameters

| Parameter | Required | Values | Example |
|-----------|----------|--------|---------|
| command | Yes | CODE, FIX, MODIFY, TEST, DOCUMENT, EXPLAIN, OPTIMIZE, ANALYZE | `CODE` |
| language | No | PYTHON, JAVASCRIPT, TYPESCRIPT, RUST, GO, SQL, HTML | `PYTHON` |
| modifiers | No | NO_COMMENTS, STRICT, ROBUST, CONCISE | `['ROBUST']` |
| task | No | Any string identifier | `FIB` |

## Encoding Rules

1. Command is always first: `C;...`
2. Language follows command: `C;P;...`
3. Modifiers follow language: `C;P;R;...`
4. Task is separated by colon: `C;P:FIB`
5. Parts are separated by semicolons
6. Unknown values are silently skipped

## Tips

1. Use short task names for maximum compression (e.g., `FIB` not `FIBONACCI_SEQUENCE`)
2. Omit language when it's obvious from context
3. Combine with batch encoding for multi-step workflows
