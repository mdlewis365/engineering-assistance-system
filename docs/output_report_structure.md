# Output Report Structure

## Engineering Assistance System (EAS)

The **Engineering Assistance System (EAS)** produces structured **Engineering Advisory Reports** rather than unstructured chatbot responses.

The report structure is designed to make EAS output more reviewable, traceable, and useful for engineering work. It helps separate the user’s problem, known inputs, assumptions, deterministic computation, unit validation, constraint results, warnings, recommendations, and human-review status.

The guiding principle is:

> AI-assisted engineering output should be structured enough for review, not merely fluent enough to sound correct.

---

## 1. Purpose of the Engineering Advisory Report

The Engineering Advisory Report is the final user-facing artifact produced by EAS.

Its purpose is to communicate:

* What problem was analyzed
* Which engineering mode was submitted
* Which engineering pack was selected
* What inputs were used
* What assumptions were made
* What information was missing
* What calculations were performed, when applicable
* What constraints passed or failed
* What warnings or limitations apply
* What recommendation is being made
* Whether human review is required

The report is intended to support engineering reasoning and review. It is not a certification, professional engineering approval, or substitute for qualified judgment.

---

## 2. Report Design Goals

EAS report structure is based on several design goals.

### 2.1 Traceability

The report should make it clear how the advisory result was reached.

This includes showing the submitted mode, selected domain pack, known inputs, assumptions, computation summary, constraint results, and governance status.

### 2.2 Reviewability

The report should be easy for a human engineer, reviewer, or technical stakeholder to inspect.

Important details should not be hidden inside long narrative paragraphs.

### 2.3 Separation of Reasoning and Computation

Where deterministic computation is used, the report should distinguish computed results from qualitative reasoning or advisory interpretation.

### 2.4 Explicit Assumptions

Assumptions should be listed clearly.

Engineering assumptions should not be silently embedded in the recommendation.

### 2.5 Explicit Human-Review Status

The report should state whether human review is required.

This helps prevent advisory output from being mistaken for final approval.

---

## 3. Standard Report Sections

A typical EAS Engineering Advisory Report may include the following sections:

```text id="60z60d"
1. Report Header
2. Problem Summary
3. Submitted Engineering Mode
4. Selected Engineering Pack
5. Known Inputs
6. Missing Information
7. Assumptions
8. Computation Summary
9. Unit Validation Notes
10. Constraint Results
11. Recommendation
12. Risks and Limitations
13. Governance Status
14. Human Review Status
15. Suggested Next Validation Steps
```

Not every report requires every section. The final structure may vary depending on the submitted engineering mode, selected pack, available information, and whether deterministic computation was applicable.

---

## 4. Report Header

The report header identifies the artifact as an EAS advisory output.

Example:

```text id="ii0fgv"
Engineering Advisory Report
System: Engineering Assistance System (EAS)
Report Type: Design Review
Status: computed_with_failure
Human Review: Required
```

The header gives the reader an immediate understanding of the report type and review posture.

---

## 5. Problem Summary

The problem summary restates the engineering request in concise form.

Example:

```text id="s60c1v"
Problem Summary:
The user requested a review of a conveyor drive design to determine whether
the proposed motor, gear ratio, and pulley diameter satisfy the required
belt speed range.
```

The purpose of this section is to confirm what EAS understood the task to be.

---

## 6. Submitted Engineering Mode

A mode is submitted with every EAS request.

If the engineer does not manually select a mode, the submitted mode defaults to **Solve Problem**.

Public-facing modes include:

```text id="c1fcme"
Solve Problem
Diagnose Root Cause
Review Design
Suggest Improvements
Explore Novel Solution
```

Example:

```text id="m8f4ph"
Submitted Engineering Mode:
Review Design
```

The submitted mode frames the report structure and governance interpretation.

For example, **Review Design** emphasizes constraints and pass/fail results, while **Diagnose Root Cause** emphasizes symptoms, likely causes, evidence, and recommended checks.

---

## 7. Selected Engineering Pack

The selected engineering pack identifies the technical context used for the report.

Current public-safe EAS packs include:

```text id="2zh80o"
Industrial Exhaust / Airflow
DC Controls / Power
Compressed Air / Pneumatics
Fluid Pump Loop
Structural / Mechanical Bracket
Thermal Enclosure Cooling
Aerospace Preliminary Design
Aerospace Aerodynamics
Mechanical Power Transmission
Software Systems Engineering
```

Example:

```text id="8zf0dl"
Selected Engineering Pack:
Mechanical Power Transmission
```

The selected pack helps determine expected variables, likely calculations, relevant constraints, warnings, and report emphasis.

---

## 8. Known Inputs

The known-inputs section lists the values, facts, constraints, or system details provided by the user.

Example:

```text id="rv6uhv"
Known Inputs:
- Motor speed: 1,750 rpm
- Gear ratio: 20:1
- Drive pulley diameter: 2.67 in
- Required belt speed range: 75–85 ft/min
- Motor horsepower: 0.5 hp
```

Known inputs should include units whenever possible.

This section helps the reader verify what the advisory report is based on.

---

## 9. Missing Information

The missing-information section identifies values or context that were not provided but may affect the result.

Example:

```text id="cztudp"
Missing Information:
- Service factor was not provided.
- Startup torque requirement was not provided.
- Duty cycle was not provided.
- Manufacturer drive derating data was not provided.
```

This section is important because missing information can change the reliability of the recommendation.

If missing information is critical, the Governance Gate may produce `computed_with_warnings` or `needs_human_review`.

---

## 10. Assumptions

The assumptions section lists any assumptions used to complete the advisory workflow.

Example:

```text id="8g7d2c"
Assumptions:
- Gear ratio is interpreted as motor speed divided by output shaft speed.
- Pulley diameter is the effective pitch diameter.
- Belt slip is neglected for the preliminary calculation.
- Required belt speed range is treated as a hard design constraint.
```

Assumptions should be stated explicitly and should not be hidden in the recommendation.

When assumptions materially affect the result, they may trigger warnings or human-review requirements.

---

## 11. Computation Summary

The computation summary explains deterministic calculations performed by the Deterministic Computation Layer or Math Computation Module (MCM), when applicable.

Example:

```text id="o8e2h1"
Computation Summary:
- Output shaft speed = motor speed / gear ratio
- Output shaft speed = 1,750 rpm / 20
- Output shaft speed = 87.5 rpm

- Belt speed was computed from pulley diameter and shaft speed.
- Computed belt speed = 61.09 ft/min
```

The purpose of this section is not to expose private implementation details. It is to summarize what was computed and why it matters.

Some reports, especially software systems engineering or exploratory reports, may not require numeric deterministic computation.

---

## 12. Unit Validation Notes

The unit validation section identifies whether units were valid, missing, ambiguous, converted, or incompatible.

Example:

```text id="yeyog1"
Unit Validation Notes:
- Motor speed was provided in rpm.
- Pulley diameter was provided in inches.
- Belt speed was reported in ft/min.
- Unit conversion from inches to feet was required.
- No unit incompatibility was identified.
```

If unit validation fails, the report should make that visible.

Example:

```text id="hmnxuf"
Unit Validation Warning:
The constraint unit does not match the computed result unit. Human review is required before relying on this result.
```

Unit validation is central to EAS because engineering calculations are often invalid when units are missing or mismatched.

---

## 13. Constraint Results

The constraint-results section summarizes pass/fail checks.

Example:

```text id="xy7iei"
Constraint Results:

| Constraint | Computed Value | Requirement | Result |
|---|---:|---:|---|
| Belt speed | 61.09 ft/min | 75–85 ft/min | Fail |
| Horsepower | 0.5 hp available | Requirement not exceeded | Pass |
```

This section is especially important for **Review Design** mode.

A completed computation does not necessarily mean the design passed. The report should clearly distinguish computed values from constraint results.

---

## 14. Candidate Option Results

Some reports involve comparing multiple candidate options.

Example:

```text id="ehfblh"
Candidate Option Results:

| Option | Result | Reason |
|---|---|---|
| Option A | Rejected | Fails pressure requirement. |
| Option B | Selected | Lowest-cost option satisfying all required constraints. |
| Option C | Passing alternative | Satisfies constraints but costs more than Option B. |
```

This section is useful when the Governance Gate assigns `computed_selection_pass`.

---

## 15. Recommendation

The recommendation section provides the advisory conclusion.

Example:

```text id="efylb5"
Recommendation:
The proposed conveyor drive configuration should be rejected for the stated
belt-speed requirement because the computed belt speed is below the required
75–85 ft/min range.

A revised gear ratio, larger pulley, or different drive configuration should
be evaluated.
```

The recommendation should be consistent with the computation, constraint results, warnings, and governance status.

If the result requires human review, the recommendation should not be framed as final approval.

---

## 16. Risks and Limitations

The risks-and-limitations section identifies caution areas.

Example:

```text id="xoo60l"
Risks and Limitations:
- Belt slip was not modeled.
- Startup torque was not provided.
- Service factor was not provided.
- Manufacturer drive ratings were not checked.
- The result is advisory and should not be treated as final machinery approval.
```

This section helps prevent overreliance on incomplete advisory output.

---

## 17. Governance Status

The governance status communicates the reliability posture of the report.

Public-facing governance statuses include:

```text id="2d4wkb"
computed_clean
computed_selection_pass
computed_with_warnings
computed_with_failure
needs_human_review
```

Example:

```text id="7gmmhs"
Governance Status:
computed_with_failure
```

The governance status is assigned after considering computation status, unit validation, constraint results, warnings, failures, safety context, and human-review triggers.

---

## 18. Human Review Status

The human-review section states whether qualified review is required.

Examples:

```text id="otnd7p"
Human Review:
Not Required
```

```text id="oiomjg"
Human Review:
Required
```

Human review may be required when:

* The request is safety-critical
* The system is regulated
* Units are invalid or ambiguous
* Required information is missing
* A computation is unsupported
* A design fails constraints
* The output affects real-world electrical, mechanical, structural, aerospace, software, production, or safety systems

Even when human review is marked “Not Required,” the EAS report remains advisory and should not be treated as certification or approval.

---

## 19. Suggested Next Validation Steps

The final section may recommend practical next steps.

Example:

```text id="a2v2oh"
Suggested Next Validation Steps:
1. Confirm pulley pitch diameter.
2. Confirm gear ratio interpretation.
3. Check service factor and startup torque.
4. Evaluate a revised gear ratio or pulley size.
5. Review the final drive selection with qualified personnel before deployment.
```

This section helps convert the report into an actionable engineering review path.

---

## 20. Mode-Specific Report Emphasis

Different submitted modes emphasize different sections.

| Submitted Mode             | Report Emphasis                                                                        |
| -------------------------- | -------------------------------------------------------------------------------------- |
| **Solve Problem**          | Known inputs, assumptions, computation summary, unit validation, result.               |
| **Diagnose Root Cause**    | Symptoms, likely causes, evidence, missing diagnostic information, recommended checks. |
| **Review Design**          | Constraints, pass/fail results, rejected options, recommendation, human-review status. |
| **Suggest Improvements**   | Current limitation, improvement options, tradeoffs, risks, validation steps.           |
| **Explore Novel Solution** | Concept, feasibility, assumptions, unknowns, risks, validation path.                   |

The report structure remains consistent, but the emphasis shifts based on the submitted mode.

---

## 21. Pack-Specific Report Emphasis

The selected engineering pack also affects the report.

Examples:

* **DC Controls / Power** reports may emphasize voltage drop, current loading, fuse suitability, and electrical review.
* **Fluid Pump Loop** reports may emphasize flow, pressure, head, pump/pipe selection, and rejected options.
* **Structural / Mechanical Bracket** reports may emphasize load, bending stress, deflection, material strength, and safety factor.
* **Thermal Enclosure Cooling** reports may emphasize heat load, cooling capacity, ambient conditions, and thermal margin.
* **Aerospace** reports may emphasize preliminary assumptions, feasibility, safety-of-flight concerns, and validation requirements.
* **Mechanical Power Transmission** reports may emphasize speed, torque, horsepower, gear ratio, service factor, and guarding/safety considerations.
* **Software Systems Engineering** reports may emphasize architecture, failure modes, logs, runtime behavior, observability, security, test coverage, deployment context, and validation steps.

This makes EAS reports more domain-specific and easier to review.

---

## 22. Example Report Skeleton

A public-safe EAS report skeleton may look like this:

```markdown id="euwmwf"
# Engineering Advisory Report

## Report Header
- System: Engineering Assistance System (EAS)
- Submitted Mode: Review Design
- Selected Pack: Mechanical Power Transmission
- Governance Status: computed_with_failure
- Human Review: Required

## Problem Summary
[Concise restatement of the engineering request.]

## Known Inputs
- [Input 1 with unit]
- [Input 2 with unit]
- [Input 3 with unit]

## Missing Information
- [Missing value or context]
- [Missing value or context]

## Assumptions
- [Assumption 1]
- [Assumption 2]

## Computation Summary
[Summary of deterministic calculations, if applicable.]

## Unit Validation Notes
[Unit checks, conversions, warnings, or assumptions.]

## Constraint Results
| Constraint | Computed / Observed Value | Requirement | Result |
|---|---:|---:|---|
| [Constraint] | [Value] | [Requirement] | [Pass/Fail] |

## Recommendation
[Advisory recommendation consistent with the computed and governed result.]

## Risks and Limitations
- [Risk or limitation]
- [Risk or limitation]

## Governance Status
[computed_clean / computed_selection_pass / computed_with_warnings / computed_with_failure / needs_human_review]

## Human Review Status
[Required / Not Required]

## Suggested Next Validation Steps
1. [Step 1]
2. [Step 2]
3. [Step 3]
```

---

## 23. Example Design-Review Report

A simplified public-safe example:

```markdown id="f1zctg"
# Engineering Advisory Report

## Report Header
- System: Engineering Assistance System (EAS)
- Submitted Mode: Review Design
- Selected Pack: Mechanical Power Transmission
- Governance Status: computed_with_failure
- Human Review: Required

## Problem Summary
The user requested a review of a conveyor drive design to determine whether
the proposed drive configuration satisfies the required belt speed range.

## Known Inputs
- Motor speed: 1,750 rpm
- Gear ratio: 20:1
- Pulley diameter: 2.67 in
- Required belt speed range: 75–85 ft/min

## Missing Information
- Service factor was not provided.
- Startup torque was not provided.
- Belt slip was not provided.

## Assumptions
- Gear ratio is interpreted as motor speed divided by output shaft speed.
- Pulley diameter is treated as effective pitch diameter.
- Belt slip is neglected for this preliminary review.

## Computation Summary
- Output shaft speed = 1,750 rpm / 20 = 87.5 rpm
- Computed belt speed = 61.09 ft/min

## Unit Validation Notes
- Pulley diameter was converted from inches to feet.
- Belt speed was evaluated in ft/min.
- No unit incompatibility was identified in the simplified calculation.

## Constraint Results
| Constraint | Computed Value | Requirement | Result |
|---|---:|---:|---|
| Belt speed | 61.09 ft/min | 75–85 ft/min | Fail |

## Recommendation
The proposed drive configuration should be rejected for the stated belt-speed
requirement because the computed belt speed is below the required range.

A revised gear ratio, larger pulley, or different drive configuration should
be evaluated.

## Risks and Limitations
- Belt slip was not modeled.
- Startup torque was not provided.
- Service factor was not provided.
- Manufacturer drive ratings were not checked.

## Governance Status
computed_with_failure

## Human Review Status
Required

## Suggested Next Validation Steps
1. Confirm pulley pitch diameter.
2. Confirm gear ratio interpretation.
3. Determine required startup torque and service factor.
4. Evaluate revised drive configurations.
5. Review final machinery design with qualified personnel before deployment.
```

---

## 24. What the Report Does Not Represent

An EAS Engineering Advisory Report does not represent:

* Professional engineering certification
* Code-compliance approval
* Safety approval
* Regulatory approval
* Manufacturing release
* Construction approval
* Airworthiness approval
* Electrical installation approval
* Cybersecurity certification
* Final design authority

The report is an advisory artifact intended to support review and decision-making.

---

## 25. Public Repository Boundary

This document describes the public-safe structure of EAS Engineering Advisory Reports.

It does not include:

* Private report templates
* Source code
* Backend implementation
* Private prompts
* Activation prompts
* Prompt contracts
* Internal schemas
* Model-routing logic
* Raw engineering reports
* Operational logs
* Full MCM traces
* Internal governance rules
* Carter or Synthetic OS private internals

The purpose of this document is to explain the public-facing report structure without exposing proprietary implementation details.

---

## 26. Implementation Status Note

This document describes the public-facing design intent of EAS report structure.

Specific report sections, formatting, status wording, deterministic computation summaries, and mode-specific behavior should be validated against the private EAS implementation and test suite.

The public repository should avoid presenting untested behavior as a guaranteed implementation property.

---

## 27. Summary

The Engineering Advisory Report is the final structured output of EAS.

It is designed to communicate:

* What was asked
* What mode was submitted
* What pack was selected
* What inputs were used
* What assumptions were made
* What was computed
* What units were checked
* What constraints passed or failed
* What recommendation is being made
* What warnings or limitations apply
* What governance status was assigned
* Whether human review is required

The core belief is:

> Engineering AI output should be structured, traceable, unit-aware, constraint-aware, and explicit about human-review requirements.
