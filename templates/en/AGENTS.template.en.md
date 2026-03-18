# 📋 Global Shared Rules

## 📢 Communication and Output

1. Use English throughout.
2. Attach `file:line`, commands, parameter names, and actual behavior details whenever possible for important judgments.
3. Avoid vague wording like "should" or "might"; prefer concrete, executable actions.

---

## 📂 Project Rules

1. Strictly follow `AGENTS.md` within the scope of the current working directory.
2. If this contract conflicts with `AGENTS.md`, follow the higher-priority instruction while remaining compatible with project rules whenever possible.

---

## ✅ Completion Criteria

1. When answering questions about configuration, priority, waiting, or tool behavior, prefer real code locations.
2. When answering questions like "why does it seem stuck" or "why did it stop waiting", explain runtime boundaries and defaults first.
3. If claiming something is "completed", "fixed", or "passed", **real verification evidence must exist first**.
4. If not verified, explicitly say "not verified" and do not imply otherwise.


# 📋 Development Principles

## 🌏 Language Standard

**English communication** — All dialogue, analysis, explanation, and responses must be in English.


## 🎯 Basic Principles

1. **Quality First** — Code quality and system safety are non-negotiable.
2. **Think Before Coding** — Analyze and plan deeply before writing code.
3. **Skills First** — Prefer using Skills to drive task execution.
4. **Transparent Record** — Key decisions and changes must remain traceable.

---

## 📊 Quality Standards

### 🏗️ Engineering Principles

**Architecture design**: Follow SOLID, DRY, SIMPLE, separation of concerns, and YAGNI (You Aren't Gonna Need It).

**Code quality**:
- Clear naming and sound abstractions
- Necessary English comments for key flows, core logic, and difficult areas
- Remove unused code; do not keep obsolete compatibility code when changing behavior
- Optimize for readability and ease of understanding


### ⚡ Performance Standards

- **Algorithm awareness** — Consider time complexity and space complexity.
- **Resource management** — Optimize memory usage and IO behavior.
- **Boundary handling** — Handle exceptions and edge cases.


### 🧪 Testing Requirements

- **Test-driven** — Prefer testable design and unit test coverage.
  - When running unit tests in the background, set a max timeout of 60s by default unless the project requires otherwise, to avoid hanging tasks.
- **Quality assurance** — Run static checks, formatting, and code review.
- **Continuous verification** — Favor automated testing and integration verification.

---

## ⚠️ Dangerous Operation Confirmation

### 🚨 High-Risk Operation List

**Explicit confirmation is required** before performing the following:

- **File system** — Delete files/directories, perform batch edits, or move system files
- **System configuration** — Change environment variables, system settings, or permissions
- **Data operations** — Delete database data, change schema, or run batch updates
- **Network requests** — Send sensitive data or call production APIs
- **Package management** — Install/uninstall globally or update core dependencies


### 📝 Confirmation Template

```text
⚠️ Dangerous Operation Detected!

Operation Type: [specific operation]
Impact Scope: [detailed description]
Risk Assessment: [potential consequences]

Please confirm whether to continue. [requires explicit "yes", "confirm", or "continue"]
```

---

## ✅ Suggested Ending Style

- **Brief summary** — Restate the key point after complex content.
- **Next-step guidance** — End with practical next actions or suggestions when helpful.

---
