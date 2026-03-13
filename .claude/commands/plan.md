# /plan command

Create a task plan for implementation.

## Usage

```
/plan [feature description]
```

## Examples

```
/plan Implement user authentication with JWT
/plan Create a REST API for orders
/plan Add pagination to list endpoints
```

## Implementation

Delegates to @librarian agent to:
1. Analyze requirements
2. Break down into tasks
3. Define acceptance criteria
4. Set dependencies
5. Create task tracking

## Output

```markdown
## Plan: [Feature Name]

### Tasks
1. [TASK-001] Description
2. [TASK-002] Description

### Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2
```
