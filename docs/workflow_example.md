# Workflow Example

## Engineering Assistance System (EAS)

This document provides a public-safe example of how the **Engineering Assistance System (EAS)** processes an engineering request.

The example is intentionally simplified and sanitized. It is meant to demonstrate the EAS workflow, not expose private prompts, implementation details, source code, schemas, internal computation traces, or proprietary engineering pack contents.

The example shows how EAS can transform a natural-language engineering request into a structured Engineering Advisory Report using:

* Submitted engineering mode
* Engineering pack selection
* LLM-assisted planning
* Deterministic computation through the Math Computation Module (MCM), when applicable
* Unit validation
* Constraint checking
* Governance status assignment
* Human-review signaling

---

## 1. Example Scenario

An engineer wants to review a conveyor drive design.

The design includes a motor, gear reduction, and drive pulley. The engineer wants to know whether the proposed configuration satisfies the required belt speed range.

This is a design-review task because the user is asking whether a proposed configuration satisfies a stated requirement.

---

## 2. Submitted Engineering Request

```text
Submitted Engineering Mode:
Review Design

Engineering Domain:
Mechanical Power Transmission

Problem Statement:
Review this conveyor drive configuration and determine whether the proposed
motor, gear ratio, and drive pulley satisfy the required belt speed range.

Known Inputs:
- Motor speed: 1,750 rpm
- Gear ratio: 20:1
- Drive pulley diameter: 2.67 in
- Required belt speed range: 75–85 ft/min

Desired Output:
Determine whether the design passes or fails the belt-speed requirement.
```

---

## 3. Mode Submission

A mode is submitted with every EAS request.

If the engineer does not manually select a mode, the submitted mode defaults to **Solve Problem**. In this example, the engineer explicitly selected:

```text
Review Design
```

The submitted mode frames the advisory workflow.

Because the submitted mode is **Review Design**, EAS emphasizes:

* Known design values
* Required constraints
* Computed design performance
* Pass/fail results
* Recommendation
* Human-review status

---

## 4. Engineering Pack Selection

For this example, the selected engineering pack is:

```text
Mechanical Power Transmission
```

This pack is appropriate because the request involves:

* Motor speed
* Gear ratio
* Pulley diameter
* Belt speed
* Drive-system performance
* Constraint comparison

The selected pack provides domain framing for the advisory report.

The private contents of the engineering pack are not included in this public repository.

---

## 5. LLM Planning Stage

At a public-safe level, the LLM planning stage interprets the request and identifies the likely calculation path.

For this example, the planning stage may identify:

```text
Task type:
Review a proposed mechanical power-transmission design.

Known values:
- Motor speed
- Gear ratio
- Pulley diameter
- Required belt speed range

Unknown value:
- Actual belt speed

Required check:
- Determine whether computed belt speed falls within the required range.

Likely deterministic computation:
- Compute output shaft speed from motor speed and gear ratio.
- Compute belt speed from pulley diameter and output shaft speed.
- Compare computed belt speed against the required range.
```

The language model helps organize the engineering workflow, but the numerical calculation should be checked deterministically where possible.

---

## 6. Deterministic Computation Stage

The deterministic computation stage is represented within the private EAS implementation by the **Math Computation Module (MCM)**.

For this example, MCM-style computation may proceed conceptually as follows.

### Step 1: Compute Output Shaft Speed

```text
Output shaft speed = motor speed / gear ratio
Output shaft speed = 1,750 rpm / 20
Output shaft speed = 87.5 rpm
```

### Step 2: Compute Pulley Circumference

```text
Pulley circumference = π × pulley diameter
Pulley circumference = π × 2.67 in
Pulley circumference ≈ 8.39 in/rev
```

### Step 3: Compute Belt Speed

```text
Belt speed = pulley circumference × output shaft speed
Belt speed ≈ 8.39 in/rev × 87.5 rev/min
Belt speed ≈ 734.1 in/min
```

Convert inches per minute to feet per minute:

```text
Belt speed ≈ 734.1 in/min ÷ 12
Belt speed ≈ 61.18 ft/min
```

The exact displayed value may vary slightly depending on rounding.

---

## 7. Unit Validation

The calculation requires unit handling.

Public-safe unit validation notes:

```text
Motor speed was provided in rpm.
Gear ratio was treated as dimensionless.
Pulley diameter was provided in inches.
Pulley circumference was computed in inches per revolution.
Belt speed was converted from inches per minute to feet per minute.
The required belt speed was provided in ft/min.
```

The computed value and required range are both evaluated in:

```text
ft/min
```

No unit incompatibility is identified in this simplified example.

---

## 8. Constraint Checking

The design requirement is:

```text
Required belt speed range: 75–85 ft/min
```

The computed result is approximately:

```text
Computed belt speed: 61.18 ft/min
```

Constraint comparison:

```text
61.18 ft/min is below the required 75–85 ft/min range.
```

Therefore:

```text
Belt speed constraint: Fail
```

---

## 9. Governance Gate Evaluation

The Governance Gate evaluates the workflow result before the final report is produced.

For this example:

```text
Submitted mode: Review Design
Selected pack: Mechanical Power Transmission
Computation status: computed
Unit validation: pass
Constraint status: fail
Primary failure: belt speed below required range
```

Because the design fails a stated requirement, the appropriate public-facing governance status is:

```text
computed_with_failure
```

The human-review status may be:

```text
Human Review: Required
```

This is appropriate because the proposed mechanical design does not satisfy the stated operating requirement and should not be deployed without review or redesign.

---

## 10. Final Engineering Advisory Report Example

A simplified public-safe final report may look like this:

```markdown
# Engineering Advisory Report

## Report Header
- System: Engineering Assistance System (EAS)
- Submitted Mode: Review Design
- Selected Pack: Mechanical Power Transmission
- Governance Status: computed_with_failure
- Human Review: Required

## Problem Summary
The user requested a review of a conveyor drive configuration to determine
whether the proposed motor, gear ratio, and drive pulley satisfy the required
belt speed range.

## Known Inputs
- Motor speed: 1,750 rpm
- Gear ratio: 20:1
- Drive pulley diameter: 2.67 in
- Required belt speed range: 75–85 ft/min

## Missing Information
- Service factor was not provided.
- Startup torque requirement was not provided.
- Belt slip was not provided.
- Manufacturer drive ratings were not provided.

## Assumptions
- Gear ratio is interpreted as motor speed divided by output shaft speed.
- Pulley diameter is treated as effective pitch diameter.
- Belt slip is neglected for this preliminary calculation.
- Required belt speed range is treated as a hard design constraint.

## Computation Summary
- Output shaft speed = 1,750 rpm / 20 = 87.5 rpm
- Pulley circumference ≈ π × 2.67 in ≈ 8.39 in/rev
- Belt speed ≈ 8.39 in/rev × 87.5 rev/min
- Belt speed ≈ 734.1 in/min
- Belt speed ≈ 61.18 ft/min

## Unit Validation Notes
- Motor speed was provided in rpm.
- Pulley diameter was provided in inches.
- Belt speed was converted to ft/min.
- The computed belt speed and required belt speed range use compatible units.

## Constraint Results

| Constraint | Computed Value | Requirement | Result |
|---|---:|---:|---|
| Belt speed | 61.18 ft/min | 75–85 ft/min | Fail |

## Recommendation
The proposed conveyor drive configuration should be rejected for the stated
belt-speed requirement because the computed belt speed is below the required
75–85 ft/min range.

A revised gear ratio, larger effective pulley diameter, or different drive
configuration should be evaluated.

## Risks and Limitations
- Belt slip was not modeled.
- Startup torque was not provided.
- Service factor was not provided.
- Manufacturer drive ratings were not checked.
- Guarding, safety, and real-world machinery requirements were not evaluated.

## Governance Status
computed_with_failure

## Human Review Status
Required

## Suggested Next Validation Steps
1. Confirm the effective pulley pitch diameter.
2. Confirm the gear ratio interpretation.
3. Determine startup torque and service factor requirements.
4. Evaluate revised gear ratio or pulley options.
5. Review the final drive configuration with qualified personnel before deployment.
```

---

## 11. Workflow Summary

This example demonstrates the EAS workflow:

```text
1. Engineer submits a design-review request.
2. EAS receives the submitted mode: Review Design.
3. EAS selects the Mechanical Power Transmission pack.
4. The LLM planning stage identifies the required calculations.
5. MCM-style deterministic computation calculates belt speed.
6. Unit validation confirms compatible speed units.
7. Constraint checking determines that the belt speed fails the required range.
8. The Governance Gate assigns computed_with_failure.
9. EAS produces a structured Engineering Advisory Report.
10. The report marks Human Review as Required.
```

---

## 12. Why This Workflow Matters

This workflow matters because EAS does not simply produce a fluent opinion.

Instead, it separates the advisory process into distinct stages:

```text
Interpret the request.
Identify the submitted mode.
Select the engineering pack.
Plan the calculation.
Compute deterministically where possible.
Validate units.
Check constraints.
Assign governance status.
Produce a structured report.
Identify human-review requirements.
```

This makes the output more traceable and reviewable than a typical unstructured AI response.

---

## 13. Alternate Workflow Types

The same EAS architecture can support other workflow types.

### Solve Problem

Example:

```text
Calculate voltage drop in a 24 VDC circuit.
```

Likely emphasis:

* Known inputs
* Computation summary
* Unit validation
* Final result
* Human-review status

### Diagnose Root Cause

Example:

```text
Diagnose why a hydraulic press fixture is producing low clamp force.
```

Likely emphasis:

* Symptoms
* Likely causes
* Evidence
* Recommended measurements
* Safety notes
* Human-review status

### Suggest Improvements

Example:

```text
Suggest ways to improve enclosure cooling performance.
```

Likely emphasis:

* Current limitation
* Improvement options
* Tradeoffs
* Risks
* Validation steps

### Explore Novel Solution

Example:

```text
Explore an alternative lightweight bracket geometry.
```

Likely emphasis:

* Concept
* Feasibility
* Assumptions
* Unknowns
* Validation path
* Human-review status

### Software Systems Engineering

Example:

```text
Diagnose why a backend workflow intermittently fails after deployment.
```

Likely emphasis:

* Observed behavior
* Expected behavior
* Logs or traces
* System architecture
* Failure hypotheses
* Recommended diagnostic steps
* Test and validation plan
* Human-review status

---

## 14. Public Repository Boundary

This document describes a public-safe EAS workflow example.

It does not include:

* Private source code
* Backend implementation
* Private prompts
* Activation prompts
* Prompt contracts
* Internal schemas
* Full MCM traces
* Internal computation logic
* Full engineering pack contents
* Model-routing logic
* Operational logs
* Raw engineering reports
* Carter or Synthetic OS private internals

The example is intended to explain the EAS workflow at a conceptual and portfolio-safe level.

---

## 15. Safety and Limitation Note

The example report is advisory only.

It does not represent:

* Professional engineering certification
* Machinery approval
* Safety approval
* Code compliance
* Manufacturing release
* Final design authority

Any real-world mechanical design, machinery change, safety-critical decision, or production deployment should be reviewed by qualified professionals.

---

## 16. Summary

This workflow example shows how EAS can transform an engineering request into a structured advisory report by combining:

* Submitted engineering mode
* Engineering pack selection
* LLM-based interpretation
* Deterministic computation through MCM where applicable
* Unit validation
* Constraint checking
* Governance status assignment
* Human-review signaling
* Structured report generation

The central idea is:

> EAS is not only generating an answer. It is organizing an engineering advisory workflow around computation, validation, governance, and review.
