# /debug command

Debug issues in the codebase.

## Usage

```
/debug [error message or description]
```

## Examples

```
/debug "ImportError: No module named 'requests'"
/debug Why is the test failing?
/debug Trace this function: get_user_by_id
```

## Implementation

1. Search for error patterns in codebase
2. Check imports and dependencies
3. Trace function calls
4. Identify root cause
5. Suggest fixes

## Tools Used

- Grep for error patterns
- Glob for file discovery
- Read for code inspection
