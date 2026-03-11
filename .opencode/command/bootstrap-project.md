---
description: Bootstrap project initialization
agent: build
model: github-copilot/gpt-4.1
---

**Purpose of this command:**
- To help users initialize a new project
- First, check if there's an existing codebase by verifying the presence of files: README.md, AGENTS.md, Claude.md
- If these files exist, automatically detect project details from them and modify the `.opencode/prompts/` folder accordingly without asking the user
- If it's a completely new project (no such files exist), ask users about the project's purpose, including:
  - Programming language (Python, TypeScript, Go, etc.)
  - Framework (FastAPI, Express, Django, React, etc.)
  - Database (PostgreSQL, MongoDB, MySQL, etc.)
  - Other technical requirements
- After gathering or detecting information, the chatbot will modify files in the `.opencode/prompts/` folder to meet the user's needs
- The current setup is configured for Python projects

**Workflow:**
1. Check: Check for existing codebase (README.md, AGENTS.md, Claude.md)
2. If exists: Auto-detect project details and modify prompts
3. If new: Ask user questions → Detect technical stack and requirements → Modify prompts