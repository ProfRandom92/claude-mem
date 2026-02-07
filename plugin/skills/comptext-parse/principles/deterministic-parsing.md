# Deterministic Parsing

CompText V5.0 uses deterministic lookup tables instead of LLM interpretation.

## Core Principle

Every CompText command maps to exactly one meaning. There is no ambiguity:

```
C → CODE     (always)
P → PYTHON   (always)
R → ROBUST   (always)
```

## Why Deterministic Beats Probabilistic

| Aspect | Natural Language | CompText V5 |
|--------|-----------------|-------------|
| Interpretation | Probabilistic (LLM) | Deterministic (lookup) |
| Hallucination risk | Non-zero | Zero |
| Parsing speed | Variable | O(1) |
| Reproducibility | Approximate | Exact |

## Implementation

The parser uses simple dictionaries for mapping:

```python
COMMANDS = {'C': 'CODE', 'F': 'FIX', 'M': 'MODIFY', ...}
LANGUAGES = {'P': 'PYTHON', 'J': 'JAVASCRIPT', ...}
MODIFIERS = {'N': 'NO_COMMENTS', 'S': 'STRICT', ...}
```

No regex complexity, no NLP pipeline, no ML model — just dictionary lookups.

## Implications for Agent Teams

- Agents can exchange commands without misunderstanding
- No need to re-prompt when commands are misinterpreted
- Protocol is language-agnostic (same syntax works in any programming language)
- Backward compatibility is guaranteed (V4 conversion is lossless)
