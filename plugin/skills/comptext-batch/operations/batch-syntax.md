# Batch Syntax

Build CompText V5.0 ULTRA batch command strings.

## When to Use

- Combining multiple commands into a single call
- Creating multi-step workflows
- Reducing round-trips to the API

## Syntax

```
B:[CMD1;LANG:TASK]|[CMD2;LANG:TASK]|[CMD3:TASK]
```

### Elements

| Element | Symbol | Description |
|---------|--------|-------------|
| Batch prefix | `B:` | Marks the string as a batch |
| Command wrapper | `[...]` | Wraps each individual command |
| Separator | `\|` | Separates commands in the batch |

## Building a Batch

### Step 1: Write Individual Commands

```
C;P:FIB
T;P:FIB
D:FIB
```

### Step 2: Wrap in Brackets

```
[C;P:FIB]
[T;P:FIB]
[D:FIB]
```

### Step 3: Join with Pipes

```
[C;P:FIB]|[T;P:FIB]|[D:FIB]
```

### Step 4: Add Batch Prefix

```
B:[C;P:FIB]|[T;P:FIB]|[D:FIB]
```

## Python API

```python
from comptext_codex.parser_v5 import CompTextParserV5

parser = CompTextParserV5()

# Encode batch
batch = parser.encode_batch([
    ('CODE', 'PYTHON', None, 'FIB'),
    ('TEST', 'PYTHON', None, 'FIB'),
    ('DOCUMENT', None, None, 'FIB')
])
# → 'B:[C;P:FIB]|[T;P:FIB]|[D:FIB]'

# Parse batch
results = parser.parse(batch)
for cmd in results:
    print(f"{parser.COMMANDS[cmd.command]}: {cmd.task}")
# CODE: FIB
# TEST: FIB
# DOCUMENT: FIB
```

## Limits

- No maximum command count (practical limit: ~20 for readability)
- Commands execute in order (left to right)
- Each command in a batch is independent
- Nested batches are not supported

## Tips

1. Keep task names consistent across a batch
2. Order commands logically (code → test → document)
3. Use batch for related operations, not unrelated ones
