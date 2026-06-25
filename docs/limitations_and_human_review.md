# Limitations and Human Review

## Engineering Assistance System (EAS)

The **Engineering Assistance System (EAS)** is a governed AI-assisted engineering advisory framework. It is designed to support engineering reasoning, structured analysis, deterministic computation where applicable, unit validation, constraint checking, and advisory report generation.

EAS is not a replacement for qualified engineering judgment.

This document describes the public-facing limitations of EAS and explains when human review is required.

The guiding principle is:

> AI-assisted engineering should support human judgment, not replace human responsibility.

---

## 1. Purpose of This Document

This document defines the public-safe limitations and human-review philosophy of EAS.

It explains:

* What EAS is intended to do
* What EAS is not intended to do
* Why human review matters
* When human review may be required
* How EAS communicates uncertainty
* How governance statuses relate to review requirements
* Why advisory output should not be treated as certification or approval

This document is intentionally conservative. Engineering systems can affect real-world safety, reliability, compliance, cost, production, and human well-being.

---

## 2. EAS Is an Advisory System

EAS produces **Engineering Advisory Reports**.

These reports are intended to support:

* Engineering reasoning
* Early-stage analysis
* Design review
* Root-cause diagnosis
* Improvement planning
* Exploratory engineering thinking
* Deterministic computation where applicable
* Constraint checking where supported
* Human-review preparation

EAS output should be treated as advisory assistance.

It should not be treated as final engineering authority.

---

## 3. What EAS Is Not

EAS is not:

* A licensed professional engineer
* A code-compliance authority
* A certification authority
* A safety approval system
* A regulatory approval system
* A manufacturing release authority
* A construction approval authority
* An airworthiness authority
* An electrical inspection authority
* A cybersecurity certification authority
* A substitute for qualified engineering judgment
* A guarantee that a design is safe, compliant, complete, or commercially viable

EAS can assist with reasoning and review, but it does not assume professional, legal, regulatory, or safety responsibility for real-world engineering decisions.

---

## 4. Why Human Review Matters

Engineering decisions often depend on context that may not be fully captured in a user request.

Examples include:

* Real-world installation conditions
* Material properties
* Manufacturer ratings
* Environmental conditions
* Regulatory requirements
* Safety factors
* Failure consequences
* Maintenance procedures
* Human interaction with equipment
* Production constraints
* Security and privacy requirements
* Test results
* Inspection findings
* Local codes and standards

Even when EAS performs deterministic computation, the result depends on the correctness and completeness of the provided inputs.

A calculation may be mathematically correct while the engineering conclusion remains incomplete or unsafe.

---

## 5. Core Limitations

### 5.1 Input Dependence

EAS depends on the information provided by the user.

If the input is incomplete, ambiguous, inaccurate, outdated, or missing critical details, the advisory report may be incomplete or unreliable.

Examples:

```text id="nq4ewn"
Missing material properties
Missing load cases
Missing wire length
Missing pump curve
Missing environmental conditions
Missing software logs
Missing safety factor
Missing manufacturer derating data
```

EAS should surface missing information rather than silently hiding it.

---

### 5.2 Unit and Dimensional Limitations

Engineering calculations depend heavily on correct units.

EAS may detect missing, ambiguous, incompatible, or unsupported units. However, EAS cannot guarantee that all user-provided units are correct or that all real-world unit assumptions have been captured.

Human review may be required when:

* Units are missing
* Units are ambiguous
* Units appear incompatible
* A unit conversion is unsupported
* A dimensional relationship is unclear
* The user-provided unit may not match the real-world measurement

---

### 5.3 Domain Scope Limitations

EAS uses engineering packs to provide domain-aware context, but no pack covers every possible engineering condition.

Current public-safe EAS packs include:

```text id="2wdoh6"
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

These packs provide structured context, but they do not replace domain experts, detailed standards, manufacturer documentation, simulation, inspection, testing, or professional review.

---

### 5.4 Deterministic Computation Limitations

The Math Computation Module (MCM) supports deterministic computation where applicable.

However, deterministic computation has limits.

MCM may not support every equation, unit conversion, domain-specific standard, material model, numerical method, or real-world design scenario.

Human review may be required when:

* The computation is unsupported
* The equation path is uncertain
* Inputs are incomplete
* The calculation depends on unstated assumptions
* The domain requires advanced simulation or empirical validation
* The result affects safety-critical or regulated systems

MCM can improve reliability, but it does not make EAS a final engineering authority.

---

### 5.5 LLM Reasoning Limitations

EAS uses language-model reasoning for interpretation, planning, synthesis, and explanation.

Language models can be useful, but they can also:

* Misinterpret user intent
* Select an incomplete reasoning path
* Miss an important constraint
* Overgeneralize from limited information
* Produce plausible but unsupported explanations
* Fail to identify a safety or compliance issue
* Mischaracterize uncertainty

EAS reduces some of these risks through structure, deterministic computation, unit validation, governance, and human-review signaling, but the risks are not eliminated.

---

### 5.6 Report Completeness Limitations

An EAS report is based on available information and supported workflow logic.

It may not include every relevant real-world factor.

Examples of factors that may be outside the report include:

* Local codes and regulations
* Manufacturer-specific design rules
* Installation quality
* Maintenance condition
* Material defects
* Environmental exposure
* Human factors
* Fatigue behavior
* Transient loads
* Cybersecurity threats
* Production-specific constraints
* Failure history
* Inspection findings

A structured report is more reviewable than an unstructured answer, but it is still advisory.

---

## 6. Human Review Status

EAS may display a human-review decision in the final report.

Public-facing examples:

```text id="m5m7h2"
Human Review: Not Required
```

```text id="d0jco2"
Human Review: Required
```

This status indicates whether the advisory result appears to require qualified human review before reliance.

Even when a report states **Human Review: Not Required**, the output remains advisory and should not be treated as professional certification, approval, or final design authority.

---

## 7. Governance Status and Review Meaning

EAS may use public-facing governance statuses such as:

| Governance Status           | Meaning                                                                                         |
| --------------------------- | ----------------------------------------------------------------------------------------------- |
| **computed_clean**          | Deterministic computation completed without required human-review flags or unresolved warnings. |
| **computed_selection_pass** | A valid selection was made among candidate options using computed constraints.                  |
| **computed_with_warnings**  | Computation completed, but warnings, assumptions, or limitations remain.                        |
| **computed_with_failure**   | One or more constraints failed, or the design/configuration was rejected.                       |
| **needs_human_review**      | The result requires qualified human review before reliance.                                     |

These statuses are advisory classifications.

They are not certifications, approvals, warranties, or guarantees.

---

## 8. When Human Review Is Required

Human review should be required when the output may affect safety, compliance, production, deployment, or real-world operation.

Common human-review triggers include:

* Safety-critical systems
* Regulated engineering decisions
* Electrical installation
* Structural support
* Pressure systems
* Pneumatics or hydraulics
* Moving machinery
* Aerospace systems
* Fire, ventilation, or life-safety systems
* Human-occupied environments
* Manufacturing release
* Physical deployment
* Production software systems
* Security-sensitive software
* Privacy-sensitive software
* AI systems affecting user decisions or business operations
* Missing critical information
* Unsupported computation
* Ambiguous units
* Failed constraints
* Conflicting assumptions
* Request for certification, approval, or final authority

Human review is not a weakness of EAS. It is part of the governance design.

---

## 9. Safety-Critical Engineering Review

Some engineering areas require especially cautious review.

### 9.1 Electrical Systems

Human review may be required when a request involves:

* Wire sizing
* Fuse or breaker selection
* Fire risk
* Power supply protection
* Equipment safety
* Field installation
* Code compliance
* Control-system reliability

EAS may assist with advisory calculations, but real electrical work should be reviewed by qualified personnel.

---

### 9.2 Structural and Mechanical Systems

Human review may be required when a request involves:

* Brackets
* Supports
* Overhead loads
* Machinery
* Rotating equipment
* Welds or fasteners
* Load paths
* Safety factors
* Fatigue or dynamic loading

A simplified stress or deflection calculation does not certify a real-world structure.

---

### 9.3 Fluid Power, Pneumatics, and Pressure Systems

Human review may be required when a request involves:

* Hydraulic pressure
* Pneumatic actuators
* Stored energy
* Clamping systems
* Pressure vessels
* Fluid hazards
* Hot or chemical fluids
* Lockout/tagout procedures

Pressure systems can be hazardous even when calculations appear straightforward.

---

### 9.4 Aerospace Systems

Human review is expected when a request involves:

* Aircraft
* Drones
* Flight vehicles
* Aerodynamics
* Flight safety
* Airworthiness
* Regulatory compliance
* Propulsion
* Structural flight components
* Flight testing

EAS may support preliminary reasoning, but aerospace output should not be treated as validated design authority.

---

### 9.5 Software Systems Engineering

Human review may be required when a request involves:

* Production software
* Sensitive data
* Security or access control
* Privacy requirements
* AI system behavior
* Reliability-critical services
* Data integrity
* Deployment failures
* Business-critical workflows
* Software controlling physical systems

Software advisory output may need engineering review, security review, privacy review, QA review, or operational review depending on the context.

---

## 10. Examples of Human-Review Escalation

### 10.1 Missing Structural Data

```text id="fej056"
Problem:
Review whether a cantilever bracket is safe for installation.

Missing information:
- Material yield strength
- Cross-section dimensions
- Mounting method
- Safety factor
- Load case

Governance result:
needs_human_review
```

Reason:

```text id="o210qb"
Critical structural information is missing, and the result may affect real-world safety.
```

---

### 10.2 Unit Ambiguity

```text id="8m49yq"
Problem:
Calculate airflow velocity.

Input:
Opening size = 24

Issue:
The unit and geometry are ambiguous.

Governance result:
needs_human_review
```

Reason:

```text id="hbwk9x"
The calculation cannot be trusted without knowing whether the opening is a diameter,
area, rectangular dimension, or another measurement.
```

---

### 10.3 Design Constraint Failure

```text id="kzmbdy"
Problem:
Review conveyor belt speed.

Computed result:
61.18 ft/min

Requirement:
75–85 ft/min

Governance result:
computed_with_failure
```

Reason:

```text id="y994xl"
The computation completed, but the design fails the stated speed requirement.
```

---

### 10.4 Warning-Bearing Thermal Estimate

```text id="83jc48"
Problem:
Estimate enclosure cooling requirement.

Warnings:
- Ambient temperature not provided
- Solar loading not provided
- Manufacturer derating data not provided

Governance result:
computed_with_warnings
```

Reason:

```text id="emgn98"
The estimate may be useful for early review, but final thermal design requires missing data.
```

---

### 10.5 Software Production Failure

```text id="iyvmws"
Problem:
Diagnose intermittent backend failure in production.

Warnings:
- Logs are incomplete
- Deployment environment differs from local environment
- Failure cannot be reproduced reliably

Governance result:
computed_with_warnings or needs_human_review
```

Reason:

```text id="d9mgmn"
The diagnostic reasoning may identify likely causes, but production changes require engineering review and validation.
```

---

## 11. Human Review Is Not a Failure

Human-review escalation should not be interpreted as system failure.

It may indicate that EAS is behaving responsibly.

A responsible engineering advisory system should be able to say:

```text id="1skq8d"
The information is incomplete.
The units are ambiguous.
The calculation is unsupported.
The design fails a constraint.
The context is safety-critical.
Qualified review is required.
```

This is preferable to giving an overconfident answer that hides uncertainty.

---

## 12. User Responsibility

Users are responsible for:

* Providing accurate inputs
* Confirming units
* Confirming assumptions
* Reviewing missing information
* Validating outputs before use
* Consulting qualified professionals when required
* Following applicable codes, standards, laws, and safety procedures
* Testing and inspecting real-world systems
* Ensuring that advisory output is not treated as final authority

EAS can support analysis, but the user remains responsible for decisions made from that analysis.

---

## 13. Public Repository Boundary

This document describes the public-safe limitations and human-review philosophy of EAS.

It does not include:

* Private source code
* Backend implementation
* Private prompts
* Activation prompts
* Prompt contracts
* Internal schemas
* Full governance rules
* Full MCM implementation
* Internal safety logic
* Operational logs
* Raw engineering reports
* Private engineering pack contents
* Carter or Synthetic OS private internals

The goal is to explain EAS limitations and review posture without exposing proprietary implementation details.

---

## 14. Implementation Status Note

This document describes the public-facing design intent of EAS limitations and human-review behavior.

Specific human-review triggers, governance status transitions, warning rules, safety flags, report wording, and domain-specific escalation behavior should be validated against the private EAS implementation and test suite.

The public repository should avoid presenting untested behavior as a guaranteed implementation property.

---

## 15. Summary

EAS is designed to support engineering analysis, not replace engineering responsibility.

Its limitations include:

* Dependence on user-provided inputs
* Unit ambiguity risk
* Domain scope limits
* Deterministic computation scope limits
* LLM reasoning limitations
* Missing real-world context
* Need for qualified review in safety-critical or regulated situations

The human-review mechanism is a core feature of the EAS architecture.

The central belief is:

> A trustworthy AI-assisted engineering system should know when to compute, when to warn, when to fail a design, and when to require human review.
