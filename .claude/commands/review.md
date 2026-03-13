# /review command

Request code review.

## Usage

```
/review [files or description]
```

## Examples

```
/review                  # Review recent changes
/review src/models/      # Review specific directory
/review PR #123          # Review pull request
```

## Implementation

Delegates to @reviewer agent to:
1. Check critical requirements
2. Score 4 dimensions
3. Provide actionable feedback
4. Approve or request changes

## Checklist

- User isolation
- Repository pattern
- Validation
- Type safety
- Tests

## Output

```
Code Review Report
Overall: X/10
Status: APPROVED / NEEDS_FIX
```
