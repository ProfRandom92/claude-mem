# Progressive Optimization

Start with natural language, compress incrementally.

## Principle

Don't try to compress everything at once. Follow this progression:

1. **Write naturally first** — Get the logic right
2. **Identify repeating patterns** — Find commands you use often
3. **Encode frequent commands** — Convert the most-used patterns to V5
4. **Batch related operations** — Group sequential commands
5. **Measure and iterate** — Use benchmarks to track improvement

## Example Progression

### Step 1: Natural Language

```
"Write a Python function to calculate Fibonacci"
"Generate unit tests for the Fibonacci function"
"Document the Fibonacci module"
```

### Step 2: Identify Pattern

All three commands target the same task (FIB) with different actions.

### Step 3: Encode Individually

```
C;P:FIB
T;P:FIB
D:FIB
```

### Step 4: Batch

```
B:[C;P:FIB]|[T;P:FIB]|[D:FIB]
```

### Step 5: Measure

```
Before: 3 calls × ~8 tokens = ~24 tokens
After:  1 call × ~1 token = ~1 token
Savings: 95.8%
```

## When NOT to Optimize

- One-off commands (not worth memorizing)
- Complex context that doesn't map to command vocabulary
- Commands to humans (readability matters more)
