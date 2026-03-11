# Dispatch Formats for Orchestrator

## To Librarian (Task Management)

```
Dispatch @librarian:
"Create task for login feature

Requirements:
- Feature: Login by email
- Scope: Domain layer only (LoginUseCase)
- AC: [list specific AC]

Check: Not a God Task, should be completable in 1-2 hours"
```

## To Coder

```
Dispatch @coder:
"Implement [TASK-ID]: [Title]

Layer: [domain|data|presentation]
Skills: done-workflow + done-conventions-critical + done-[layer]-layer

AC:
1. [AC1]
2. [AC2]

Follow TDD. Report when done."
```

## To Checker

```
Dispatch @checker:
"Validate [TASK-ID]

Run:
- flutter analyze
- dart format
- flutter test
- Convention check

Report: ✅ Passed or ❌ Failed"
```

## To Reviewer

```
Dispatch @reviewer:
"Review [feature]

Check: logic, conventions, edge cases, tests
Score: 1-10 (4 dimensions)
Report: ✅ APPROVED or ❌ NEEDS_FIX"
```

## To Explore

```
Dispatch @explore:
"Find all test files for login feature

Search in test/ folder for files matching login.*test.dart"
```
