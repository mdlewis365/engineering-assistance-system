# Output Report Structure

## Engineering Advisory Report

The final EAS output is an Engineering Advisory Report. For computed results, the public-safe report shape includes:

- title
- recommendation
- decision status
- evidence basis or source basis
- calculation basis
- key calculations
- pass/fail checks
- risks and limitations
- human review requirement when applicable
- immediate next step
- missing information that could materially change the answer

## Evidence Basis

The report should identify which supporting documents were used, which values were computed by MCM, which decision criteria were checked, and which assumptions or missing inputs affect certainty.

## Sanitation

The implementation includes final report cleanup that strips internal payloads, raw debug structures, provider/model disclosure lines, secrets, and unsupported overclaiming from normal user-facing reports.

## What Is Not Included

This document does not publish final prompt templates, raw JSON, hidden internal stages, model details, internal payload schemas, or raw EDR/governance objects.
