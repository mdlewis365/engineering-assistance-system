# Validation Examples

## Computed Clean

The required variables are available, equations execute, requested outputs are present, unit validation is acceptable, and no blocking run-health issues are present. Governance may allow a computed result, while still requiring human review for high-risk categories.

## Computed With Failure

The deterministic calculation completes successfully, but the engineering design, condition, or selected candidate fails one or more criteria. This is an engineering failure result, not an MCM system failure.

## Partial

Some computation was possible, but required variables, outputs, unit validation, or equation execution were incomplete. The report must not certify the result.

## Needs Human Review

The workflow identifies risk, ambiguity, conflict, missing evidence, or unsupported selected-candidate status that requires human engineering review.

## Unsupported

The requested deterministic computation is outside current MCM capability. The report can provide qualitative guidance and explain the limitation.

## Error

The system encountered a computation or workflow error. The report should not present unsupported engineering conclusions.

## What Is Not Included

These examples are conceptual. They do not include raw MCM requests, private schemas, formulas, parser behavior, prompt text, or test fixtures.
