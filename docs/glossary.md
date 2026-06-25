# Glossary

## Engineering Assistance System (EAS)

This glossary defines public-facing terms used in the **Engineering Assistance System (EAS)** documentation.

The purpose of this glossary is to make the repository easier to understand for reviewers, recruiters, engineers, researchers, and technical stakeholders.

These definitions are public-safe and conceptual. They do not expose private source code, prompts, schemas, implementation details, model-routing logic, internal validation rules, or proprietary engineering pack contents.

---

## Advisory Output

An output intended to support engineering reasoning, review, diagnosis, or decision preparation.

Advisory output is not certification, approval, professional engineering sign-off, code-compliance verification, or final design authority.

---

## Assumption

A stated condition used to complete an advisory workflow when some information is missing or simplified.

Example:

```text
Assumption:
Belt slip is neglected for this preliminary conveyor speed calculation.
```

Assumptions should be made explicit in the Engineering Advisory Report.

---

## Candidate Option

One of multiple design, component, or configuration choices being evaluated by EAS.

Example:

```text
Option A: Pipe A + Pump P-1
Option B: Pipe B + Pump P-2
Option C: Pipe C + Pump P-3
```

Candidate options may be compared using constraints, cost, performance, capacity, or other selection criteria.

---

## Constraint

A requirement or limit used to evaluate whether a computed value, design, or candidate option passes or fails.

Examples:

```text
Voltage drop must be less than 5%.
Belt speed must be between 75 and 85 ft/min.
Power supply loading must not exceed 80%.
Tip deflection must be less than L/180.
```

Constraints are central to design review and governance.

---

## Constraint Checking

The process of comparing computed or observed values against stated engineering requirements.

Example:

```text
Computed belt speed: 61.18 ft/min
Required belt speed: 75–85 ft/min
Result: Fail
```

Constraint checking helps EAS avoid presenting a completed calculation as a successful design when the design actually fails a requirement.

---

## Computation Status

A status describing whether deterministic computation was completed, partial, unsupported, or blocked by an error or review condition.

Public-facing examples include:

```text
computed
partial
unsupported
needs_human_review
error
```

Computation status is not necessarily the same as final governance status.

---

## computed_clean

A public-facing governance status indicating that deterministic computation completed without required human-review flags or unresolved warnings.

Example meaning:

```text
Computation status: computed
Unit validation: pass
Constraint status: pass
Warnings: none
Governance status: computed_clean
```

This does not mean the design is professionally certified. It means EAS completed the advisory workflow cleanly under the provided assumptions and supported scope.

---

## computed_selection_pass

A public-facing governance status indicating that EAS evaluated multiple candidate options and selected a valid option using computed constraints and a selection rule.

Example:

```text
Selection rule:
Select the lowest-cost option among candidates that pass all required constraints.

Result:
Option B is selected because it is the lowest-cost passing candidate.
```

---

## computed_with_failure

A public-facing governance status indicating that deterministic computation completed, but one or more required constraints failed or the proposed design/configuration was rejected.

Example:

```text
Computed belt speed: 61.18 ft/min
Required belt speed: 75–85 ft/min
Governance status: computed_with_failure
```

A completed computation can still produce a failed design result.

---

## computed_with_warnings

A public-facing governance status indicating that deterministic computation completed, but warnings, assumptions, missing information, or limitations remain.

Example:

```text
Governance status: computed_with_warnings
Warnings:
- Ambient temperature was assumed.
- Manufacturer derating data was not provided.
```

This status helps prevent warning-bearing results from being presented as fully clean.

---

## Deterministic Computation

Computation performed through structured, repeatable calculation logic rather than relying only on generated language-model output.

In EAS, deterministic computation is used where possible for:

* Arithmetic
* Unit-sensitive calculations
* Constraint checks
* Pass/fail evaluation
* Candidate option comparison
* Selection logic

---

## Deterministic Computation Layer

The EAS architectural layer responsible for structured calculation, unit-aware validation, constraint checking, and computed status generation where deterministic computation is applicable.

Within the private EAS implementation, this capability is represented by the **Math Computation Module (MCM)**.

---

## Domain Pack

A structured engineering context pack used to help EAS interpret a technical problem.

A domain pack may conceptually provide:

* Relevant engineering concepts
* Expected variables
* Typical units
* Common constraints
* Failure modes
* Report expectations
* Human-review triggers

The full private contents of EAS domain packs are proprietary and are not included in this public repository.

---

## EAS

**Engineering Assistance System.**

EAS is a governed AI-assisted engineering advisory framework developed by Synthetic OS Labs.

It combines:

* Submitted engineering modes
* Engineering pack selection
* LLM-based interpretation
* Deterministic computation where applicable
* Unit validation
* Constraint checking
* Governance statuses
* Human-review signaling
* Structured Engineering Advisory Reports

---

## Engineering Advisory Report

The final structured user-facing report produced by EAS.

A typical report may include:

* Problem summary
* Submitted engineering mode
* Selected engineering pack
* Known inputs
* Missing information
* Assumptions
* Computation summary
* Unit validation notes
* Constraint results
* Recommendation
* Risks and limitations
* Governance status
* Human-review status
* Suggested next validation steps

The report is advisory and does not represent professional certification or approval.

---

## Engineering Mode

The submitted task type for an EAS request.

A mode is submitted with every EAS request. If the engineer does not manually select a mode, the submitted mode defaults to **Solve Problem**.

Public-facing modes include:

```text
Solve Problem
Diagnose Root Cause
Review Design
Suggest Improvements
Explore Novel Solution
```

The submitted mode helps frame the report structure, computation strategy, and governance interpretation.

---

## Engineering Pack

A public-safe term for structured domain or technical context used by EAS.

Current public-safe EAS packs include:

```text
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

Engineering packs help EAS produce domain-aware advisory reports.

---

## Explore Novel Solution

An EAS engineering mode used for exploratory engineering concepts, alternative architectures, or unconventional solution paths.

This mode emphasizes:

* Concept framing
* Feasibility discussion
* Assumptions
* Risks
* Unknowns
* Validation path
* Human-review requirements

Exploratory output should not be treated as validated design authority.

---

## Failure Condition

A warning or result indicating that a required constraint failed or that the advisory workflow could not safely produce a clean result.

Examples:

```text
constraint_failed
invalid_unit
no_passing_candidate
unsupported_equation
missing_critical_input
```

Failure conditions are evaluated by the Governance Gate.

---

## Governance Gate

The EAS reliability and review layer that evaluates computation status, unit validation, constraint results, warnings, failures, missing information, safety concerns, and human-review triggers before the final Engineering Advisory Report is presented.

The Governance Gate helps classify the advisory result as clean, warning-bearing, failed, selection-based, or requiring human review.

---

## Governance Status

A public-facing advisory classification assigned after the Governance Gate evaluates the result.

Public-facing governance statuses include:

```text
computed_clean
computed_selection_pass
computed_with_warnings
computed_with_failure
needs_human_review
```

Governance statuses are advisory classifications, not certifications or approvals.

---

## Human Review

Qualified human evaluation of an EAS advisory result before reliance, implementation, deployment, or real-world use.

Human review may be required when:

* Inputs are missing
* Units are ambiguous
* The computation is unsupported
* Constraints fail
* The system is safety-critical
* The decision is regulated
* The output affects production, safety, compliance, security, or real-world operation

Human review is a core feature of the EAS governance philosophy.

---

## Human Review: Not Required

A report-level signal indicating that EAS did not identify required human-review triggers under the provided assumptions and supported scope.

This does not mean the result is certified, professionally approved, or guaranteed safe.

---

## Human Review: Required

A report-level signal indicating that the advisory result should not be relied on without qualified human review.

This may occur because of missing information, failed constraints, safety-sensitive context, unsupported computation, ambiguous units, or regulated real-world implications.

---

## Known Inputs

Values, facts, constraints, system details, measurements, or observations provided by the engineer.

Example:

```text
Motor speed: 1,750 rpm
Gear ratio: 20:1
Pulley diameter: 2.67 in
Required belt speed range: 75–85 ft/min
```

Known inputs form the basis of the advisory report.

---

## LLM Planning Layer

The EAS layer that uses language-model reasoning to interpret the engineering request, identify relevant variables, organize the workflow, identify possible calculations, and prepare the advisory structure.

The LLM Planning Layer supports interpretation and planning, but deterministic computation is used where applicable for mathematical and unit-sensitive operations.

---

## Math Computation Module (MCM)

The private EAS component that represents the deterministic computation capability.

At a public-safe conceptual level, MCM supports:

* Structured engineering calculations
* Unit-aware validation
* Unit conversion where supported
* Constraint checking
* Candidate option evaluation
* Pass/fail result generation
* Computation status generation
* Warning and review escalation

MCM source code, parser logic, internal schemas, equation handlers, unit algebra, validation tests, operational traces, and implementation details are proprietary and are not included in this public repository.

---

## Missing Information

Information that was not provided but may be required to complete a reliable advisory result.

Examples:

```text
Material yield strength
Safety factor
Ambient temperature
Pump curve
Service factor
Startup torque
Deployment logs
Manufacturer derating data
```

Missing information may trigger warnings or human-review requirements.

---

## Mode Submission

The process by which an engineering mode is included with every EAS request.

If the engineer does not manually select a mode, the submitted mode defaults to:

```text
Solve Problem
```

If the engineer selects another mode, such as **Review Design** or **Explore Novel Solution**, that selected mode is submitted as the primary workflow frame.

---

## needs_human_review

A public-facing governance status indicating that the advisory result requires qualified human review before reliance.

This status may apply when:

* Critical information is missing
* Units are invalid or ambiguous
* The calculation is unsupported
* The context is safety-critical
* The request is regulated or code-governed
* The output could affect real-world systems
* The result depends on assumptions requiring professional confirmation

---

## Pack Selection

The process of identifying the engineering pack most relevant to the submitted request.

Pack selection may consider:

* Request wording
* Submitted engineering mode
* Domain-specific variables
* Units
* Constraints
* Failure symptoms
* Desired output
* Safety context

Pack selection is advisory routing, not proof that the problem is fully understood.

---

## Pass/Fail Evaluation

The process of determining whether a computed value, observed value, design, or candidate option satisfies a stated constraint.

Example:

```text
Computed power supply loading: 75%
Maximum allowed loading: 80%
Result: Pass
```

Pass/fail evaluation is especially important in **Review Design** mode.

---

## Recommendation

The advisory conclusion produced by EAS after considering known inputs, assumptions, computations, constraints, warnings, and governance status.

A recommendation should be consistent with the report’s evidence and should not present warning-bearing or human-review-required results as final approval.

---

## Review Design

An EAS engineering mode used to evaluate whether a proposed design, configuration, component, or option satisfies stated constraints.

This mode emphasizes:

* Proposed design values
* Constraints
* Computed results
* Pass/fail evaluation
* Rejected options
* Recommendation
* Human-review status

---

## Risk or Limitation

A condition that may reduce confidence in the advisory result or require further review.

Examples:

```text
Belt slip was not modeled.
Startup torque was not provided.
Manufacturer ratings were not checked.
Production logs were incomplete.
Aerospace safety requirements were not evaluated.
```

Risks and limitations should be clearly surfaced in the report.

---

## Safety-Critical Context

Any engineering or software context where failure could harm people, damage property, affect regulated systems, disrupt production, compromise security, or create unacceptable risk.

Examples include:

* Electrical systems
* Structural supports
* Pressure systems
* Moving machinery
* Aerospace systems
* Production software
* Security-sensitive software
* AI systems affecting consequential decisions

Safety-critical context may trigger human review.

---

## Selected Engineering Pack

The engineering pack chosen as the primary technical context for an EAS request.

Example:

```text
Selected Engineering Pack:
Mechanical Power Transmission
```

The selected pack influences variables, expected calculations, warnings, report emphasis, and human-review considerations.

---

## Solve Problem

The default submitted EAS engineering mode.

**Solve Problem** is used when the engineer wants EAS to compute, estimate, or determine an engineering result from known inputs.

If the engineer does not manually choose another mode, EAS receives **Solve Problem** as the submitted mode.

---

## Software Systems Engineering Pack

An EAS engineering pack that supports software architecture, debugging, reliability, integration, deployment, observability, security, and AI/software workflow review.

This pack may be used for requests involving:

* Backend architecture
* APIs
* State management
* Error logs
* Runtime failures
* Deployment behavior
* Security-sensitive design
* Observability
* AI system orchestration
* Test and validation planning

Not every software systems request requires numeric deterministic computation.

---

## Structured Advisory Workflow

The staged EAS process that transforms an engineering request into an Engineering Advisory Report.

A public-safe workflow may include:

```text
Engineer Input
Submitted Engineering Mode
Engineering Pack Selection
LLM Planning Layer
Deterministic Computation Layer / MCM, when applicable
Unit Validation, when applicable
Constraint Checking
Governance Gate
Engineering Advisory Report
Human Review Status
```

---

## Submitted Engineering Mode

The engineering mode received by EAS for a request.

A submitted engineering mode is always present. If the user does not manually choose a mode, the submitted mode defaults to **Solve Problem**.

---

## Suggest Improvements

An EAS engineering mode used when the engineer wants recommendations for improving an existing design, system, process, or configuration.

This mode emphasizes:

* Current limitations
* Improvement options
* Tradeoffs
* Risks
* Implementation considerations
* Validation steps
* Human-review status

---

## Unit Validation

The process of checking whether units are present, compatible, and dimensionally appropriate for a calculation or constraint.

Examples:

```text
Motor speed: rpm
Pulley diameter: inches
Computed belt speed: ft/min
Required belt speed: ft/min
Unit validation: pass
```

Unit validation helps prevent plausible but invalid engineering output.

---

## Unsupported Computation

A requested calculation or validation that is outside the supported deterministic scope.

Unsupported computation may occur when:

* The equation is not supported
* Units are unsupported
* Required variables are missing
* The domain requires advanced simulation
* The result depends on unavailable real-world data
* The calculation requires professional standards or manufacturer-specific methods

Unsupported computation may trigger warnings or human review.

---

## Warning

A report condition indicating that the advisory result depends on an assumption, missing information, partial computation, uncertain unit, unsupported detail, or other limitation.

Examples:

```text
missing_input
missing_unit
ambiguous_value
unsupported_conversion
unsafe_assumption
requires_human_review
```

Warnings should be visible in the Engineering Advisory Report.

---

## Public Repository Boundary

This glossary defines public-facing terms for the EAS documentation repository.

It does not include:

* Private source code
* Backend implementation
* Private prompts
* Activation prompts
* Prompt contracts
* Internal schemas
* Full MCM implementation
* Full governance rules
* Full engineering pack contents
* Model-routing logic
* Operational logs
* Raw engineering reports
* Carter or Synthetic OS private internals

The definitions are intended to explain the EAS architecture and documentation language without exposing proprietary implementation details.
