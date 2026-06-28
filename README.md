# Engineering Assistance System

Engineering Assistance System (EAS) is a Carter/Synthetic OS workflow for structured engineering decision support.

This public repository is documentation only. It describes the implemented EAS architecture at a public-safe level without publishing private prompts, source code, model routing, schemas, route names, logs, or cloneable implementation details.

## What It Does

EAS helps an engineer frame a problem, provide supporting documents, choose a type of help, and receive an Engineering Advisory Report.

The current implementation supports a staged workflow:

1. Engineer input and optional supporting files.
2. First-stage engineering analysis that produces a structured computation or qualitative plan.
3. Strict parsing and validation of that plan.
4. Optional deterministic Math Computation Module (MCM) execution.
5. Engineering Decision Record (EDR), governance classification, run-health summary, and evidence basis.
6. Second-stage final Engineering Advisory Report.
7. Final report sanitation and human-review gating.

## Engineering Modes

- Solve the problem
- Diagnose root cause
- Review design
- Suggest improvements
- Explore novel solution

## Deterministic Computation

When a request requires bounded calculation, EAS can route a structured plan to MCM. MCM supports deterministic arithmetic, dependency-ordered equation plans, unit-aware outputs, constraint checks, selection or screening summaries, diagnostic summaries, and run-health reporting.

## Human Review

EAS is advisory. It does not replace licensed engineering review, safety review, code compliance review, commissioning, field verification, or domain expert judgment.

## What Is Not Included

This repository excludes private prompts, source code, backend routes, function names, authentication logic, model-routing internals, credentials, raw supporting documents, raw logs, raw job payloads, database schemas, proprietary governance logic, and implementation details that would allow cloning the system.

## Verification Without Source Code

Because the production implementation is proprietary, this repository verifies the system through architecture docs, sanitized examples, validation traces, screenshots, and public-safe workflow descriptions.
