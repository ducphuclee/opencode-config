---
name: gitnexus
description: Code knowledge graph navigation for debugging, impact analysis, exploring code, and safe refactoring. Use gitnexus tools to understand your codebase.
allowed-tools: ["gitnexus_*"]
---

# GitNexus Knowledge Graph Navigation

GitNexus provides code knowledge graph tools for understanding, debugging, and refactoring your codebase.

---

## 1. Debugging with GitNexus

### When to Use
- "Why is this function failing?"
- "Trace where this error comes from"
- "Who calls this method?"
- "This endpoint returns 500"
- Investigating bugs, errors, or unexpected behavior

### Workflow

```
1. gitnexus_query({query: "<error or symptom>"})            → Find related execution flows
2. gitnexus_context({name: "<suspect>"})                    → See callers/callees/processes
3. READ gitnexus://repo/{name}/process/{name}                → Trace execution flow
4. gitnexus_cypher({query: "MATCH path..."})                 → Custom traces if needed
```

> If "Index is stale" → run `npx gitnexus analyze` in terminal.

### Checklist

```
- [ ] Understand the symptom (error message, unexpected behavior)
- [ ] gitnexus_query for error text or related code
- [ ] Identify the suspect function from returned processes
- [ ] gitnexus_context to see callers and callees
- [ ] Trace execution flow via process resource if applicable
- [ ] gitnexus_cypher for custom call chain traces if needed
- [ ] Read source files to confirm root cause
```

### Debugging Patterns

| Symptom | GitNexus Approach |
|---------|-------------------|
| Error message | `gitnexus_query` for error text → `context` on throw sites |
| Wrong return value | `context` on the function → trace callees for data flow |
| Intermittent failure | `context` → look for external calls, async deps |
| Performance issue | `context` → find symbols with many callers (hot paths) |
| Recent regression | `gitnexus_detect_changes` to see what your changes affect |

---

## 2. Impact Analysis with GitNexus

### When to Use
- "Is it safe to change this function?"
- "What will break if I modify X?"
- "Show me the blast radius"
- "Who uses this code?"
- Before making non-trivial code changes
- Before committing — to understand what your changes affect

### Workflow

```
1. gitnexus_impact({target: "X", direction: "upstream"})  → What depends on this
2. READ gitnexus://repo/{name}/processes                   → Check affected execution flows
3. gitnexus_detect_changes()                               → Map current git changes to affected flows
4. Assess risk and report to user
```

### Understanding Output

| Depth | Risk Level | Meaning |
|-------|-----------|---------|
| d=1 | **WILL BREAK** | Direct callers/importers |
| d=2 | LIKELY AFFECTED | Indirect dependencies |
| d=3 | MAY NEED TESTING | Transitive effects |

### Risk Assessment

| Affected | Risk |
|----------|------|
| <5 symbols, few processes | LOW |
| 5-15 symbols, 2-5 processes | MEDIUM |
| >15 symbols or many processes | HIGH |
| Critical path (auth, payments) | CRITICAL |

---

## 3. Exploring Codebase with GitNexus

### When to Use
- "How does X work?"
- "Find all places that do Y"
- "What code handles Z?"
- Understanding unfamiliar code
- Finding relevant files for a feature

### Workflow

```
1. gitnexus_query({query: "<concept>"})      → Find related processes
2. gitnexus_context({name: "<symbol>"})      → Get 360° view of a symbol
3. READ relevant files                        → Understand implementation
```

### Tools

**gitnexus_query** — semantic search:
```
gitnexus_query({query: "payment validation error"})
→ Processes: CheckoutFlow, ErrorHandling
→ Symbols: validatePayment, handlePaymentError, PaymentException
```

**gitnexus_context** — full context for a symbol:
```
gitnexus_context({name: "validatePayment"})
→ Incoming calls: processCheckout, webhookHandler
→ Outgoing calls: verifyCard, fetchRates
→ Processes: CheckoutFlow (step 3/7)
```

---

## 4. Safe Refactoring with GitNexus

### When to Use
- Renaming functions, classes, or variables
- Moving code between files
- Extracting methods
- Large-scale refactoring

### Workflow

```
1. gitnexus_impact({target: "X", direction: "upstream"})  → Check blast radius
2. gitnexus_rename({symbol_name: "old", new_name: "new"}) → Preview changes
3. Review d=1 items (WILL BREAK)
4. Make changes incrementally
5. gitnexus_detect_changes()                              → Verify impact
```

### Safety Rules

- **d=1 = WILL BREAK** — These must be updated
- **d=2 = LIKELY AFFECTED** — Review carefully
- **d=3 = MAY NEED TESTING** — Consider edge cases
- Always run tests after refactoring

---

## Cypher Query Examples

See [cypher-examples.md](cypher-examples.md) for common patterns.

### Basic Queries

**Find callers of a function:**
```cypher
MATCH (a)-[:CodeRelation {type: 'CALLS'}]->(b:Function {name: "validateUser"})
RETURN a.name, a.filePath
```

**Trace call chains:**
```cypher
MATCH path = (a)-[:CodeRelation {type: 'CALLS'}*1..3]->(b:Function {name: "target"})
RETURN [n IN nodes(path) | n.name] AS chain
```

**Find community members:**
```cypher
MATCH (f)-[:CodeRelation {type: 'MEMBER_OF'}]->(c:Community)
WHERE c.heuristicLabel = "Auth"
RETURN f.name
```

---

## Quick Reference

| Task | Primary Tool | Fallback |
|------|--------------|----------|
| Debug error | gitnexus_query | gitnexus_context |
| Check blast radius | gitnexus_impact | - |
| Explore codebase | gitnexus_query | gitnexus_cypher |
| Rename symbol | gitnexus_rename | Manual search |
| Check git changes | gitnexus_detect_changes | - |
| Custom traces | gitnexus_cypher | - |

---

## Additional Resources

- For detailed cypher patterns, see [cypher-examples.md](cypher-examples.md)
