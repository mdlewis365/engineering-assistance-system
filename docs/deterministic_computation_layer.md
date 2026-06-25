# Deterministic Computation Layer

## Engineering Assistance System (EAS)

The **Deterministic Computation Layer** is a core architectural component of the Engineering Assistance System (EAS).

Its purpose is to reduce unchecked reliance on language-model-generated numerical output by routing structured engineering calculations, unit-sensitive operations, constraint checks, and pass/fail evaluations through deterministic computation wherever possible.

Within the private EAS implementation, this deterministic capability is represented by the **Math Computation Module (MCM)**.

EAS uses language models for interpretation, planning, explanation, and advisory synthesis. However, when an engineering problem requires arithmetic, unit validation, constraint comparison, or option selection, EAS is designed to separate those operations from purely generative reasoning.

The guiding principle is:

> Language models can help reason about engineering problems, but engineering calculations should be deterministically checked whenever possible.

---

## 1. Purpose

The Deterministic Computation Layer exists to address a major risk in AI-assisted engineering:

> A language model may produce fluent, plausible, and well-formatted engineering calculations that are numerically wrong, dimensionally invalid, or unsupported by the provided inputs.

This layer helps EAS reduce that risk by providing a structured computation pathway for mathematical portions of an engineering advisory workflow.

The layer supports:

* Calculation checking
* Unit validation
* Unit conversion
* Constraint evaluation
* Pass/fail status generation
* Candidate option comparison
* Selection logic
* Warning generation
* Human-review escalation

The goal is not to eliminate the need for engineering judgment. The goal is to make AI-assisted engineering output more reviewable, traceable, and resistant to unchecked numerical hallucination.

---

## 2. Role in the EAS Architecture

At a high level, the Deterministic Computation Layer sits between the LLM planning layer and the governance gate.

```text
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
```

The LLM Planning Layer may identify what needs to be calculated. The Deterministic Computation Layer performs or validates the structured computation where possible. The Governance Gate then evaluates the result, warnings, failures, and human-review requirements before the final advisory report is produced.

---

## 3. Math Computation Module (MCM)

Within the private EAS implementation, the deterministic computation layer is represented by the **Math Computation Module (MCM)**.

MCM supports structured engineering calculations, unit-aware validation, constraint checking, pass/fail evaluation, candidate selection, and computed status generation where deterministic computation is possible.

In the EAS architecture, the language model may help interpret the engineering request, identify relevant variables, organize the workflow, and determine what calculations appear necessary. MCM provides a separate deterministic pathway for checking mathematical and unit-sensitive portions of that workflow.

This helps reduce reliance on unchecked language-model-generated numerical output.

Public-safe MCM responsibilities include:

* Receiving structured calculation inputs
* Handling known values and requested unknowns
* Supporting equation dependency ordering
* Performing supported deterministic calculations
* Checking unit compatibility
* Supporting unit conversions where available
* Evaluating engineering constraints
* Producing pass/fail results
* Supporting candidate option selection
* Returning computation statuses and warnings
* Escalating unsupported or unsafe cases to human review

MCM is not presented in this repository as open-source software. This repository describes MCM only at a conceptual level.

The following remain proprietary and are not included:

* MCM source code
* Parser implementation
* Internal schemas
* Private prompt contracts
* Equation handler implementation
* Unit-algebra implementation
* Internal helper functions
* Full validation logic
* Test harness details
* Operational traces
* Raw computation logs

---

## 4. Why Deterministic Computation Matters

Engineering workflows often depend on exact or bounded calculations.

Examples include:

* Voltage drop
* Power supply loading
* Pressure drop
* Pump flow requirements
* Belt speed
* Torque
* Horsepower
* Thermal load
* Airflow area
* Structural deflection
* Stress margin
* Candidate option cost comparison

For these tasks, a fluent explanation is not enough. The system must check whether the numbers, units, and constraints are coherent.

The Deterministic Computation Layer helps EAS answer questions such as:

* Were the required values provided?
* Are the units compatible?
* Can the calculation be performed?
* Does the result satisfy the constraint?
* Which candidate options pass?
* Which passing option is preferred?
* Are there warnings or missing assumptions?
* Should human review be required?

---

## 5. Public-Safe Capability Summary

At a public-safe level, the Deterministic Computation Layer and MCM may support the following capabilities.

### 5.1 Structured Variable Handling

The layer receives structured values rather than relying only on prose.

Example values may include:

```text
supply_voltage = 24 V
load_current = 6 A
wire_length = 40 ft
power_supply_rating = 8 A
voltage_drop_limit = 5 %
```

Structured values help make computation more repeatable and reviewable.

---

### 5.2 Equation Dependency Ordering

Some engineering problems require multiple calculations in sequence.

For example:

```text
Step 1: Calculate current draw.
Step 2: Calculate voltage drop.
Step 3: Calculate voltage drop percentage.
Step 4: Compare result against allowable limit.
```

The Deterministic Computation Layer may use dependency ordering to determine which values must be computed before later constraints can be evaluated.

---

### 5.3 Unit-Aware Calculation

Engineering calculations are unit-sensitive.

The Deterministic Computation Layer is designed to treat units as part of the computation rather than as informal labels.

Examples:

```text
ft to in
gpm to in³/min
hp to W
°C temperature difference to K-equivalent interval
ft/min belt speed
lb-ft torque
```

Unit-aware calculation reduces the chance that incompatible quantities are combined incorrectly.

---

### 5.4 Unit Conversion

Where supported, the layer may convert between compatible units.

Examples:

```text
feet ↔ inches
gallons ↔ cubic inches
watts ↔ horsepower
minutes ↔ seconds
psi ↔ pressure-related engineering quantities
```

Unsupported or ambiguous conversions may generate warnings or trigger human review.

---

### 5.5 Constraint Checking

Engineering design review often depends on constraints.

Examples:

```text
Voltage drop must be less than 5%.
Power supply loading must not exceed 80%.
Belt speed must be between 75 and 85 ft/min.
Tip deflection must be less than L/180.
Candidate option must satisfy required flow and pressure.
```

The Deterministic Computation Layer can compare computed values against constraints and return pass/fail results.

---

### 5.6 Candidate Option Evaluation

Some EAS workflows involve comparing multiple candidate designs or configurations.

Example:

```text
Option A: lower cost, fails pressure requirement
Option B: moderate cost, passes all constraints
Option C: higher cost, passes all constraints
```

The Deterministic Computation Layer may support computed selection logic such as:

```text
Select the lowest-cost option among candidates that pass all required constraints.
```

This helps EAS avoid selecting an option based only on language-model preference.

---

### 5.7 Warning and Failure Generation

The layer may produce warnings when computation is incomplete, uncertain, or partially unsupported.

Examples:

* Missing required input
* Missing unit
* Incompatible unit
* Unsupported conversion
* Constraint cannot be evaluated
* Candidate option is incomplete
* Computation depends on an assumption
* Result exceeds a limit
* No candidate option satisfies all constraints

Warnings are passed forward to the Governance Gate and final advisory report.

---

## 6. Example Calculation Flow

A simplified deterministic computation flow may look like this:

```text
Input:
Review a 24 VDC control circuit.

Known values:
- Supply voltage: 24 VDC
- Load current: 6 A
- Power supply rating: 8 A
- Continuous loading limit: 80%

Computation:
- Maximum recommended continuous load = 8 A × 0.80
- Maximum recommended continuous load = 6.4 A

Constraint:
- Load current must be less than or equal to 6.4 A

Result:
- 6 A ≤ 6.4 A
- Constraint passes

Governance implication:
- Power supply loading passes under the provided continuous-load limit.
```

This example illustrates the basic idea: EAS should not merely state that the power supply is acceptable. It should calculate the relevant value, compare it against the constraint, and report the result.

---

## 7. Example Candidate Selection Flow

A simplified candidate selection workflow may look like this:

```text
Input:
Select the lowest-cost pump and pipe configuration that satisfies all constraints.

Candidates:
- Option A: cost $4,800, fails pressure requirement
- Option B: cost $5,220, passes flow and pressure requirements
- Option C: cost $5,700, passes flow and pressure requirements

Selection rule:
- Select the lowest-cost option among passing candidates.

Computed result:
- Option B is selected because it is the lowest-cost passing option.

Rejected options:
- Option A is rejected because it fails the pressure requirement.
- Option C passes but is more expensive than Option B.
```

This type of workflow allows EAS to distinguish between a preferred option, rejected options, and alternatives that pass but are not optimal under the selected criterion.

---

## 8. Computation Statuses

The Deterministic Computation Layer may produce computation statuses that are later interpreted by the Governance Gate.

Public-facing examples include:

| Status                 | Meaning                                                                     |
| ---------------------- | --------------------------------------------------------------------------- |
| **computed**           | A deterministic computation was completed.                                  |
| **partial**            | Some computation was completed, but required values or checks were missing. |
| **unsupported**        | The requested calculation is outside the supported deterministic scope.     |
| **needs_human_review** | The computation or context requires qualified review before reliance.       |
| **error**              | A computation could not be completed due to invalid or inconsistent input.  |

These statuses are not necessarily the final advisory status. The Governance Gate may combine computation status, unit validation, constraint results, warnings, and safety triggers into a final report-level decision.

---

## 9. Relationship to Governance Status

The Deterministic Computation Layer provides computational evidence. The Governance Gate interprets that evidence.

For example:

```text
Deterministic computation status: computed
Constraint status: pass
Warnings: none
```

May lead to:

```text
Governance status: computed_clean
Human review required: false
```

Another example:

```text
Deterministic computation status: computed
Constraint status: fail
Warnings: design does not satisfy required speed range
```

May lead to:

```text
Governance status: computed_with_failure
Human review required: true or advisory-dependent
```

Another example:

```text
Deterministic computation status: partial
Warnings: missing material property and ambiguous units
```

May lead to:

```text
Governance status: needs_human_review
Human review required: true
```

This distinction is important. Computation is not the same thing as final approval.

---

## 10. Relationship to Engineering Modes

The Deterministic Computation Layer supports different engineering modes in different ways.

| Mode                       | Deterministic Computation Role                                         |
| -------------------------- | ---------------------------------------------------------------------- |
| **Solve Problem**          | Compute requested values from known inputs.                            |
| **Diagnose Root Cause**    | Check measurable relationships that may support or weaken a diagnosis. |
| **Review Design**          | Compare computed values against design constraints.                    |
| **Suggest Improvements**   | Quantify improvement margins or compare alternatives.                  |
| **Explore Novel Solution** | Perform early feasibility checks where sufficient data exists.         |

The layer is most directly applicable to calculation-heavy and constraint-heavy workflows, especially **Solve Problem** and **Review Design**. It may also support diagnostics, improvements, and exploratory concepts when measurable relationships are available.

---

## 11. Relationship to Engineering Packs

Engineering packs provide domain context. The Deterministic Computation Layer provides structured computation.

For example:

```text
Domain Pack: DC Controls / Power
Possible computations:
- Voltage drop
- Current loading
- Fuse sizing checks
- Power supply loading
```

```text
Domain Pack: Mechanical Power Transmission
Possible computations:
- Belt speed
- Shaft speed
- Torque
- Horsepower
```

```text
Domain Pack: Fluid Pump Loop
Possible computations:
- Flow
- Pressure
- Head
- Pump/pipe candidate comparison
```

The full private engineering pack contents and internal computation implementation are not included in this public repository.

---

## 12. Unit Validation and Human Review

Unit validation is one of the most important functions of the deterministic layer.

Human review may be required when:

* Units are missing
* Units are ambiguous
* Units are incompatible
* A conversion is unsupported
* A dimensional relationship is invalid
* A safety-critical calculation depends on assumed units
* A result appears numerically plausible but dimensionally questionable

EAS should not hide unit uncertainty. Unit problems should be surfaced in the advisory report.

---

## 13. Constraints and Pass/Fail Logic

Constraint checking allows EAS to produce more useful design-review outputs.

Examples:

```text
Computed belt speed: 61.09 ft/min
Required belt speed range: 75–85 ft/min
Constraint result: fail
```

```text
Computed power supply loading: 75%
Maximum recommended loading: 80%
Constraint result: pass
```

```text
Computed deflection: 0.08 in
Maximum allowed deflection: 0.10 in
Constraint result: pass
```

These comparisons allow EAS to explain not only the answer, but why the design passes or fails.

---

## 14. Warnings and Failure Conditions

The Deterministic Computation Layer may generate warnings or failure conditions such as:

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

These warnings help the Governance Gate determine whether the final advisory report should be clean, warning-bearing, failed, or human-review-required.

---

## 15. What the Layer Does Not Do

The Deterministic Computation Layer does not replace engineering judgment.

It does not:

* Certify a design
* Guarantee safety
* Verify code compliance
* Replace a licensed professional engineer
* Validate all possible engineering domains
* Prove that all assumptions are correct
* Guarantee that the LLM selected the correct equations
* Guarantee that the user-provided inputs are accurate
* Eliminate the need for testing, inspection, or professional review

It provides structured computation and validation support within the limits of the available inputs and supported calculation scope.

---

## 16. Public Repository Boundary

This document describes the public-safe design intent of the Deterministic Computation Layer and MCM.

It does not include:

* Source code
* Parser implementation
* Internal schemas
* Private prompts
* Activation prompts
* Prompt contracts
* Equation registry implementation
* Unit algebra implementation
* Domain handler implementation
* Internal helper functions
* Validation test harness
* Operational logs
* Raw computation traces
* Private engineering pack contents

The goal is to explain the architectural role of deterministic computation in EAS without exposing proprietary implementation details.

---

## 17. Implementation Status Note

This document describes the public-facing architecture and design intent of the Deterministic Computation Layer and MCM.

Specific supported equations, units, conversions, handlers, warnings, and statuses should be validated against the private implementation and test suite.

The public repository should avoid presenting untested behavior as a guaranteed implementation property.

---

## 18. Summary

The Deterministic Computation Layer is a central reliability feature of EAS.

Within the private EAS implementation, this deterministic capability is represented by the **Math Computation Module (MCM)**.

Together, the Deterministic Computation Layer and MCM support the broader EAS goal of making AI-assisted engineering more structured, traceable, and reviewable by providing:

* Structured variable handling
* Unit-aware computation
* Unit validation
* Unit conversion
* Constraint checking
* Candidate option evaluation
* Computed pass/fail results
* Warning generation
* Human-review escalation

This layer reflects a core EAS belief:

> AI-assisted engineering should not depend on fluent generated text alone when deterministic validation is possible.
