# Governance Gate

## Engineering Assistance System (EAS)

The **Governance Gate** is a core reliability and review layer within the Engineering Assistance System (EAS).

Its purpose is to evaluate the state of an engineering advisory workflow before the final Engineering Advisory Report is presented. The Governance Gate considers deterministic computation results, unit validation, constraint checks, warnings, failures, missing information, safety concerns, and human-review triggers.

The Governance Gate helps EAS avoid presenting every answer as equally reliable.

Instead, EAS distinguishes between:

* Clean computed results
* Computed results with warnings
* Failed or rejected designs
* Partial or unsupported computations
* Safety-sensitive results requiring human review
* Under-specified engineering problems

The guiding principle is:

> Engineering AI output should include not only an answer, but also a review status that communicates how the answer should be treated.

---

## 1. Purpose

The Governance Gate exists to reduce the risk of overconfident or unsupported engineering output.

In a purely generative workflow, a language model may produce an answer that appears confident even when:

* Required inputs are missing
* Units are ambiguous
* Calculations are unsupported
* A constraint failed
* A design is unsafe or incomplete
* The problem requires qualified human review
* The answer depends on assumptions that were not confirmed

The Governance Gate addresses this by evaluating the advisory workflow before final output.

It helps determine whether the result should be presented as:

* A clean computed advisory
* A computed advisory with warnings
* A failed design or rejected option
* A partial result
* A result requiring human review

---

## 2. Role in the EAS Architecture

At a public-safe level, the Governance Gate sits after deterministic computation and before final report generation.

```text id="hps9gk"
Engineer Input
    ↓
Engineering Mode Submission
    ↓
Domain Pack Selection
    ↓
LLM Planning Layer
    ↓
Deterministic Computation Layer / MCM
    ↓
Unit Validation
    ↓
Constraint Checking
    ↓
Governance Gate
    ↓
Engineering Advisory Report
    ↓
Human Review Status
```

The Governance Gate does not replace engineering judgment. It organizes the system’s internal evidence into a clear advisory status.

---

## 3. Inputs to the Governance Gate

The Governance Gate may consider several categories of information.

### 3.1 Submitted Engineering Mode

A mode is submitted with every EAS request.

Public-facing modes include:

```text id="sw4hlt"
Solve Problem
Diagnose Root Cause
Review Design
Suggest Improvements
Explore Novel Solution
```

If the engineer does not manually choose a mode, the submitted mode defaults to **Solve Problem**.

The submitted mode helps determine how the result should be evaluated. For example, **Review Design** mode emphasizes constraint pass/fail status, while **Explore Novel Solution** mode emphasizes feasibility, uncertainty, and validation requirements.

---

### 3.2 Domain Pack Context

The selected engineering domain pack provides technical context for the advisory workflow.

Examples include:

* DC controls and power
* Fluid pump loops
* Structural and mechanical brackets
* Thermal enclosure cooling
* Mechanical power transmission
* Aerospace preliminary design
* Aerospace aerodynamics

The Governance Gate may use the selected domain context to interpret whether the result is within expected scope, whether human review is appropriate, and whether the advisory report should include domain-specific limitations.

---

### 3.3 Deterministic Computation Status

The Governance Gate evaluates the status returned by the deterministic computation layer or Math Computation Module (MCM).

Public-facing computation statuses may include:

| Status                 | Meaning                                                                     |
| ---------------------- | --------------------------------------------------------------------------- |
| **computed**           | A deterministic computation was completed.                                  |
| **partial**            | Some computation was completed, but required values or checks were missing. |
| **unsupported**        | The requested calculation is outside the supported deterministic scope.     |
| **needs_human_review** | The computation or context requires qualified review before reliance.       |
| **error**              | A computation could not be completed due to invalid or inconsistent input.  |

These statuses help the Governance Gate determine whether the final report can be presented as computed, warning-bearing, failed, or human-review-required.

---

### 3.4 Unit Validation Results

Unit validation is a major governance input.

The Governance Gate may consider:

* Missing units
* Ambiguous units
* Incompatible units
* Unsupported conversions
* Invalid dimensional relationships
* Unit mismatch between computed result and constraint
* Unit assumptions that require confirmation

If unit validation fails or remains uncertain, the Governance Gate may generate warnings or require human review.

---

### 3.5 Constraint Results

Engineering design review often depends on explicit constraints.

Examples:

```text id="9al82k"
Voltage drop must be less than 5%.
Power supply loading must not exceed 80%.
Belt speed must be between 75 and 85 ft/min.
Tip deflection must be less than L/180.
Pump option must satisfy required flow and pressure.
```

The Governance Gate evaluates whether constraints passed, failed, were not evaluated, or were unsupported.

Constraint results may include:

* Pass
* Fail
* Warning
* Not evaluated
* Unsupported
* Requires human review

---

### 3.6 Warnings and Failure Conditions

The Governance Gate may receive warnings or failure conditions from earlier workflow stages.

Examples include:

* `missing_input`
* `missing_unit`
* `invalid_unit`
* `incompatible_units`
* `unsupported_equation`
* `unsupported_conversion`
* `constraint_failed`
* `no_passing_candidate`
* `ambiguous_value`
* `unsafe_assumption`
* `requires_human_review`

These warnings help determine whether the final advisory report should be clean, warning-bearing, failed, or escalated.

---

### 3.7 Safety and Review Triggers

Some requests require human review even if a computation appears successful.

Human review may be required when the request involves:

* Safety-critical systems
* Regulated engineering decisions
* Aerospace systems
* Electrical installations
* Pressure systems
* Lifting devices
* Structural supports
* Fire or life-safety systems
* Human-occupied spaces
* Manufacturing changes
* Physical deployment decisions
* Code compliance
* Certification or approval requests

The Governance Gate helps ensure that safety-sensitive outputs are not presented as final approvals.

---

## 4. Public-Facing Governance Statuses

The Governance Gate may assign a public-facing advisory status.

These statuses help communicate the reliability and review posture of the final Engineering Advisory Report.

| Governance Status           | Meaning                                                                                         |
| --------------------------- | ----------------------------------------------------------------------------------------------- |
| **computed_clean**          | Deterministic computation completed without required human-review flags or unresolved warnings. |
| **computed_selection_pass** | A valid selection was made among candidate options using computed constraints.                  |
| **computed_with_warnings**  | Computation completed, but warnings, assumptions, or limitations remain.                        |
| **computed_with_failure**   | One or more constraints failed, or the design/configuration was rejected.                       |
| **needs_human_review**      | The result requires qualified human review before reliance.                                     |

These statuses are advisory classifications. They are not certifications, approvals, or guarantees of safety.

---

## 5. Status Definitions

### 5.1 computed_clean

`computed_clean` indicates that deterministic computation was completed and no required human-review flags or unresolved warnings were identified.

This status may apply when:

* Required inputs were provided
* Units were valid
* Required calculations were supported
* Constraints passed
* No critical warnings were present
* No safety-critical escalation was required

Example:

```text id="q3fp5q"
Computation status: computed
Unit validation: pass
Constraint status: pass
Warnings: none
Human review required: false

Governance status: computed_clean
```

This does not mean the design is professionally certified. It means EAS completed the advisory workflow cleanly under the provided assumptions and supported scope.

---

### 5.2 computed_selection_pass

`computed_selection_pass` indicates that EAS evaluated multiple candidate options and selected a valid option based on computed constraints and selection criteria.

This status may apply when:

* Candidate options were provided
* Required constraints were evaluated
* At least one candidate passed
* A selection rule was applied
* The selected option satisfied required constraints

Example:

```text id="ntzj44"
Selection rule:
Select the lowest-cost candidate that satisfies all required constraints.

Candidate results:
- Option A: fails pressure requirement
- Option B: passes all constraints, cost $5,220
- Option C: passes all constraints, cost $5,700

Selected option:
Option B

Governance status: computed_selection_pass
```

This status is useful for engineering design-review workflows where EAS compares options rather than computing a single value.

---

### 5.3 computed_with_warnings

`computed_with_warnings` indicates that deterministic computation completed, but warnings, assumptions, limitations, or non-critical uncertainties remain.

This status may apply when:

* Some values were assumed
* Some units required interpretation
* A non-critical value was missing
* A calculation completed but depends on user-confirmed assumptions
* The result is advisory but not fully clean
* A constraint was checked but related context remains incomplete

Example:

```text id="tipxoc"
Computation status: computed
Unit validation: pass
Constraint status: pass
Warnings:
- Ambient temperature was assumed.
- Manufacturer derating data was not provided.

Governance status: computed_with_warnings
```

This status helps prevent a warning-bearing result from being presented as fully clean.

---

### 5.4 computed_with_failure

`computed_with_failure` indicates that computation completed and one or more required constraints failed, or that a proposed design/configuration was rejected.

This status may apply when:

* A computed value exceeds a limit
* A design fails a required constraint
* No candidate option satisfies all constraints
* A selected component is undersized
* A required speed, pressure, flow, stress, load, or capacity range is not met

Example:

```text id="txde94"
Computed belt speed: 61.09 ft/min
Required belt speed range: 75–85 ft/min
Constraint result: fail

Governance status: computed_with_failure
```

This status is important because a completed computation does not necessarily mean the design passed.

---

### 5.5 needs_human_review

`needs_human_review` indicates that the advisory result should not be relied on without qualified human review.

This status may apply when:

* Required information is missing
* Units are invalid or ambiguous
* The calculation is unsupported
* The problem is outside validated scope
* The result affects safety-critical systems
* The request involves regulated engineering requirements
* The LLM planning layer and deterministic layer disagree
* The result depends on assumptions that require professional confirmation
* The user appears to be asking for certification, approval, or final design authority

Example:

```text id="z65xv3"
Computation status: partial
Warnings:
- Material yield strength was not provided.
- Load case is incomplete.
- Structural design may affect real-world safety.

Governance status: needs_human_review
Human review required: true
```

This status is a protective feature of the EAS architecture.

---

## 6. Human Review Decision

In addition to a governance status, EAS may present a human-review decision.

Public-facing examples:

```text id="kkvu4p"
Human Review: Not Required
```

```text id="u8rhct"
Human Review: Required
```

The human-review decision communicates whether the advisory output should be treated as requiring qualified professional review before reliance.

Even when human review is marked “Not Required,” EAS output remains advisory and should not be treated as certification or approval.

---

## 7. Governance Decision Record

EAS may conceptually produce an engineering decision record that summarizes the basis for the governance result.

A public-safe decision record may include:

* Submitted engineering mode
* Selected domain pack
* Computation status
* Unit validation status
* Constraint status
* Warnings
* Failure conditions
* Human-review triggers
* Final governance status
* Human-review decision
* Short rationale

Example:

```text id="7tcvf7"
Submitted mode: Review Design
Selected domain pack: Mechanical Power Transmission
Computation status: computed
Unit validation: pass
Constraint status: fail
Failure condition: belt_speed_below_required_range
Governance status: computed_with_failure
Human review required: true
Rationale: The proposed design does not meet the required belt speed range.
```

This record improves traceability and helps the final report show how the advisory status was determined.

---

## 8. Governance and Engineering Modes

The selected or default-submitted engineering mode influences how the Governance Gate interprets the workflow.

| Mode                       | Governance Emphasis                                                                     |
| -------------------------- | --------------------------------------------------------------------------------------- |
| **Solve Problem**          | Whether the requested calculation completed cleanly and with valid units.               |
| **Diagnose Root Cause**    | Whether the diagnosis is evidence-supported and whether more measurements are required. |
| **Review Design**          | Whether constraints passed or failed.                                                   |
| **Suggest Improvements**   | Whether recommendations are advisory, computed, or require further validation.          |
| **Explore Novel Solution** | Whether feasibility is preliminary and what validation is required.                     |

For example, `computed_clean` in Solve Problem mode may mean a calculation completed cleanly. In Explore Novel Solution mode, a clean preliminary calculation does not mean the concept is validated for real-world use.

---

## 9. Governance and MCM

Within EAS, the Math Computation Module (MCM) provides deterministic computation evidence that the Governance Gate can evaluate.

MCM may provide:

* Computed values
* Unit validation results
* Constraint results
* Candidate option results
* Warnings
* Computation status
* Failure conditions

The Governance Gate interprets this evidence in the broader context of the submitted mode, selected domain pack, safety concerns, and report requirements.

MCM provides computational evidence. The Governance Gate provides advisory classification.

---

## 10. Governance and Final Report Generation

The Governance Gate affects how the final Engineering Advisory Report is written.

For example:

* A `computed_clean` result may be reported with a direct computed recommendation.
* A `computed_selection_pass` result may emphasize the selected option and rejected alternatives.
* A `computed_with_warnings` result may place warnings and assumptions prominently.
* A `computed_with_failure` result may clearly state that the design/configuration does not satisfy constraints.
* A `needs_human_review` result may avoid presenting the output as a final recommendation.

This helps ensure that the final report reflects the actual reliability posture of the workflow.

---

## 11. Examples

### 11.1 Clean Computed Result

```text id="6johku"
Request:
Calculate whether a power supply can support a 6 A load with an 8 A rating
and an 80% continuous loading limit.

Computation:
8 A × 0.80 = 6.4 A
6 A ≤ 6.4 A

Result:
Constraint passes.

Governance status:
computed_clean

Human Review:
Not Required
```

---

### 11.2 Selection Pass

```text id="nb4yxn"
Request:
Select the lowest-cost pump and pipe option that satisfies flow and pressure.

Candidate results:
- Option A: fails pressure
- Option B: passes flow and pressure, cost $5,220
- Option C: passes flow and pressure, cost $5,700

Result:
Option B is the lowest-cost passing option.

Governance status:
computed_selection_pass

Human Review:
Not Required, assuming input data and constraints are confirmed.
```

---

### 11.3 Computed with Warnings

```text id="q92wo5"
Request:
Estimate enclosure cooling requirement.

Computation:
Heat load estimate completed.

Warnings:
- Ambient temperature was assumed.
- Solar loading was not provided.
- Manufacturer derating data was not provided.

Governance status:
computed_with_warnings

Human Review:
Required if used for final thermal design.
```

---

### 11.4 Computed with Failure

```text id="5oepx0"
Request:
Review conveyor drive speed.

Computation:
Computed belt speed = 61.09 ft/min
Required belt speed range = 75–85 ft/min

Result:
Constraint fails.

Governance status:
computed_with_failure

Human Review:
Required before design change or deployment.
```

---

### 11.5 Needs Human Review

```text id="9k1efc"
Request:
Evaluate a structural bracket for real-world installation.

Warnings:
- Material yield strength missing.
- Load case incomplete.
- Safety factor not provided.
- Real-world structural installation may be safety-critical.

Governance status:
needs_human_review

Human Review:
Required
```

---

## 12. What the Governance Gate Does Not Do

The Governance Gate does not:

* Certify engineering designs
* Guarantee safety
* Replace a licensed professional engineer
* Verify code compliance
* Confirm that user-provided inputs are accurate
* Prove that all assumptions are valid
* Validate every possible engineering domain
* Eliminate the need for testing, inspection, or professional review

It provides advisory classification and review signaling within the limits of the EAS workflow.

---

## 13. Public Repository Boundary

This document describes the public-safe design intent of the EAS Governance Gate.

It does not include:

* Source code
* Internal governance logic
* Private prompts
* Activation prompts
* Prompt contracts
* Internal schemas
* Backend implementation
* Model-routing logic
* Full validation rules
* Operational logs
* Raw engineering reports
* Private engineering pack contents
* Carter or Synthetic OS private internals

The purpose of this document is to explain the role of governance in EAS without exposing proprietary implementation details.

---

## 14. Implementation Status Note

This document describes the public-facing architecture and design intent of the Governance Gate.

Specific status transitions, warning rules, human-review triggers, domain-specific policies, and implementation details should be validated against the private EAS implementation and test suite.

The public repository should avoid presenting untested behavior as a guaranteed implementation property.

---

## 15. Summary

The Governance Gate is a key reliability feature of EAS.

It helps transform engineering advisory output from a simple generated answer into a structured, reviewable result with explicit status signaling.

The Governance Gate evaluates:

* Submitted engineering mode
* Selected domain pack
* Deterministic computation status
* Unit validation results
* Constraint results
* Warnings
* Failures
* Safety concerns
* Human-review triggers

It then supports public-facing advisory statuses such as:

```text id="zbv3jt"
computed_clean
computed_selection_pass
computed_with_warnings
computed_with_failure
needs_human_review
```

This reflects a core EAS belief:

> AI-assisted engineering should clearly communicate not only what it recommends, but also whether the result is clean, warning-bearing, failed, or requires human review.
