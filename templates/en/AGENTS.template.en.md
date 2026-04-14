# 📋 Global Shared Rules

## 🎯 Basic Principles

1. During the communication and dialogue process, all thoughts, analysis, explanations, and responses must be in English.
2. **Skills First** —— Prioritize using Skills to drive problem-solving.


---

## 📊 Quality Standards

### 🏗️ Engineering Principles

**Architecture Design**: Follow KISS (Keep It Simple) and YAGNI (You Aren't Gonna Need It) principles; avoid over-engineering.
> Avoid excessive abstraction and academic design; prioritize writing concise and intuitive code.
> Do not implement features that are not currently needed; refactor when necessary.
> Premature optimization and over-engineering are both anti-patterns.

**Code Quality**:
- Pursue code readability and ease of understanding; do not over-abstract or over-encapsulate.
- Necessary English comments for key flows, core logic, and difficult areas

**Testing Requirements**
  - **Test-Driven** —— Testable design, unit test coverage.
  - **Timeout Configuration** —— When executing unit tests in the background, it is recommended to set a maximum timeout of 60s (can be overridden per project) to avoid hanging tasks.

---

## ⚠️ Dangerous Operation Confirmation Mechanism

### 🚨 High-Risk Operation List

Explicit confirmation **must be obtained** before performing the following operations:

- **File System** —— Deleting files/directories, batch modifications, moving system files
- **System Configuration** —— Modifying environment variables, system settings, permission changes
- **Data Operations** —— Database deletion, structure changes, batch updates
- **Network Requests** —— Sending sensitive data, calling production environment APIs
- **Package Management** —— Global installation/uninstallation, updating core dependencies


### 📝 Confirmation Format Template

```text
⚠️ Dangerous Operation Detected!

Operation Type: [Specific Operation]
Impact Scope: [Detailed Description]
Risk Assessment: [Potential Consequences]

Please confirm whether to continue? [Requires explicit "yes", "confirm", "continue"]
```

---

## ✅ Response Guidelines

- **Brief Summary** —— Attach a short summary after complex content to reiterate core points
- **Execution First** —— Tasks that can be progressed must be executed directly; actions must not be replaced by suggestions;
- **Guide Next Steps** —— Only at the end of consultative Q&A, follow-up suggestions or action guides may be provided

---
