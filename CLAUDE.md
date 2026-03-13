# Project Configuration

This project uses a multi-agent workflow for development tasks.

## Active Agents

The following agents are configured for this project:

- **@orchestrator** - PO & Coordinator. Delegates tasks to specialist agents.
- **@solution-architector** - Solution architect for design decisions.
- **@coder1** - Python implementation (Primary).
- **@coder2** - Python implementation (Worker 1).
- **@coder3** - Python implementation (Worker 2).
- **@coder4** - Python implementation (Worker 3).
- **@coder5** - Python implementation (Worker 4).
- **@reviewer** - Senior Architect code review.
- **@checker** - QA Inspector (runs validation commands).
- **@explore** - Codebase Navigator.
- **@librarian** - Task & Knowledge Manager.

## Available Skills

Claude Code automatically loads these skills when relevant:

### Development Skills

- **/get-api-docs** - Retrieve accurate API documentation before writing code (chub → context7)
- **/gitnexus** - Code knowledge graph navigation (debug, impact analysis, explore, refactor)
- **/brainstorming** - Brainstorm ideas into designs before creative work
- **/writing-plans** - Create detailed implementation plans (bite-sized tasks)
- **/executing-plans** - Execute implementation plans task-by-task
- **/finish-branch** - Complete development work (merge, PR, cleanup)

### Skills Integrated into Agents

- **TDD** - Integrated in @coder (write failing test first, watch it fail, minimal code)
- **Verification** - Integrated in @checker (run all validations before marking complete)

## Workflow

```
Planning (@librarian)
    ↓
Implementation (@coder1-5)
    ↓
Validation (@checker)
    ↓
Review (@reviewer)
    ↓
Completion (@librarian)
```

## Gates (NEVER Skip)

1. After coder → MUST checker
2. After checker pass → MUST reviewer
3. After reviewer pass → MUST librarian

## MCP Tools

This project uses the following MCP tools:

- **ripgrep** - Fast file search using ripgrep
- **gitnexus** - Code knowledge graph navigation

## References

- **Standards**: `AGENTS.md`
