# Parse Commands

Parse CompText V5.0 ULTRA commands into structured format.

## When to Use

- Decoding a CompText command string
- Understanding what a compressed command means
- Extracting command, language, modifiers, and task from a V5 string

## Methods

### Python API

```python
from comptext_codex.parser_v5 import CompTextParserV5

parser = CompTextParserV5()

# Simple command
result = parser.parse("C;P:FIB")
print(result[0].command)    # 'C'
print(result[0].language)   # 'P'
print(result[0].task)       # 'FIB'

# Full name lookup
print(parser.COMMANDS[result[0].command])   # 'CODE'
print(parser.LANGUAGES[result[0].language]) # 'PYTHON'
```

### CLI

```bash
comptext parse "C;P:FIB"
# Output: Command: CODE, Language: PYTHON, Task: FIB

comptext parse "T;P;R:FIB"
# Output: Command: TEST, Language: PYTHON, Modifiers: [ROBUST], Task: FIB
```

### MCP Tool

```
parse_v5(command="C;P:FIB")
```

**Response:**
```json
{
  "success": true,
  "count": 1,
  "commands": [{
    "command": "CODE",
    "command_char": "C",
    "language": "PYTHON",
    "language_char": "P",
    "modifiers": [],
    "task": "FIB"
  }]
}
```

## Command Formats

| Format | Example | Description |
|--------|---------|-------------|
| `CMD:TASK` | `D:SUM` | Command + task only |
| `CMD;LANG:TASK` | `C;P:FIB` | Command + language + task |
| `CMD;LANG;MOD:TASK` | `T;P;R:FIB` | Command + language + modifier + task |

## Error Handling

- Unknown command chars are passed through as-is
- Missing task results in `task=None`
- Empty strings return empty list

## Tips

1. Use the CLI for quick one-off parsing
2. Use the Python API for programmatic access
3. Use the MCP tool for integration with agent workflows
