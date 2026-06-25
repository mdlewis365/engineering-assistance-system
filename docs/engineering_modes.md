# Engineering Modes

## Engineering Assistance System (EAS)

The **Engineering Assistance System (EAS)** supports multiple engineering modes. These modes define the type of engineering assistance being requested and help guide the system’s workflow, domain-pack selection, computation strategy, governance evaluation, and final advisory report structure.

Engineering modes allow EAS to behave less like a general chatbot and more like a structured engineering advisory workflow.

A mode is submitted with every EAS request. If the engineer does not manually choose a mode, the submitted mode defaults to **Solve Problem**.

The current public-facing EAS modes are:

```text
Solve Problem
Diagnose Root Cause
Review Design
Suggest Improvements
Explore Novel Solution
```

Each mode has a different purpose, input expectation, output structure, and human-review profile.

---

## 1. Purpose of Engineering Modes

Engineering requests vary significantly.

One engineer may ask EAS to compute a value. Another may ask it to diagnose a failure. Another may ask whether a proposed design satisfies constraints. Another may want improvement ideas or exploration of a possible solution path.

Engineering modes help EAS determine:

* What kind of task is being performed
* What information should be extracted
* Which domain context is relevant
* Whether deterministic computation is likely required
* What kind of advisory report should be produced
* What warnings or human-review triggers should be considered

Because a mode is submitted with every request, EAS does not begin from a mode-less input. The submitted mode acts as the primary workflow frame for the advisory report.

---

## 2. Mode Overview

| Mode                       | Primary Purpose                                                     | Typical Output                                                           |
| -------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **Solve Problem**          | Compute or estimate an engineering result from known inputs.        | Calculation summary, result, assumptions, unit notes, review status.     |
| **Diagnose Root Cause**    | Identify likely causes of a failure, symptom, or performance issue. | Ranked causes, evidence, recommended checks, review status.              |
| **Review Design**          | Evaluate whether a proposed design satisfies stated constraints.    | Pass/fail results, constraint checks, rejection reasons, recommendation. |
| **Suggest Improvements**   | Recommend improvements to an existing design or system.             | Improvement options, tradeoffs, risks, next validation steps.            |
| **Explore Novel Solution** | Explore a possible engineering concept or alternative architecture. | Concept analysis, feasibility notes, risks, validation path.             |

---

## 3. Solve Problem Mode

### Purpose

**Solve Problem** mode is used when the engineer wants EAS to compute, estimate, or determine an engineering result from known inputs.

This mode is most appropriate when the request has a clear unknown value and enough known values to support calculation, estimation, or structured analysis.

**Solve Problem** is also the default submitted mode when the engineer does not manually choose another mode.

### Typical Requests

Examples:

```text
Calculate the voltage drop in this 24 VDC circuit.
```

```text
Determine the required airflow area for a given flow rate and face velocity.
```

```text
Estimate the heat removal requirement for this enclosure.
```

```text
Calculate the torque required at this shaft.
```

### Expected Inputs

Solve Problem mode benefits from:

* Known values
* Units
* Target unknowns
* Equations or engineering context, if known
* Constraints or acceptance criteria
* Environmental or operating assumptions

### Typical Outputs

A Solve Problem report may include:

* Problem summary
* Known values
* Unknown value being solved
* Assumptions
* Computation summary
* Unit validation notes
* Final result
* Sensitivity notes, if applicable
* Human-review status

### Deterministic Computation Role

Solve Problem mode is often a strong candidate for deterministic computation.

When values, units, and relationships are sufficiently structured, EAS may route calculations to a deterministic computation layer to reduce reliance on generated numerical output.

### Human-Review Considerations

Human review may be required if:

* Critical inputs are missing
* Units are ambiguous or incompatible
* The requested calculation is outside supported scope
* The result affects real-world safety or regulated design
* The calculation depends on assumptions that require confirmation

---

## 4. Diagnose Root Cause Mode

### Purpose

**Diagnose Root Cause** mode is used when the engineer wants EAS to analyze a failure, symptom, performance issue, or abnormal system behavior.

This mode emphasizes evidence, likely causes, diagnostic sequencing, and confirmation steps.

### Typical Requests

Examples:

```text
Diagnose why this hydraulic press fixture is producing low clamp force.
```

```text
Determine why the motor is overheating during normal operation.
```

```text
Identify likely causes of low airflow in this exhaust system.
```

```text
Explain why this pump loop is not reaching the required flow rate.
```

### Expected Inputs

Diagnose Root Cause mode benefits from:

* Observed symptoms
* Normal operating expectations
* Recent changes to the system
* Measurements already taken
* Known good and known bad conditions
* System configuration
* Failure timing
* Environmental or operating context

### Typical Outputs

A diagnostic report may include:

* Problem summary
* Observed symptoms
* Known facts
* Missing diagnostic information
* Ranked likely causes
* Evidence supporting each cause
* Recommended inspection or measurement order
* Immediate risk notes
* Human-review status

### Deterministic Computation Role

Diagnose Root Cause mode may use deterministic computation when a symptom depends on measurable relationships.

Examples include:

* Pressure drop
* Flow rate
* Voltage drop
* Power draw
* Torque requirement
* Heat load
* Speed mismatch

However, diagnostic reasoning often includes qualitative evidence that cannot be reduced fully to computation.

### Human-Review Considerations

Human review may be required if:

* The failure mode is safety-critical
* The system involves pressure, electricity, heat, motion, or structural loads
* Evidence is insufficient to rank causes confidently
* The diagnosis could lead to hazardous maintenance actions
* The issue involves regulated equipment or code compliance

---

## 5. Review Design Mode

### Purpose

**Review Design** mode is used when the engineer wants EAS to evaluate whether a proposed design, configuration, or selection satisfies stated requirements.

This mode emphasizes constraints, pass/fail logic, rejected options, and final recommendation.

### Typical Requests

Examples:

```text
Review this 24 VDC control circuit and determine whether the wire size,
fuse size, and power supply are appropriate.
```

```text
Evaluate whether this cantilever bracket satisfies stress and deflection limits.
```

```text
Determine whether this conveyor drive design meets the required belt speed.
```

```text
Select the lowest-cost pump and pipe configuration that satisfies the required flow and pressure.
```

### Expected Inputs

Review Design mode benefits from:

* Proposed design values
* Candidate options, if applicable
* Required constraints
* Units
* Acceptance criteria
* Safety factors
* Environmental or operating conditions
* Material or component properties

### Typical Outputs

A design-review report may include:

* Problem summary
* Proposed design
* Selected domain pack
* Known inputs
* Assumptions
* Constraint table
* Pass/fail status
* Rejected options and reasons
* Recommended option or design correction
* Human-review status

### Deterministic Computation Role

Review Design mode is one of the strongest use cases for deterministic computation.

Where possible, EAS can compute values and compare them against constraints instead of relying on a language model to state whether the design passes.

Examples include:

* Required versus available capacity
* Maximum versus actual load
* Speed range compliance
* Voltage drop limit
* Deflection limit
* Pressure or flow requirement
* Cost-based selection among passing options

### Human-Review Considerations

Human review may be required if:

* The design affects real-world safety
* The design is regulated or code-governed
* Constraint data is incomplete
* Material properties are missing
* Safety factors are not specified
* The design fails one or more required constraints
* The design passes only under assumptions that require confirmation

---

## 6. Suggest Improvements Mode

### Purpose

**Suggest Improvements** mode is used when the engineer wants EAS to recommend ways to improve an existing design, system, workflow, or configuration.

This mode emphasizes alternatives, tradeoffs, and practical next steps rather than a single computed answer.

### Typical Requests

Examples:

```text
Suggest improvements to reduce voltage drop in this control circuit.
```

```text
Recommend ways to improve cooling performance in this enclosure.
```

```text
Suggest design changes to improve pump-loop efficiency.
```

```text
Recommend ways to increase conveyor throughput without replacing the motor.
```

### Expected Inputs

Suggest Improvements mode benefits from:

* Current design or system description
* Known performance limitations
* Constraints
* Budget or cost limits
* Space limits
* Operating conditions
* Components that cannot be changed
* Desired improvement target

### Typical Outputs

An improvement report may include:

* Problem summary
* Current system limitations
* Improvement options
* Benefits and tradeoffs
* Implementation complexity
* Risks
* Required validation
* Recommended next steps
* Human-review status

### Deterministic Computation Role

Suggest Improvements mode may use deterministic computation to compare improvement options.

Examples include:

* Calculating improvement margins
* Estimating capacity changes
* Comparing pressure drop reductions
* Estimating thermal benefit
* Checking whether a proposed improvement satisfies constraints

However, this mode may also include qualitative engineering judgment, tradeoff analysis, and practical implementation notes.

### Human-Review Considerations

Human review may be required if:

* The improvement changes a safety-critical function
* The change affects code compliance
* The recommendation alters structural, electrical, pressure, thermal, or moving equipment
* The improvement depends on uncertain assumptions
* The change could introduce new failure modes

---

## 7. Explore Novel Solution Mode

### Purpose

**Explore Novel Solution** mode is used when the engineer wants to examine a possible engineering concept, alternative architecture, or unconventional solution path.

This mode is exploratory rather than certifying.

It is useful for early-stage engineering thinking, concept development, feasibility discussion, and identifying validation requirements.

### Typical Requests

Examples:

```text
Explore a passive cooling alternative for this electronics enclosure.
```

```text
Consider whether a different airflow architecture could improve capture performance.
```

```text
Explore a lightweight bracket geometry that reduces deflection.
```

```text
Evaluate whether a different power-transmission approach could meet the same speed requirement.
```

### Expected Inputs

Explore Novel Solution mode benefits from:

* Current problem or limitation
* Desired outcome
* Existing constraints
* Available materials or components
* Operating environment
* Performance targets
* Known failure modes
* Boundaries on what may be changed

### Typical Outputs

An exploratory report may include:

* Concept summary
* Engineering rationale
* Feasibility notes
* Key assumptions
* Advantages
* Risks
* Unknowns
* Required calculations
* Suggested validation path
* Human-review status

### Deterministic Computation Role

Explore Novel Solution mode may use deterministic computation for early feasibility checks.

Examples include:

* Approximate capacity
* Estimated load
* Basic geometry checks
* Thermal estimates
* Flow estimates
* Speed or torque estimates

However, exploratory concepts are often under-specified. EAS should avoid presenting speculative concepts as validated designs.

### Human-Review Considerations

Human review is especially important in this mode because the work is exploratory.

Human review may be required if:

* The concept is novel or untested
* The concept affects safety-critical systems
* The feasibility depends on assumptions
* Required material or environmental data is missing
* The design would require physical prototyping or regulated approval
* The output could be mistaken for a certified engineering design

---

## 8. Mode Submission and Interpretation Logic

EAS receives an engineering mode with every submitted request.

If the engineer does not manually select a mode, the input workflow submits **Solve Problem** as the default mode. If the engineer selects another mode, such as **Diagnose Root Cause**, **Review Design**, **Suggest Improvements**, or **Explore Novel Solution**, that selected mode is submitted with the request.

This means EAS does not begin from a mode-less request. The system always receives a declared primary mode.

Public-facing modes include:

```text
Solve Problem
Diagnose Root Cause
Review Design
Suggest Improvements
Explore Novel Solution
```

The submitted mode acts as the primary workflow frame for the advisory report.

For example, if the submitted mode is:

```text
Explore Novel Solution
```

EAS should treat the request as an exploratory engineering task unless the request is clearly incompatible with that mode or raises a safety, scope, or governance concern.

When the submitted mode and the natural-language request appear to have mixed characteristics, EAS may identify supporting characteristics without silently replacing the submitted primary mode.

Example:

```text
Submitted mode: Explore Novel Solution
Detected supporting characteristic: Review Design
Mode note: The request includes design-review characteristics, but the advisory report preserves the submitted exploratory mode as the primary workflow frame.
```

Similarly, if the user leaves the default mode unchanged, EAS receives:

```text
Submitted mode: Solve Problem
```

In that case, the system may proceed with **Solve Problem** as the primary mode, while still noting if the request appears to involve diagnosis, design review, improvement suggestions, or exploratory reasoning.

Example:

```text
Submitted mode: Solve Problem
Detected supporting characteristic: Diagnose Root Cause
Mode note: The request asks for causal analysis, but the submitted mode is Solve Problem. The report may include diagnostic observations while preserving the submitted mode unless implementation logic or user correction changes it.
```

This design makes the input workflow explicit: every EAS request has a submitted mode, and **Solve Problem** is the default when the user does not choose another mode.

---

## 9. Mode and Domain Pack Interaction

Engineering mode and engineering domain are separate but related.

The mode describes the type of task.

The domain describes the technical context.

Example:

```text
Mode: Review Design
Domain: Mechanical Power Transmission
```

This combination tells EAS that it should evaluate a proposed power-transmission design against relevant constraints.

Another example:

```text
Mode: Diagnose Root Cause
Domain: Fluid Power / Hydraulics
```

This combination tells EAS that it should reason about symptoms, failure modes, pressure, flow, and recommended measurements.

The mode influences report structure. The domain influences engineering content.

---

## 10. Mode and Governance Interaction

The selected or default-submitted engineering mode influences how the governance layer interprets the result.

Examples:

* In **Solve Problem** mode, governance may focus on whether the calculation was completed cleanly.
* In **Diagnose Root Cause** mode, governance may focus on whether the diagnosis is evidence-supported or requires further measurements.
* In **Review Design** mode, governance may focus on constraint pass/fail status.
* In **Suggest Improvements** mode, governance may focus on whether recommendations are advisory or computed.
* In **Explore Novel Solution** mode, governance may emphasize uncertainty, assumptions, and validation requirements.

Public-facing governance statuses may include:

```text
computed_clean
computed_selection_pass
computed_with_warnings
computed_with_failure
needs_human_review
```

---

## 11. Report Structure by Mode

Although all EAS reports share a common advisory structure, each mode emphasizes different report sections.

| Mode                       | Report Emphasis                                                  |
| -------------------------- | ---------------------------------------------------------------- |
| **Solve Problem**          | Computation, result, units, assumptions.                         |
| **Diagnose Root Cause**    | Symptoms, likely causes, evidence, recommended checks.           |
| **Review Design**          | Constraints, pass/fail status, rejected options, recommendation. |
| **Suggest Improvements**   | Options, tradeoffs, benefits, risks, next steps.                 |
| **Explore Novel Solution** | Concept, feasibility, assumptions, unknowns, validation path.    |

This mode-specific reporting helps make EAS output more useful and reviewable.

---

## 12. Implementation Status Note

This document describes the public-facing design intent of EAS engineering modes.

Specific behavior should be validated through implementation testing, especially where submitted mode, natural-language request intent, domain-pack selection, deterministic computation, and governance status interact.

The repository should avoid presenting untested behavior as a guaranteed implementation property.

---

## 13. Public Repository Boundary

This document describes the public-facing engineering modes used by EAS.

It does not include:

* Private prompt templates
* Activation schemas
* Backend implementation
* Source code
* Model-routing logic
* Internal mode-selection code
* Internal scoring logic
* Operational logs
* Private engineering pack contents

The purpose of this document is to explain the design intent and workflow role of the EAS engineering modes without exposing proprietary implementation details.

---

## 14. Summary

Engineering modes are a core part of the EAS architecture.

They help EAS transform a submitted engineering request into a structured engineering advisory workflow by identifying the intended purpose of the task.

The five public-facing modes are:

```text
Solve Problem
Diagnose Root Cause
Review Design
Suggest Improvements
Explore Novel Solution
```

A mode is submitted with every EAS request. If the engineer does not manually select a mode, the submitted mode defaults to **Solve Problem**.

Together, these modes allow EAS to support calculation, diagnosis, design review, improvement planning, and exploratory engineering while preserving deterministic validation, governance, and human-review awareness.
