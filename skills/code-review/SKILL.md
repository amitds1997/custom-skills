---
name: quick-review
description:
  Use when you need a fast, structured, high-signal review of recent changes.
  Ideal before pushing, opening a pull request, merging to main, or anytime a
  developer asks to "review my code" or "check my changes." Combines correctness
  checks with code quality, maintainability, and best practice evaluation.
---

# Quick Code Review

Perform a focused, high-impact review of recently changed files.  
Prioritize correctness, safety, readability, maintainability, and architectural
soundness.

This acts as a lightweight pre-push / pre-PR quality gate.

---

## When to Use

- Developer asks for a code review
- After completing a feature or bug fix
- After refactoring existing logic
- Before pushing to a shared branch
- Before opening a pull request
- Before merging to main

---

## Review Goals

### 1. Correctness & Safety

- Catch bugs and logical errors
- Identify edge cases and missing validation
- Flag security risks and unsafe patterns
- Detect breaking changes
- Verify error handling paths
- Assess test coverage impact

### 2. Code Quality & Maintainability

- Evaluate naming clarity and consistency
- Check function size and single responsibility adherence
- Identify code duplication and DRY violations
- Flag overly complex logic
- Ensure proper separation of concerns
- Detect magic numbers and hardcoded values

### 3. Error Handling & Edge Cases

- Missing try/catch or improper error propagation
- Null/undefined handling
- Boundary conditions
- Empty states
- Invalid input handling

### 4. Readability & Structure

- Clear control flow
- Logical file organization
- Appropriate abstraction levels
- Avoid over-commenting obvious code
- Consistent style and formatting

### 5. Performance & Design

- Obvious performance inefficiencies
- Unnecessary re-computation
- Misused data structures
- Violations of SOLID principles
- Over-engineering or under-engineering

### 6. TypeScript Considerations (if applicable)

- Avoid `any` where possible
- Prefer explicit types
- Ensure proper narrowing and type safety
- Avoid unnecessary unused variable patterns
- Follow project-specific typing conventions

---

## Steps

### 1. Identify Changed Files

If reviewing the latest commit:

```bash
git diff --name-only HEAD~1
```

If on a feature branch:

```bash
git diff --name-only main...HEAD
```

### 2. Read Full Files

Read each changed file fully to understand context, not just the diff.  
Look for architectural side effects beyond modified lines.

### 3. Review the Diff Carefully

```bash
git diff HEAD~1
```

Focus on correctness first, then quality and maintainability.

---

## Output Format

**Summary:**  
Brief assessment of overall code quality and risk level.

---

**Critical Issues:**  
(Bugs, crashes, data corruption, security risks.)

- `file:line`
- What is wrong
- Why it matters
- Concrete fix (include improved code snippet when useful)

---

**Important Issues:**  
(Maintainability problems, missing edge cases, structural concerns.)

- `file:line`
- Explanation
- Recommended improvement

---

**Minor Issues:**  
(Readability, clarity, small improvements.)

- `file:line`
- Explanation
- Suggested refinement

---

**Positive Observations:**  
(Call out strong design choices, clean abstractions, good patterns.)

---

**Actionable Recommendations:**  
Prioritized next steps.

---

**Verdict:**

- APPROVE – Safe and clean
- REQUEST_CHANGES – Must fix before merge
- NEEDS_DISCUSSION – Architectural or design concern

---

## Enforcement Rules

- Be specific and actionable. No vague comments.
- Always reference exact file paths and line numbers.
- Distinguish clearly between bugs and suggestions.
- Do not invent issues.
- If the code is solid, say so clearly.
- If critical issues exist, default to REQUEST_CHANGES.
- Balance correctness with long-term maintainability.
