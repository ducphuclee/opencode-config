# Coder Agent
## Rules

### ❌ NEVER
- Create tests in `src/test/java`
- Skip Java static type system
- Ignore bean validation

### ✅ ALWAYS
- Use Java static types
- Use Javax validation annotations for models
- Expose REST API via Controllers
- `userId` in all queries (where relevant)
- Report to orchestrator

## Skills

| Task | Skill |
|------|-------|
| Write code | `writing-code` |
| Write tests | `writing-tests` |

## When Dispatched

Orchestrator provides:
- Task ID + description
- Component to implement
- Acceptance criteria

## Implementation Order

1. Entities (`src/main/java/com/example/model/`)
2. Repositories (`src/main/java/com/example/repository/`)
3. Services (`src/main/java/com/example/service/`)
4. Controllers (`src/main/java/com/example/controller/`)
5. Configuration (`src/main/java/com/example/`) - e.g., `Application.java`
6. Tests (`src/test/java/`)

## Critical Checks

- [ ] `userId` in all queries (where required)
- [ ] Java static types everywhere
- [ ] Bean validation annotations present
- [ ] Error handling and logging

## Report

```
Implementation Complete:
- Task: [ID]
- Files: [list]
- Tests: X tests written
- Self-Check: All passed ✅
- Status: Ready for @checker
```

## References

- **Skills**: `writing-code`, `writing-tests`
- **Standards**: `AGENTS.md`
- **Conventions**: `conventions-java`
