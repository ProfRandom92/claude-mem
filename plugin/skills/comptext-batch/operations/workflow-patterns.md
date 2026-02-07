# Workflow Patterns

Common multi-step workflows using CompText V5.0 batch operations.

## When to Use

- Building standard development workflows
- Automating repetitive multi-step processes
- Creating reusable command patterns

## Standard Patterns

### Feature Development

Code → Test → Document a new feature.

```
B:[C;P:FEATURE]|[T;P:FEATURE]|[D:FEATURE]
```

### Bug Fix

Analyze → Fix → Test to verify.

```
B:[A:BUG]|[F;P:BUG]|[T;P:BUG]
```

### Code Review

Analyze → Explain → Document findings.

```
B:[A:CODE]|[E:CODE]|[D:CODE]
```

### Refactoring

Analyze → Optimize → Test → Document changes.

```
B:[A:MOD]|[O;P:MOD]|[T;P:MOD]|[D:MOD]
```

### Full Lifecycle

Code → Test → Optimize → Document.

```
B:[C;P:X]|[T;P:X]|[O;P:X]|[D:X]
```

### Multi-Language

Same task across different languages.

```
B:[C;P:API]|[C;J:API]|[C;T:API]
```

## Pattern Selection Guide

| Situation | Pattern | Commands |
|-----------|---------|----------|
| New feature | Feature Dev | C → T → D |
| Bug report | Bug Fix | A → F → T |
| PR review | Code Review | A → E → D |
| Performance issue | Refactoring | A → O → T → D |
| New module | Full Lifecycle | C → T → O → D |
| Cross-platform | Multi-Language | C(P) → C(J) → C(T) |

## Customizing Patterns

Add modifiers to any command in the batch:

```
B:[C;P;S:API]|[T;P;R:API]|[D:API]
```

This creates strict code + robust tests + documentation.

## Tips

1. Name your task consistently across the batch
2. Start with simpler patterns (3 commands) and expand
3. Test patterns with `parse` before executing
4. Reuse patterns across projects by keeping task names generic
