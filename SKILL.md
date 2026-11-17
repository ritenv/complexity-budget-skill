---
name: complexity-budget
description: Evaluate whether the complexity of a software implementation is proportionate to its requirements and existing architecture. Use when reviewing implementation plans, pull requests, diffs, refactors, dependencies, or design alternatives for unnecessary complexity. Supports read-only audit mode by default and opt-in strict mode.
---

# Complexity Budget

Assess **complexity relative to value**, not raw line count. Preserve necessary complexity for security, correctness, reliability, accessibility, performance, and compatibility.

## Modes

- **Audit (default):** Read-only analysis. Do not modify files, block work, or assume approval authority. Report findings and suggested reductions.
- **Strict (only when explicitly requested):** Before introducing *material* complexity beyond the agreed budget, present alternatives, costs, and trade-offs; request user approval. This is an instruction-level checkpoint, not a guaranteed enforcement hook. Do not block routine or safety-critical changes.

## Inputs and evidence

Use the original request and acceptance criteria, constraints, current codebase conventions, proposed plan, and/or actual diff. Inspect available files, tests, dependency manifests, and call sites where tools permit. Never claim to have inspected or executed something you have not. If inputs are incomplete, state the limitation; do not invent architecture or metrics.

## Workflow

1. **Establish purpose:** Restate the requested outcome, quality constraints, anticipated lifetime, expected reuse, and known scale. Separate confirmed requirements from assumptions.
2. **Set a proportional budget:** Choose *small*, *moderate*, or *substantial* complexity tolerance based on the problem's risk, existing architecture, and expected evolution. Treat this as a qualitative guideline, not a universal numerical threshold. If user supplies an explicit budget, prioritize it unless it conflicts with necessary safeguards.
3. **Inventory complexity:** Identify added concepts, layers/abstractions, new dependencies, state, configuration, branching, operational requirements, data migrations, and new failure modes. Compare to the existing approach and realistic alternatives.
4. **Assess each material cost:** Label **Essential**, **Justified investment**, **Questionable**, or **Excessive** using `references/classification-guide.md`. Explain the concrete cost and benefit with evidence. Avoid treating file count or LOC as proof.
5. **Propose a minimum sufficient alternative:** Prefer existing conventions and the least complex design that meets all requirements. Explain trade-offs and any lost capabilities. Do not recommend deleting tests, validation, or safeguards solely to simplify.
6. **Report:** Produce a concise audit with an overall verdict, the top findings, and specific next actions. Explicitly distinguish observed facts from estimates and uncertainties.

## Report format

Use `templates/complexity-audit.md` as a guide. Include:

- Mode and scope reviewed
- Complexity budget and rationale
- Verdict: **Within budget**, **Near budget**, **Over budget**, or **Insufficient evidence**
- Material findings: component/change, classification, evidence, ongoing cost, recommendation
- Minimum sufficient alternative and trade-offs
- Unknowns / checks not performed

Do not fabricate numerical scores. If user asks for a score, explain the rubric and assumptions, and avoid false precision.

## Boundaries

- **Complexity is not scope creep:** A requested feature may still be unnecessarily complex; an unrequested change may be justified. Consider Scope Creep Detector separately if available.
- **Do not penalize useful abstraction automatically:** An abstraction is justified when actual reuse, variability, or isolation needs support it.
- **Do not optimize for shortest code:** Readability and maintainability matter.
- **Do not assume future needs:** Require evidence for speculative extensibility.
- **Never silently change code in audit mode.**

For detailed decision examples, read `references/classification-guide.md`.
