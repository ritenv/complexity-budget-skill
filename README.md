# Complexity Budget

A portable Agent Skill for ChatGPT and Claude that evaluates whether implementation complexity is proportionate to actual needs.

## Modes

- **Audit (default):** Read-only evaluation and recommendations.
- **Strict (opt-in):** Ask for approval before material complexity increases. This is instruction-based, not a technical enforcement guarantee.

## Use

Install the `complexity-budget` directory in your agent's supported skills location, or upload the skill through the agent's skill interface where supported. Exact installation methods depend on the product/version.

Examples:

- "Use Complexity Budget to audit this implementation plan."
- "Review this Git diff for unnecessary abstractions and operational complexity."
- "Use Complexity Budget in strict mode before implementing this feature."

## Structure

- `SKILL.md`: Skill metadata and main workflow
- `references/classification-guide.md`: Decision rubric and examples
- `templates/complexity-audit.md`: Suggested report format

## Important

The skill cannot inspect a repository or run commands without tool access. It should never imply that a plan or diff was inspected if it was not provided. The audit is not a security review, nor is a low line count a measure of quality.
