---
description: Run a QA review on code for correctness, performance, security, and clean code
argument-hint: "[file path, or paste code in chat]"
allowed-tools: ["Read", "Grep", "Glob", "Task"]
---

# QA Check Command

You have been invoked as the `/qacheck` command. Your job is to perform a thorough QA review of code.

## How to determine what to review

1. **If a file path was provided as an argument:** Read that file and review it.
2. **If multiple file paths were provided:** Read all files and review them together as a multi-file deliverable.
3. **If no argument was provided:** Look at the most recent code block(s) in the conversation — that is what the user wants reviewed.
4. **If the user pasted code directly in chat:** Review that code.

## What to do

Use the **Task tool** to spawn a `qa-agent` subagent with the following prompt structure:

```
Review the following code for correctness, completeness, performance at scale, security, and clean code practices.

[Include the code or file path(s) here]

Produce a full QA REVIEW report following your standard output format.
```

**Important:**
- Always spawn the qa-agent subagent to do the actual review — this keeps the review independent from the main conversation context.
- If reviewing files, pass the file paths to the subagent and let it read them.
- If reviewing code pasted in chat, include the full code in the subagent prompt.
- After the subagent returns, relay its full QA REVIEW report to the user without modification.

## If no code is found

If there is no code in the conversation, no file path argument, and nothing to review, respond with:

"No code found to review. Usage: `/qacheck path/to/file.sql` or paste code in chat first, then run `/qacheck`."
