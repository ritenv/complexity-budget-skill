# Complexity classification guide

Classify *incremental complexity*, not the developer's competence or style.

| Class | Meaning | Typical example |
|---|---|---|
| Essential | Necessary to meet explicit requirements or protect correctness/security | Authorization check on an endpoint exposing private data |
| Justified investment | Not strictly required now, but has evidence-backed near-term value | Reusing the project's existing export helper rather than duplicating logic |
| Questionable | Benefit is speculative or costs are not explained | Adding a plugin architecture for a single fixed exporter |
| Excessive | Clearly disproportionate to requirements and existing conventions | Introducing a distributed job queue for a tiny synchronous local transformation without workload justification |

## Evidence prompts

- What requirement or observed constraint motivates the addition?
- Is there an existing simpler pattern in the repository?
- What new failure modes, ownership, configuration, or maintenance burden does it introduce?
- What would break or become harder if this addition were omitted?
- Is complexity shifted elsewhere (for example from application code into operations)?
- What evidence supports expected scale or reuse?

## Examples

### CSV export for a small table
- Add an export action and CSV escaping: **Essential**.
- Reuse an existing shared download utility: **Justified investment** when it fits.
- Add an export provider registry supporting six hypothetical formats: **Questionable**.
- Introduce a microservice and message broker for a small in-browser export: **Excessive**, unless specific scale or security requirements justify it.

### Authentication feature
- Secure password hashing, authorization, expiry validation, and tests: **Essential** even if they increase code size.
- Centralize repeated auth checks in an existing middleware convention: **Justified investment**.
- Create a generic policy DSL for two fixed roles: **Questionable**, absent evidence of broader policy needs.

### Mature system refactor
- More files may improve separation and ownership. Judge based on actual coupling, reliability, and migration risks, not file count.

## Handling uncertainty

If a cost or benefit depends on missing requirements, classify as **Questionable / needs evidence**, not **Excessive**. If no plan, diff, or architecture information is available, return **Insufficient evidence** and request the smallest missing input.
