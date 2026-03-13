# /lint command

Run linting and code quality checks.

## Usage

```
/lint [path]
```

## Examples

```
/lint                    # Lint entire project
/lint src/               # Lint specific directory
/lint src/models/user.py # Lint specific file
```

## Implementation

Run linters in order:
1. ruff (preferred) or flake8
2. mypy for type checking
3. autofix if requested

## Commands

```bash
# Python
ruff check .
ruff format .
mypy .
```
