# Sanitized Engineering Request

## Engineering Assistance System (EAS)

This file provides a public-safe example of an engineering request that could be submitted to the **Engineering Assistance System (EAS)**.

The example is intentionally simplified and sanitized. It does not represent a real customer request, proprietary design, confidential system, private operational log, or complete engineering specification.

The purpose of this example is to show the type of structured input EAS is designed to process.

---

## Example Request Type

```text
Submitted Engineering Mode:
Review Design
```

```text
Engineering Domain:
Mechanical Power Transmission
```

```text
Selected Engineering Pack:
mechanical_power_transmission_pack
```

---

## Problem Statement

Review a conveyor drive configuration and determine whether the proposed motor, gear ratio, and drive pulley satisfy the required belt speed range.

The advisory output should determine whether the design passes or fails the stated speed requirement and should identify any missing information, assumptions, risks, and recommended next validation steps.

---

## Known Inputs

```text
Motor speed: 1,750 rpm
Gear ratio: 20:1
Drive pulley diameter: 2.67 in
Required belt speed range: 75–85 ft/min
```

---

## Desired Outputs

```text
- Compute output shaft speed.
- Compute approximate belt speed.
- Compare computed belt speed against the required range.
- Determine whether the design passes or fails.
- Identify missing information.
- Identify assumptions.
- Provide a recommendation.
- Assign governance status.
- Assign human-review status.
```

---

## Constraints

```text
Belt speed must be between 75 and 85 ft/min.
```

---

## Candidate Design

```text
Motor:
- Nominal speed: 1,750 rpm

Reducer:
- Gear ratio: 20:1

Drive pulley:
- Effective diameter: 2.67 in

Application:
- Conveyor drive
```

---

## Missing or Unconfirmed Information

```text
- Service factor was not provided.
- Startup torque requirement was not provided.
- Belt slip was not provided.
- Duty cycle was not provided.
- Manufacturer drive ratings were not provided.
- Guarding and machinery-safety requirements were not provided.
```

---

## Assumptions Allowed for Preliminary Review

```text
- Gear ratio may be interpreted as motor speed divided by output shaft speed.
- Pulley diameter may be treated as effective pitch diameter.
- Belt slip may be neglected for preliminary calculation.
- Required belt speed range may be treated as a hard design constraint.
```

---

## Expected EAS Workflow

```text
1. Receive submitted mode: Review Design.
2. Identify domain context: Mechanical Power Transmission.
3. Extract known values and units.
4. Identify missing information.
5. Plan required calculations.
6. Route supported calculations to the deterministic computation layer / MCM.
7. Validate units.
8. Check the belt-speed constraint.
9. Assign governance status.
10. Produce an Engineering Advisory Report.
11. Identify whether human review is required.
```

---

## Expected Public-Safe Result Type

The expected result should be a structured **Engineering Advisory Report**.

The report should include:

```text
- Problem Summary
- Submitted Engineering Mode
- Selected Engineering Pack
- Known Inputs
- Missing Information
- Assumptions
- Computation Summary
- Unit Validation Notes
- Constraint Results
- Recommendation
- Risks and Limitations
- Governance Status
- Human Review Status
- Suggested Next Validation Steps
```

---

## Safety and Review Note

This request is for advisory demonstration only.

It does not represent final machinery approval, professional engineering certification, code compliance, safety approval, manufacturing release, or deployment authorization.

Any real conveyor drive, machinery design, or moving-equipment system should be reviewed by qualified professionals before implementation or operation.

---

## Public Repository Boundary

This example does not include:

```text
- Private prompts
- Activation prompts
- Source code
- Backend implementation details
- Internal schemas
- Full MCM traces
- Operational logs
- Raw EAS reports
- Proprietary engineering pack contents
- Customer data
- Confidential design data
```

This file is intended only to demonstrate the kind of sanitized input EAS can process.
