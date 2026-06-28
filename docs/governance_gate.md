# Governance Gate

## Purpose

The EAS Governance Gate converts computation state, run health, risk classification, mode, and decision-record summaries into a bounded user-facing status.

It does not perform engineering calculations. It classifies how strong the final report is allowed to be.

## Public Status Families

- deterministic MCM not required
- computed criteria passed
- computed selected solution passed
- computed with failed criteria
- computed with unknowns
- computed screening pass
- computed screening found no viable option
- computed diagnostic result
- partial deterministic result
- needs human engineering review
- unsupported deterministic computation
- system error
- unknown status

## Human Review Triggers

Human review is required or emphasized when:

- risk is high
- deterministic computation is partial, unsupported, blocked, or errored
- selected-candidate status is unknown
- diagnostic evidence conflicts
- inputs are missing or ambiguous
- the decision affects safety, code compliance, regulated systems, or production risk

## What Is Not Included

This file does not disclose private risk keyword lists, exact decision logic, source code, schemas, route names, prompt text, or raw governance payloads.
