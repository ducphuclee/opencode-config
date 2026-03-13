# /validate command

Run full validation suite.

## Usage

```
/validate
```

## Examples

```
/validate                # Run full validation
```

## Implementation

Delegates to @checker agent to run:
1. Lint checks (ruff/flake8)
2. Type checks (mypy)
3. Tests (pytest)
4. Coverage report

## Gates

- Must pass all checks to continue
- Failures return to coder
- Success proceeds to reviewer

## Report

```
✅ Validation Passed
- lint: 0 issues
- typecheck: 0 errors
- tests: X/X passed
- coverage: XX%
```
