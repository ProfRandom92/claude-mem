# Pipeline Execution

Execute CompText V5.0 batch pipelines end-to-end.

## When to Use

- Running a complete batch pipeline from command string to results
- Integrating batch execution into automated workflows
- Using the MCP server for agent-to-agent communication

## Methods

### Python API

```python
from comptext_codex.parser_v5 import CompTextParserV5

parser = CompTextParserV5()

# Parse the batch
batch_str = "B:[C;P:FIB]|[T;P:FIB]|[D:FIB]"
commands = parser.parse(batch_str)

# Process each command
for cmd in commands:
    action = parser.COMMANDS.get(cmd.command, cmd.command)
    lang = parser.LANGUAGES.get(cmd.language, '') if cmd.language else ''
    print(f"Execute: {action} {lang} → {cmd.task}")
```

### MCP Pipeline

Step 1: Parse the batch

```
parse_v5(command="B:[C;P:FIB]|[T;P:FIB]|[D:FIB]")
```

Step 2: Execute each parsed command individually

Step 3: (Optional) Measure reduction

```
calculate_token_reduction(
    natural_language="Code Python Fibonacci, test Python Fibonacci, document Fibonacci",
    v5_command="B:[C;P:FIB]|[T;P:FIB]|[D:FIB]"
)
```

### CLI

```bash
# Parse batch to see individual commands
comptext parse "B:[C;P:FIB]|[T;P:FIB]|[D:FIB]"
```

## Error Handling

- Malformed brackets → Parser handles gracefully, strips outer brackets
- Unknown command chars → Passed through as-is
- Empty batch → Returns empty list

## Tips

1. Always parse before executing to validate syntax
2. Log each step for debugging multi-command pipelines
3. Use MCP `parse_v5` to validate batch strings before processing
4. Combine with `calculate_token_reduction` to measure savings
