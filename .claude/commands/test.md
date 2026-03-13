# /test command

Run tests for the current project.

## Usage

```
/test [pattern]
```

## Examples

```
/test                    # Run all tests
/test test_user.py       # Run specific test file
/test -k test_login      # Run tests matching pattern
```

## Implementation

Detect the test framework and run appropriate command:
- pytest: `pytest [pattern]`
- unittest: `python -m unittest [pattern]`

Always run linting first if available (ruff, flake8).
