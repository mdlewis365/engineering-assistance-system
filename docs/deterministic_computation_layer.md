# Deterministic Computation Layer

## MCM Role

MCM means Math Computation Module. In EAS, it is used when an engineering request requires bounded deterministic calculation.

## Public Capabilities

The implemented MCM can publicly be described as supporting:

- direct arithmetic expression evaluation
- simple numeric operations
- dependency-ordered equation plans
- known formula handlers
- unit normalization and validation
- boolean and status outputs
- constraint checks and margins
- screening and selection summaries
- diagnostic summaries
- sensitivity summaries where requested and supported
- run-health summaries

## Status Outcomes

MCM can return statuses such as computed, partial, needs human review, unsupported, error, not required, or unknown depending on the computation plan and available data.

## Human Review Boundary

A computed MCM result is not a licensed engineering certification. It is a deterministic decision-support artifact that must be interpreted through the EAS Governance Gate and human review where appropriate.

## What Is Not Included

This document does not publish exact schemas, helper lists, formula code, unit tables, parser internals, private prompts, raw MCM payloads, or implementation details sufficient to reproduce MCM.
