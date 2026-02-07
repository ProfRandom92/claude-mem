---
name: comptext-batch
description: Execute batch operations with CompText V5.0. Use when running multiple compressed commands together, building multi-step workflows, or orchestrating agent task pipelines.
---

# CompText Batch

Build and execute multi-command batch operations using CompText V5.0 ULTRA protocol. Process multiple commands in a single compressed call.

## When to Use

Use for multi-command workflows:

- "Run generate, test, and document together"
- "Build a batch pipeline"
- "Execute multiple CompText commands"
- "Create a workflow: code → test → document"

## Available Operations

Choose the appropriate operation for detailed instructions:

1. **[Batch Syntax](operations/batch-syntax.md)** - Build batch command strings
2. **[Workflow Patterns](operations/workflow-patterns.md)** - Common multi-step workflows
3. **[Pipeline Execution](operations/pipeline-execution.md)** - Execute batch pipelines end-to-end

## Syntax

```
B:[CMD1;LANG:TASK]|[CMD2;LANG:TASK]|[CMD3:TASK]
```

**Batch separator:** `|` (pipe)
**Command wrapper:** `[...]` (brackets)

## Quick Examples

**Generate + Test + Document:**

```
B:[C;P:FIB]|[T;P:FIB]|[D:FIB]
```

**Analyze + Fix + Optimize:**

```
B:[A:STRUCT]|[F;T:MEM]|[O;S:Q]|[D:API]
```

**Encode a batch in Python:**

```python
from comptext_codex.parser_v5 import CompTextParserV5

parser = CompTextParserV5()
batch = parser.encode_batch([
    ('DOCUMENT', None, None, 'SUM'),
    ('CODE', 'PYTHON', None, 'FIB'),
    ('EXPLAIN', None, ['CONCISE'], 'WHY')
])
# → 'B:[D:SUM]|[C;P:FIB]|[E;C:WHY]'
```

**MCP tool usage:**

```
encode_batch_v5(commands=[
    {"command": "CODE", "language": "PYTHON", "task": "FIB"},
    {"command": "TEST", "language": "PYTHON", "task": "FIB"},
    {"command": "DOCUMENT", "task": "FIB"}
])
```

## Common Workflows

| Workflow | CompText | Steps |
|----------|----------|-------|
| Full Feature | `B:[C;P:X]|[T;P:X]|[D:X]` | Code → Test → Document |
| Bug Fix | `B:[A:X]|[F;P:X]|[T;P:X]` | Analyze → Fix → Test |
| Refactor | `B:[A:X]|[O;P:X]|[T;P:X]` | Analyze → Optimize → Test |
| Review | `B:[A:X]|[E:X]|[D:X]` | Analyze → Explain → Document |

## Principles

- **[Composability](principles/composability.md)** - Build complex workflows from simple commands
- **[Ordering Matters](principles/ordering.md)** - Why command sequence affects results
