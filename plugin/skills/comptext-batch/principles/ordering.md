# Ordering Matters

Why command sequence in a batch affects results.

## Principle

While CompText batch commands are technically independent, their **semantic order** matters for practical workflows. Place commands in the order you want them executed.

## Why Order Matters

### Logical Dependencies

Even though commands are structurally independent, workflows have natural sequences:

```
✅ B:[C;P:FIB]|[T;P:FIB]|[D:FIB]   → Code first, then test, then document
❌ B:[D:FIB]|[T;P:FIB]|[C;P:FIB]   → Document before code exists?
```

### Common Orderings

| Order | Rationale |
|-------|-----------|
| Code → Test | Test what you just wrote |
| Analyze → Fix | Understand before fixing |
| Analyze → Optimize | Understand before optimizing |
| Code → Test → Document | Full feature lifecycle |
| Analyze → Fix → Test | Bug fix lifecycle |

## Guidelines

1. **Create before verify** — Code/Fix before Test
2. **Understand before change** — Analyze before Fix/Optimize
3. **Change before document** — Code/Fix before Document
4. **Verify before document** — Test before Document (optional)

## Exceptions

- **Explain before Code** — When you need to understand a concept first
- **Document before Code** — When writing spec-first (TDD-like approach)
- **Analyze at any position** — Analysis is always useful

## Tips

1. Think of batch order as a narrative: "First X, then Y, finally Z"
2. If order doesn't matter, alphabetize for consistency
3. Put the most critical command first (if execution is interrupted, at least the first command runs)
