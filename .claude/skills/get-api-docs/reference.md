# Chub & Context7 Quick Reference

## Chub Commands

### Search
```bash
chub search "library name" --json
```

### Get Documentation
```bash
# With language
chub get <id> --lang py
chub get <id> --lang ts

# Without language
chub get <id>

# Save to file
chub get <id> -o docs.md
```

### Annotate
```bash
# Add note to existing
chub annotate <id> "vX update: change description"

# Create custom namespace
chub annotate custom/<library> "API behavior"

# List annotations
chub annotate --list
```

### Feedback
```bash
chub feedback <id> up
chub feedback <id> down --label outdated
```

## Context7 Commands

### Resolve Library ID
```
context7_resolve_library_id({
  libraryName: "library-name",
  query: "specific question"
})
```

### Query Documentation
```
context7_query_docs({
  libraryId: "/org/project",
  query: "specific question"
})
```

## Decision Flow

```
Search chub
     │
     ├─ Found + correct version → use chub docs
     │
     ├─ Found but version mismatch → fallback context7
     │
     └─ Not found → fallback context7
```

## Principles

1. **Never write API code without documentation**
2. **Prefer chub over context7**
3. **Use context7 only as a fallback**
4. **Persist critical findings to chub**
5. **Never rely on training memory for API shapes**
