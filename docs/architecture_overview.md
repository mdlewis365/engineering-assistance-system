# Architecture Overview

## Purpose

EAS provides structured engineering advisory support inside Carter/Synthetic OS. It combines language-model planning, deterministic computation where appropriate, governance status classification, and human-review framing.

## Current Staged Workflow

1. Engineer submits a problem, optional supporting files, and a help mode.
2. EAS selects workflow guidance based on the requested mode and detected domain signals.
3. First stage analyzes the problem and produces a structured plan.
4. The plan is parsed, normalized, and validated.
5. If deterministic calculation is required, MCM runs the bounded computation.
6. MCM run health summarizes computation status, missing data, constraints, unit issues, screening, selection, or diagnostic outputs.
7. EDR stores compact decision-relevant summaries.
8. Governance Gate classifies the result and human-review requirement.
9. Evidence basis maps uploaded documents, computed values, assumptions, and limitations into user-facing reporting.
10. Second stage generates the final Engineering Advisory Report.
11. Report sanitation removes internal payloads and prevents overclaiming.

## What Is Not Included

This overview omits private prompts, exact structured-plan schemas, route names, source code, function names, model-routing details, raw file contents, raw logs, and proprietary governance internals.
