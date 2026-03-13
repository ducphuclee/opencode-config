---
name: get-api-docs
description: Retrieve accurate API documentation before writing code. Always query chub first, fallback to context7. Never rely on training knowledge for API shapes.
allowed-tools: ["Bash"]
---

# Get API Documentation (chub → context7 fallback)

When writing code that depends on a third-party library, SDK, or API, you must fetch the documentation first.

Never assume API signatures from training data.

Primary source: **chub**
Fallback source: **context7**

---

## Decision Flow

```
Search chub
     │
     ├─ Found + correct version → use chub docs
     │
     ├─ Found but version mismatch → fallback context7
     │
     └─ Not found → fallback context7
```

---

## Step 1 — Search documentation in chub

Always begin by searching the local registry.

```bash
chub search "<library name>" --json
```

Evaluate results:

* Identify the **best matching ID**
* Check whether the **version matches the user's requirement**

Possible outcomes:

### Case A — Matching documentation found

Proceed to Step 2.

### Case B — Version mismatch

Treat as **outdated documentation**.
Proceed to Step 3 (fallback).

### Case C — No documentation found

Proceed to Step 3 (fallback).

---

## Step 2 — Fetch documentation from chub

If a valid ID exists:

```bash
chub get <id> --lang py
```

or

```bash
chub get <id> --lang ts
```

Omit `--lang` if the document has only one language.

Guidelines:

* Only use API shapes that appear in the docs
* Do not guess missing parameters
* Prefer official examples from the document

After using the document, complete **Step 6 (feedback)**.

---

## Step 3 — Fallback to context7

If chub lacks the required documentation or version, use context7.

Query for **precise technical details**:

```
context7 query "
<library name> <version> API reference.

Return only:
- method signatures
- request/response schema
- authentication rules
- breaking changes
- minimal working code examples
"
```

Avoid retrieving long tutorials or blog-style content.

Extract only the information needed for implementation.

---

## Step 4 — Use the retrieved documentation

Use the documentation (from chub or context7) to write the code.

Rules:

* Follow the API exactly
* Use official method signatures
* Respect required headers, auth flows, and request bodies
* Never invent parameters

---

## Step 5 — Persist new knowledge (critical)

If you used **context7**, save the most important discoveries to chub.

This ensures future sessions become smarter.

If an existing ID exists:

```bash
chub annotate <id> "vX update: <important change>"
```

Example:

```bash
chub annotate stripe/api "v15 webhook verification requires raw body"
```

If no ID exists, create a custom namespace:

```bash
chub annotate custom/<library> "<important API behavior>"
```

Example:

```bash
chub annotate custom/bun-http "server.listen now returns a Promise in Bun v1.1"
```

### Annotation Guidelines

Only annotate **high-value information**:

* breaking changes
* authentication requirements
* version-specific behavior
* undocumented constraints
* common implementation pitfalls

Avoid storing large text blocks.

Annotations should be **short, precise, and actionable**.

---

## Step 6 — Provide feedback (chub docs only)

If the documentation came from chub, rate its quality.

```bash
chub feedback <id> up
```

or

```bash
chub feedback <id> down --label outdated
```

Available labels:

```
outdated
inaccurate
incomplete
wrong-examples
wrong-version
poorly-structured
accurate
well-structured
helpful
good-examples
```

---

## Quick Reference

| Goal              | Command                                       |
| ----------------- | --------------------------------------------- |
| Search docs       | `chub search "nextjs"`                        |
| Fetch docs        | `chub get stripe/api --lang py`               |
| Save docs to file | `chub get anthropic/sdk --lang py -o docs.md` |
| Query fallback    | `context7 query "nextjs 15 api reference"`    |
| Add note          | `chub annotate stripe/api "needs raw body"`   |
| List notes        | `chub annotate --list`                        |
| Rate docs         | `chub feedback stripe/api up`                 |

---

## Core Principles

1. **Never write API code without documentation**
2. **Prefer chub over context7**
3. **Use context7 only as a fallback**
4. **Persist critical findings to chub**
5. **Never rely on training memory for API shapes**

## Additional Resources

- For detailed API patterns, see [reference.md](reference.md)
