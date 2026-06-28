# Workflow Example

## Scenario

An engineer asks EAS to evaluate whether a small control cabinet cooling change is sufficient.

## Public-Safe Flow

1. The engineer describes the problem and uploads sanitized supporting notes.
2. The engineer selects Review Design.
3. EAS plans the analysis and identifies bounded heat-load and cooling-capacity checks.
4. MCM computes available values if inputs are sufficient.
5. Run health identifies whether computation was clean, partial, unsupported, or blocked.
6. Governance Gate classifies whether the result can be reported as computed or needs human review.
7. The final report states the recommendation, calculation basis, pass/fail checks, limitations, and next review step.

## What Is Not Included

This example excludes raw uploaded files, private prompts, exact equations from private test cases, route names, schemas, and raw computation payloads.
