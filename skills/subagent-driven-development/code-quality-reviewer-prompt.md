# Code Quality Reviewer Prompt Template

Use this template when dispatching a code quality reviewer subagent.

**Purpose:** Verify implementation is well-built (clean, tested, maintainable)

Do not re-review specification compliance. Assume spec compliance review already passed.

**Only dispatch after spec compliance review passes.**

```
Review pass input:

- What was implemented: [from implementer's report]
- Plan or requirements: [Task N full text or relevant requirements]
- Files changed: [list of changed files]
- Relevant diffs or code sections: [paste or summarize relevant changes]
- Task summary: [short summary]
```

**Code reviewer returns:** Strengths, Issues (Critical/Important/Minor), Assessment
