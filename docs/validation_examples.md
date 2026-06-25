# Validation Examples

## Engineering Assistance System (EAS)

This document provides public-safe validation examples for the **Engineering Assistance System (EAS)**.

The examples show how EAS can classify engineering advisory results using deterministic computation, unit validation, constraint checking, warning handling, governance status assignment, and human-review signaling.

These examples are intentionally simplified and sanitized. They are not raw operational logs, private test traces, full Math Computation Module (MCM) outputs, private prompts, source code, or internal validation records.

The guiding principle is:

> Validation examples should demonstrate the EAS review philosophy without exposing proprietary implementation details.

---

## 1. Purpose of Validation Examples

Validation examples help demonstrate how EAS treats different engineering advisory outcomes.

A mature AI-assisted engineering system should not present every response as equally reliable. Some outputs are clean computed results. Some are computed but warning-bearing. Some show that a design fails. Some require human review because the input is incomplete, ambiguous, unsupported, or safety-sensitive.

This document provides examples of:

* Clean computed result
* Computed selection pass
* Computed result with warnings
* Computed design failure
* Human-review-required result
* Unit validation warning
* Software systems engineering diagnostic review
* Exploratory engineering concept review

The examples are designed to show the relationship between:

```text id="c0nyyz"
Submitted Mode
Selected Engineering Pack
MCM / Deterministic Computation
Unit Validation
Constraint Results
Warnings
Governance Status
Human Review Status
```

---

## 2. Public-Facing Governance Statuses

EAS may use public-facing governance statuses such as:

| Governance Status           | Meaning                                                                                         |
| --------------------------- | ----------------------------------------------------------------------------------------------- |
| **computed_clean**          | Deterministic computation completed without required human-review flags or unresolved warnings. |
| **computed_selection_pass** | A valid selection was made among candidate options using computed constraints.                  |
| **computed_with_warnings**  | Computation completed, but warnings, assumptions, or limitations remain.                        |
| **computed_with_failure**   | One or more constraints failed, or the design/configuration was rejected.                       |
| **needs_human_review**      | The result requires qualified human review before reliance.                                     |

These statuses are advisory classifications, not certifications or approvals.

---

## 3. Validation Example Summary

| Example                          | Submitted Mode         | Selected Pack                   | Governance Status       | Human Review                                |
| -------------------------------- | ---------------------- | ------------------------------- | ----------------------- | ------------------------------------------- |
| 1. Power supply load check       | Solve Problem          | DC Controls / Power             | computed_clean          | Not Required                                |
| 2. Pump/pipe option selection    | Review Design          | Fluid Pump Loop                 | computed_selection_pass | Not Required, assuming inputs are confirmed |
| 3. Enclosure cooling estimate    | Solve Problem          | Thermal Enclosure Cooling       | computed_with_warnings  | Required for final design                   |
| 4. Conveyor drive speed review   | Review Design          | Mechanical Power Transmission   | computed_with_failure   | Required                                    |
| 5. Structural bracket review     | Review Design          | Structural / Mechanical Bracket | needs_human_review      | Required                                    |
| 6. Unit mismatch case            | Solve Problem          | Industrial Exhaust / Airflow    | needs_human_review      | Required                                    |
| 7. Software runtime failure      | Diagnose Root Cause    | Software Systems Engineering    | computed_with_warnings  | Context-dependent                           |
| 8. Exploratory aerospace concept | Explore Novel Solution | Aerospace Preliminary Design    | needs_human_review      | Required                                    |

---

## 4. Example 1: Clean Computed Result

### Scenario

The engineer wants to check whether a 24 VDC power supply can support a known load under a continuous loading limit.

### Submitted Request

```text id="rwoacw"
Submitted Mode:
Solve Problem

Selected Pack:
DC Controls / Power

Problem:
Determine whether an 8 A power supply can support a 6 A load using an
80% continuous loading limit.

Known Inputs:
- Power supply rating: 8 A
- Load current: 6 A
- Continuous loading limit: 80%
```

### Deterministic Computation

```text id="umr36j"
Maximum recommended continuous load = 8 A × 0.80
Maximum recommended continuous load = 6.4 A

Load current = 6 A
Constraint: load current ≤ maximum recommended continuous load

6 A ≤ 6.4 A
```

### Unit Validation

```text id="x5esmx"
Power supply rating unit: A
Load current unit: A
Computed limit unit: A
Unit validation: pass
```

### Constraint Result

| Constraint           | Computed / Observed Value | Requirement | Result |
| -------------------- | ------------------------: | ----------: | ------ |
| Power supply loading |                       6 A |     ≤ 6.4 A | Pass   |

### Governance Result

```text id="p3tzyf"
Computation status: computed
Unit validation: pass
Constraint status: pass
Warnings: none
Governance status: computed_clean
Human Review: Not Required
```

### Interpretation

This example demonstrates a clean deterministic computation. The required values are present, units are compatible, and the constraint passes.

This does not certify the electrical installation. It only means the simplified advisory check completed cleanly under the provided assumptions.

---

## 5. Example 2: Computed Selection Pass

### Scenario

The engineer wants to select the lowest-cost pump and pipe configuration that satisfies required flow and pressure constraints.

### Submitted Request

```text id="x5x163"
Submitted Mode:
Review Design

Selected Pack:
Fluid Pump Loop

Problem:
Select the lowest-cost pump and pipe option that satisfies flow and pressure.

Known Inputs:
- Required flow: 50 gpm
- Required discharge pressure: 60 psi
- Candidate options with cost and computed pass/fail results
```

### Candidate Results

```text id="fkttg1"
Option A:
- Cost: $4,800
- Flow requirement: pass
- Pressure requirement: fail

Option B:
- Cost: $5,220
- Flow requirement: pass
- Pressure requirement: pass

Option C:
- Cost: $5,700
- Flow requirement: pass
- Pressure requirement: pass
```

### Selection Rule

```text id="kgijxt"
Select the lowest-cost option among candidates that satisfy all required constraints.
```

### Deterministic Selection

```text id="tqsjr8"
Passing candidates:
- Option B: $5,220
- Option C: $5,700

Lowest-cost passing candidate:
- Option B
```

### Constraint Result

| Option   | Flow Requirement | Pressure Requirement |   Cost | Result              |
| -------- | ---------------- | -------------------- | -----: | ------------------- |
| Option A | Pass             | Fail                 | $4,800 | Rejected            |
| Option B | Pass             | Pass                 | $5,220 | Selected            |
| Option C | Pass             | Pass                 | $5,700 | Passing alternative |

### Governance Result

```text id="bdxk3a"
Computation status: computed
Selection status: pass
Unit validation: pass, assuming candidate data is confirmed
Constraint status: at least one candidate passes
Governance status: computed_selection_pass
Human Review: Not Required, assuming inputs and candidate data are confirmed
```

### Interpretation

This example demonstrates selection governance. EAS does not merely choose an option by preference. It applies a selection rule to passing candidates and identifies rejected options with reasons.

---

## 6. Example 3: Computed With Warnings

### Scenario

The engineer wants to estimate whether an enclosure cooling approach is sufficient, but important environmental and manufacturer data are missing.

### Submitted Request

```text id="pn272x"
Submitted Mode:
Solve Problem

Selected Pack:
Thermal Enclosure Cooling

Problem:
Estimate the cooling requirement for an electronics enclosure.

Known Inputs:
- Internal heat load: 600 W
- Maximum internal temperature: 40 °C
- Ambient temperature: not provided
- Solar loading: not provided
- Manufacturer derating data: not provided
```

### Computation Summary

```text id="0h34n4"
A preliminary heat-load estimate can be performed from the provided internal
heat load, but final cooling suitability cannot be confirmed without ambient
conditions, enclosure details, and equipment derating data.
```

### Warning Conditions

```text id="jtzxkf"
Warnings:
- Ambient temperature was not provided.
- Solar loading was not provided.
- Enclosure dimensions and material were not provided.
- Manufacturer derating data was not provided.
```

### Governance Result

```text id="zoh5fc"
Computation status: partial or computed_with_assumptions
Unit validation: pass for provided heat-load unit
Constraint status: incomplete
Warnings: present
Governance status: computed_with_warnings
Human Review: Required for final thermal design
```

### Interpretation

This example demonstrates that a computation may be possible while the result remains warning-bearing. EAS should surface the limitations rather than presenting the estimate as final design approval.

---

## 7. Example 4: Computed With Failure

### Scenario

The engineer wants to review whether a conveyor drive configuration satisfies a required belt speed range.

### Submitted Request

```text id="6dzp4d"
Submitted Mode:
Review Design

Selected Pack:
Mechanical Power Transmission

Problem:
Review a conveyor drive configuration.

Known Inputs:
- Motor speed: 1,750 rpm
- Gear ratio: 20:1
- Drive pulley diameter: 2.67 in
- Required belt speed range: 75–85 ft/min
```

### Deterministic Computation

```text id="5u95mg"
Output shaft speed = 1,750 rpm / 20
Output shaft speed = 87.5 rpm

Pulley circumference ≈ π × 2.67 in
Pulley circumference ≈ 8.39 in/rev

Belt speed ≈ 8.39 in/rev × 87.5 rev/min
Belt speed ≈ 734.1 in/min
Belt speed ≈ 61.18 ft/min
```

### Unit Validation

```text id="iqnyhr"
Motor speed: rpm
Pulley diameter: inches
Computed belt speed: ft/min
Required belt speed: ft/min
Unit validation: pass
```

### Constraint Result

| Constraint | Computed Value |  Requirement | Result |
| ---------- | -------------: | -----------: | ------ |
| Belt speed |   61.18 ft/min | 75–85 ft/min | Fail   |

### Governance Result

```text id="lp31a8"
Computation status: computed
Unit validation: pass
Constraint status: fail
Failure condition: belt_speed_below_required_range
Governance status: computed_with_failure
Human Review: Required
```

### Interpretation

This example demonstrates that completed computation does not imply design success. The calculation completed cleanly, but the design fails the stated requirement.

---

## 8. Example 5: Needs Human Review Due to Missing Structural Data

### Scenario

The engineer wants to evaluate a bracket for real-world installation, but critical structural inputs are missing.

### Submitted Request

```text id="n92y7i"
Submitted Mode:
Review Design

Selected Pack:
Structural / Mechanical Bracket

Problem:
Evaluate whether a cantilever bracket is acceptable for real-world use.

Known Inputs:
- Load: 150 lbf
- Arm length: 18 in
- Bracket material: unspecified
- Cross-section dimensions: incomplete
- Mounting method: unspecified
- Safety factor: not provided
```

### Missing Critical Information

```text id="6dhiaf"
Missing Information:
- Material yield strength
- Cross-section dimensions
- Moment of inertia
- Mounting method
- Fastener details
- Load case
- Safety factor
- Dynamic or fatigue conditions
```

### Governance Result

```text id="gwljqi"
Computation status: partial or unsupported
Unit validation: incomplete
Constraint status: not fully evaluable
Warnings: critical structural information missing
Governance status: needs_human_review
Human Review: Required
```

### Interpretation

This example demonstrates a protective escalation. Even if some simplified calculations could be attempted, the missing structural information makes the advisory result inappropriate for reliance without qualified review.

---

## 9. Example 6: Needs Human Review Due to Unit Mismatch

### Scenario

The engineer wants to evaluate airflow performance, but the input units are ambiguous or incompatible.

### Submitted Request

```text id="l212wz"
Submitted Mode:
Solve Problem

Selected Pack:
Industrial Exhaust / Airflow

Problem:
Determine whether an exhaust opening satisfies the required airflow condition.

Known Inputs:
- Airflow: 2,000 cfm
- Opening size: 24
- Required velocity: 100 ft/min
```

### Unit Problem

```text id="expm9p"
The opening size is provided as "24" without a unit or geometry.
It is unclear whether this means:
- 24 in diameter
- 24 in by 24 in
- 24 ft²
- another opening dimension
```

### Governance Result

```text id="0vy61w"
Computation status: partial
Unit validation: fail or incomplete
Constraint status: not evaluable
Warnings:
- Missing unit
- Ambiguous geometry
Governance status: needs_human_review
Human Review: Required
```

### Interpretation

This example demonstrates that EAS should not force a calculation when dimensional information is ambiguous. Unit ambiguity should be surfaced instead of silently assumed.

---

## 10. Example 7: Software Systems Engineering Diagnostic Review

### Scenario

The engineer wants help diagnosing an intermittent backend failure after deployment.

### Submitted Request

```text id="hvywns"
Submitted Mode:
Diagnose Root Cause

Selected Pack:
Software Systems Engineering

Problem:
Diagnose why a backend workflow intermittently fails after deployment.

Known Inputs:
- Failure occurs only in production
- Local development environment works
- Error appears after a background job resumes
- Logs show occasional timeout and missing state
- Deployment environment differs from local environment
```

### Diagnostic Reasoning

A public-safe diagnostic result may identify likely causes:

```text id="s096tm"
Likely causes:
1. Environment-specific configuration mismatch
2. Race condition or stale state during job resume
3. Timeout threshold too low for production latency
4. Missing persistence or incomplete recovery logic
5. External dependency failure or rate limiting
```

### Validation Recommendations

```text id="dlfqdt"
Recommended checks:
- Compare environment variables between local and production.
- Add correlation IDs to job lifecycle logs.
- Inspect resume-state persistence.
- Measure timeout frequency and latency distribution.
- Reproduce with production-like timing and dependency conditions.
```

### Governance Result

```text id="escn1r"
Computation status: not primarily numeric
Validation status: diagnostic reasoning with evidence gaps
Warnings:
- Logs are incomplete.
- Exact failure trace is not provided.
- Production environment details are incomplete.
Governance status: computed_with_warnings
Human Review: Context-dependent
```

### Interpretation

This example demonstrates that not every EAS validation workflow is numeric. For software systems engineering, validation may involve diagnostic reasoning, evidence requirements, observability recommendations, and testing steps.

---

## 11. Example 8: Exploratory Aerospace Concept Requires Review

### Scenario

The engineer wants to explore an early aerospace concept.

### Submitted Request

```text id="505upp"
Submitted Mode:
Explore Novel Solution

Selected Pack:
Aerospace Preliminary Design

Problem:
Explore whether a lightweight aerial platform concept could satisfy a
preliminary payload and endurance target.

Known Inputs:
- Payload target provided
- Endurance target provided
- Vehicle mass estimate incomplete
- Propulsion data not provided
- Aerodynamic coefficients not provided
- Flight safety and regulatory context not provided
```

### Advisory Notes

```text id="1m8nlj"
The concept may be discussed at a preliminary feasibility level, but the
available information is insufficient for a validated aerospace design.
```

### Warning Conditions

```text id="xe3jr5"
Warnings:
- Mass estimate incomplete
- Propulsion data missing
- Aerodynamic data missing
- Flight envelope not defined
- Safety and regulatory requirements not evaluated
```

### Governance Result

```text id="30ej65"
Computation status: partial or unsupported
Unit validation: incomplete
Constraint status: not fully evaluable
Warnings: safety-critical aerospace context
Governance status: needs_human_review
Human Review: Required
```

### Interpretation

This example demonstrates the difference between exploring a concept and validating a design. EAS may support early reasoning, but aerospace concepts require qualified review before any real-world development, testing, or deployment.

---

## 12. Cross-Example Lessons

The examples demonstrate several EAS validation principles.

### 12.1 Computed Does Not Always Mean Passed

A calculation can complete successfully while the design fails.

Example:

```text id="pn9m2o"
Belt speed was computed successfully.
The computed value failed the required speed range.
Governance status: computed_with_failure
```

---

### 12.2 Missing Information Should Be Visible

EAS should not hide missing values.

Example:

```text id="crqbwb"
Material strength missing.
Safety factor missing.
Mounting method missing.
Governance status: needs_human_review
```

---

### 12.3 Unit Problems Should Not Be Ignored

EAS should not silently assume units when they are critical.

Example:

```text id="xm5vy8"
Opening size = 24
Unit and geometry are ambiguous.
Governance status: needs_human_review
```

---

### 12.4 Selection Should Be Constraint-Based

Candidate selection should be based on passing constraints and stated selection rules.

Example:

```text id="m9p8qw"
Option B is selected because it is the lowest-cost passing candidate.
Option A is rejected because it fails pressure.
Option C passes but costs more than Option B.
```

---

### 12.5 Human Review Is a Feature, Not a Failure

Human-review escalation is part of the EAS safety and governance design.

Example:

```text id="7gm9ip"
Aerospace concept has incomplete mass, propulsion, and aerodynamic data.
Governance status: needs_human_review
```

This is not a system failure. It is appropriate caution.

---

## 13. Validation Pattern

A public-safe validation pattern can be summarized as:

```text id="uv37qf"
1. Receive submitted engineering mode.
2. Select engineering pack.
3. Extract known inputs and constraints.
4. Identify missing information.
5. Route supported calculations to MCM, when applicable.
6. Validate units.
7. Check constraints.
8. Identify warnings and failure conditions.
9. Assign governance status.
10. Set human-review status.
11. Produce structured advisory report.
```

---

## 14. Public Repository Boundary

This document provides public-safe validation examples.

It does not include:

* Private source code
* Backend implementation
* Private prompts
* Activation prompts
* Prompt contracts
* Internal schemas
* Full MCM traces
* Parser logic
* Unit-algebra implementation
* Internal equation handlers
* Full validation test harness
* Operational logs
* Raw engineering reports
* Private engineering pack contents
* Carter or Synthetic OS private internals

The examples are intended to show the EAS validation philosophy without exposing proprietary implementation details.

---

## 15. Implementation Status Note

These examples describe public-facing validation concepts and simplified expected behavior.

Specific outputs, rounding, supported calculations, status transitions, human-review triggers, warnings, and report formatting should be validated against the private EAS implementation and test suite.

The public repository should avoid presenting untested behavior as a guaranteed implementation property.

---

## 16. Summary

EAS validation is not limited to checking whether an answer sounds plausible.

The validation approach emphasizes:

* Submitted engineering mode
* Domain-aware engineering pack selection
* Structured known inputs
* Missing information visibility
* MCM-supported deterministic computation where applicable
* Unit validation
* Constraint checking
* Warning generation
* Governance status assignment
* Human-review signaling

The core belief is:

> AI-assisted engineering should show the status of the result, not just the result itself.
