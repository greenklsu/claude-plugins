# QA Agent Plugin

General-purpose QA reviewer for code correctness, completeness, performance at scale, security, and clean code practices. Works with any project — no project-specific configuration required.

## Supported Languages

- Oracle SQL
- PL/SQL
- Oracle APEX
- Power BI (DAX / Power Query M)
- Python
- JavaScript

## Installation

1. Copy the `qa-agent/` folder to your `~/.claude/plugins/` directory
2. Add the following to your `~/.claude/settings.json` under `enabledPlugins`:
   ```json
   "qa-agent@local": true
   ```
3. Restart Claude Code or start a new session

## Usage

### Slash Command

Review a specific file:
```
/qacheck path/to/file.sql
```

Review code you just pasted in chat:
```
[paste your code]
/qacheck
```

### Auto-Trigger

The agent also activates when you say things like:
- "QA this"
- "Review the code"
- "Check this"
- "Is this safe to run?"

## What It Checks

| Category | What It Catches |
|----------|----------------|
| **Completeness** | Missing error handling, unhandled code paths, TODO placeholders, missing imports |
| **Robustness** | NULL/empty handling, boundary conditions, resource cleanup, exception specificity |
| **Logic & Correctness** | Wrong operators, division by zero, JOIN errors, off-by-one, unreachable code |
| **Performance at Scale** | Full table scans, correlated subqueries, memory issues, missing indexes |
| **Security** | SQL injection, XSS, hardcoded secrets, unsafe deserialization, path traversal |
| **Clean Code** | Magic numbers, dead code, copy-paste duplication, naming inconsistency |
| **AI Anti-Patterns** | Hallucinated APIs, over-engineering, wrong comments, incomplete refactors |

## Output Format

Every review produces a structured report:

```
QA REVIEW
=========
Code:       [file or description]
Type:       [SQL / PL/SQL / Python / etc.]
Complexity: [Low / Medium / High]

Findings by Severity:
  Blocker: n    High: n    Medium: n    Low: n

--- FINDINGS ---
[SEVERITY] Line n: description
  Fix: corrected code

--- MINIMAL PATCHES ---
Corrected code for Blocker/High items

--- PERFORMANCE NOTES ---
Index suggestions, optimization notes

--- VALIDATION STEPS ---
SQL checks, test commands, reconciliation steps

QA complete.
```

## Important Notes

- The agent is **read-only** — it never modifies your files
- It does **not** add features or redesign code — it only finds and fixes defects
- Review depth scales to code complexity (a 5-line query gets a quick check, a 200-line procedure gets the full treatment)
- Assumes **production scale** unless told otherwise

## Author

Kyle Green
