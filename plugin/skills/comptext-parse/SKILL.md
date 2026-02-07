---
name: comptext-parse
description: Parse and encode CompText V5.0 ULTRA commands. Use when working with compressed command syntax (e.g., "C;P:FIB"), converting between natural language and CompText protocol, or understanding command structures.
---

# CompText Parse

Parse, encode, and convert CompText V5.0 ULTRA commands. Works with the single-character compression protocol that reduces token usage by up to 94%.

## When to Use

Use when users work with CompText V5.0 ULTRA protocol:

- "Parse this CompText command"
- "Encode this into CompText format"
- "What does C;P:FIB mean?"
- "Convert this natural language to CompText"
- Converting between V5 and V4 formats

## Command Reference

### Single-Character Commands

| Char | Command | Description |
|------|---------|-------------|
| `C` | CODE | Generate code |
| `F` | FIX | Fix a bug |
| `M` | MODIFY | Modify existing code |
| `T` | TEST | Generate tests |
| `D` | DOCUMENT | Write documentation |
| `E` | EXPLAIN | Explain code/concept |
| `O` | OPTIMIZE | Optimize code |
| `A` | ANALYZE | Analyze structure |

### Language Codes

| Char | Language |
|------|----------|
| `P` | Python |
| `J` | JavaScript |
| `T` | TypeScript |
| `R` | Rust |
| `G` | Go |
| `S` | SQL |
| `H` | HTML |

### Modifiers

| Char | Modifier | Description |
|------|----------|-------------|
| `N` | NO_COMMENTS | Strip comments |
| `S` | STRICT | Strict mode |
| `R` | ROBUST | Robust error handling |
| `C` | CONCISE | Minimal output |

## Syntax

```
CMD;LANG:TASK           → Single command
CMD;LANG;MOD:TASK       → With modifier
B:[CMD1]|[CMD2]|[CMD3]  → Batch operations
```

## Available Operations

Choose the appropriate operation for detailed instructions:

1. **[Parse Commands](operations/parse.md)** - Parse V5.0 ULTRA commands into structured format
2. **[Encode Commands](operations/encode.md)** - Encode natural language into V5.0 format
3. **[Convert Formats](operations/convert.md)** - Convert between V5 and V4 formats

## Quick Examples

**Parse a command:**

```python
from comptext_codex.parser_v5 import CompTextParserV5

parser = CompTextParserV5()
result = parser.parse("C;P:FIB")
# → command='C' (CODE), language='P' (PYTHON), task='FIB'
```

**CLI usage:**

```bash
comptext parse "C;P:FIB"
# Output: Command: CODE, Language: PYTHON, Task: FIB
```

**MCP tool usage:**

```
parse_v5(command="C;P:FIB")
encode_v5(command="CODE", language="PYTHON", task="FIB")
```

## Principles

- **[Token Efficiency](principles/token-efficiency.md)** - Why CompText saves 94% tokens
- **[Deterministic Parsing](principles/deterministic-parsing.md)** - Zero-hallucination command mapping
