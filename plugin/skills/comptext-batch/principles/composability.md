# Composability

Build complex workflows from simple, single-character commands.

## Principle

CompText V5.0 commands are composable by design. Each command is independent and can be combined with any other command in a batch without side effects.

## Why Composability Matters

### Simple Units

Each command does one thing:

```
C;P:FIB → Generate Python code for Fibonacci
T;P:FIB → Generate Python tests for Fibonacci
D:FIB   → Generate documentation for Fibonacci
```

### Compose Freely

Combine any commands in any order:

```
B:[C;P:FIB]|[T;P:FIB]|[D:FIB]     → Code + Test + Document
B:[A:FIB]|[O;P:FIB]|[T;P:FIB]     → Analyze + Optimize + Test
B:[E:FIB]|[D:FIB]                   → Explain + Document
```

### No Side Effects

- Commands don't depend on each other's output
- Removing a command from a batch doesn't break others
- Adding a command to a batch doesn't affect existing ones

## Design Implications

1. **Flat, not nested** — Batches are one level deep (no batch-of-batches)
2. **Order is semantic, not structural** — Commands run in order for logical flow, not dependency
3. **Uniform interface** — Every command follows `CMD;LANG:TASK` format
4. **Language mixing** — Different languages can appear in the same batch

## Anti-Patterns

- Don't create batches where commands depend on prior command output
- Don't use batch to replace conditional logic
- Don't create batches with unrelated tasks (group by feature/purpose)
