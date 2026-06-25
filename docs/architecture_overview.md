# Architecture Overview

## Engineering Assistance System (EAS)

The **Engineering Assistance System (EAS)** is a governed AI-assisted engineering advisory framework developed by **Synthetic OS Labs**.

EAS is designed to support engineering reasoning, design review, root-cause analysis, deterministic computation, unit validation, constraint checking, and structured advisory reporting.

The system is built around a central architectural principle:

> Language models are useful for interpretation, reasoning, synthesis, and explanation, but engineering calculations and constraint checks should be deterministically validated whenever possible.

EAS is therefore not designed as a simple chatbot or prompt template. It is a layered engineering-assistance workflow that separates interpretation, planning, calculation, validation, governance, and final reporting.

---

## 1. System Purpose

EAS was created to explore how AI systems can assist with engineering tasks while reducing common risks associated with purely generative output.

These risks include:

* Plausible but incorrect calculations
* Unit mismatches
* Missing assumptions
* Unsupported conclusions
* Overconfident recommendations
* Incomplete constraint checks
* Failure to identify when human review is required

EAS addresses these risks by combining language-model reasoning with deterministic computation and explicit governance logic.

The goal is not to replace engineers. The goal is to produce a more reviewable, traceable, and safety-aware engineering advisory workflow.

---

## 2. Design Philosophy

EAS is based on several core design principles.

### 2.1 Separate Reasoning from Computation

Language models are used for understanding the problem, identifying relevant engineering concepts, organizing the workflow, and explaining results.

Deterministic computation is used for mathematical operations, unit-sensitive calculations, pass/fail checks, and constraint comparisons wherever possible.

This separation reduces the risk of accepting unchecked numerical output from a language model.

### 2.2 Make Assumptions Explicit

Engineering problems often contain incomplete information.

EAS is designed to surface assumptions, missing values, unsupported calculations, and review conditions instead of hiding them inside a fluent response.

### 2.3 Treat Units as First-Class Information

Unit handling is central to engineering reliability.

EAS treats units as part of the computational structure rather than as informal text. Unit validation helps identify dimensional inconsistencies, unsupported conversions, and invalid expressions.

### 2.4 Use Governance Before Final Output

The final report is not produced solely from language-model reasoning.

A governance layer evaluates the computation status, constraint results, warnings, failures, and human-review triggers before the advisory report is finalized.

### 2.5 Preserve Human Responsibility

EAS is an assistance system, not a certification authority.

The system is designed to make human-review requirements explicit, especially for safety-critical, regulated, under-specified, or unsupported engineering decisions.

---

## 3. High-Level Workflow

At a public-safe level, EAS follows this workflow:

```text
Engineer Input
    ↓
Problem Interpretation
    ↓
Engineering Mode Selection
    ↓
Domain Pack Selection
    ↓
Structured Planning
    ↓
Deterministic Computation Request
    ↓
Unit Validation and Constraint Checking
    ↓
Governance Gate
    ↓
Engineering Advisory Report
    ↓
Human Review Decision
```

This workflow allows EAS to move from natural-language engineering requests toward structured, reviewable advisory output.

---

## 4. Conceptual System Layers

EAS can be described as a set of conceptual layers.

```text
┌─────────────────────────────────────────────┐
│              Engineer Input Layer           │
└─────────────────────┬───────────────────────┘
                      ↓
┌─────────────────────────────────────────────┐
│          Engineering Mode Selection         │
└─────────────────────┬───────────────────────┘
                      ↓
┌─────────────────────────────────────────────┐
│           Domain Pack Selection Layer       │
└─────────────────────┬───────────────────────┘
                      ↓
┌─────────────────────────────────────────────┐
│              LLM Planning Layer             │
└─────────────────────┬───────────────────────┘
                      ↓
┌─────────────────────────────────────────────┐
│       Deterministic Computation Layer       │
└─────────────────────┬───────────────────────┘
                      ↓
┌─────────────────────────────────────────────┐
│              Unit Validation Layer          │
└─────────────────────┬───────────────────────┘
                      ↓
┌─────────────────────────────────────────────┐
│               Governance Gate               │
└─────────────────────┬───────────────────────┘
                      ↓
┌─────────────────────────────────────────────┐
│        Engineering Advisory Report Layer    │
└─────────────────────┬───────────────────────┘
                      ↓
┌─────────────────────────────────────────────┐
│              Human Review Status            │
└─────────────────────────────────────────────┘
```

---

## 5. Engineer Input Layer

The Engineer Input Layer captures the user’s engineering request.

A request may include:

* Problem statement
* Engineering mode
* Domain or system type
* Known values
* Unknown values
* Units
* Constraints
* Candidate design options
* Symptoms or failure conditions
* Safety-critical context
* Desired output format

Example engineering requests include:

```text
Review this 24 VDC control circuit for wire size, fuse size, and power supply capacity.
```

```text
Determine whether this pump and pipe configuration satisfies the required flow rate.
```

```text
Diagnose why a hydraulic press fixture is producing low clamp force.
```

```text
Evaluate whether this cantilever bracket satisfies stress and deflection limits.
```

The input layer is responsible for receiving the problem context, not for deciding the final answer.

---

## 6. Engineering Mode Selection

EAS supports multiple engineering assistance modes.

| Mode                       | Purpose                                                             |
| -------------------------- | ------------------------------------------------------------------- |
| **Solve Problem**          | Compute or estimate a result from known engineering inputs.         |
| **Diagnose Root Cause**    | Identify likely causes of a failure, symptom, or performance issue. |
| **Review Design**          | Evaluate whether a proposed design satisfies constraints.           |
| **Suggest Improvements**   | Recommend improvements to an existing system or design.             |
| **Explore Novel Solution** | Explore a possible engineering concept or alternative architecture. |

Mode selection affects how EAS structures the workflow, what kind of output is expected, and how the governance layer interprets the result.

For example, a design-review task may emphasize pass/fail constraints, while a root-cause diagnostic task may emphasize likelihood ranking, evidence, and recommended inspections.

---

## 7. Domain Pack Selection Layer

EAS uses domain-oriented engineering packs to provide structured context for different engineering problem classes.

Public-safe examples include:

* Industrial exhaust and airflow
* DC controls and power
* Compressed air and pneumatics
* Fluid pump loops
* Structural and mechanical brackets
* Thermal enclosure cooling
* Aerospace preliminary design
* Aerospace aerodynamics
* Mechanical power transmission

A domain pack may conceptually provide:

* Relevant engineering concepts
* Common variables
* Expected units
* Typical equations
* Common constraints
* Failure modes
* Human-review triggers
* Report expectations

The full internal engineering pack contents are proprietary and are not included in this repository.

---

## 8. LLM Planning Layer

The LLM Planning Layer interprets the engineering request and prepares a structured plan.

This layer may identify:

* What the user is asking
* Which engineering mode applies
* Which domain pack is relevant
* What values are known
* What values are missing
* Which calculations are required
* Which constraints should be checked
* Whether deterministic computation is appropriate
* Whether human review may be required

The LLM Planning Layer is useful for engineering interpretation and workflow organization. However, its mathematical output is not treated as automatically authoritative.

Where possible, structured calculations are routed to the deterministic computation layer.

---

## 9. Deterministic Computation Layer

The Deterministic Computation Layer is one of the central architectural features of EAS.

Its purpose is to compute or validate mathematical portions of the engineering workflow using deterministic methods rather than relying entirely on generated text.

Public-safe capabilities include:

* Structured variable handling
* Equation dependency ordering
* Unit-aware calculation
* Unit conversion
* Constraint checking
* Pass/fail evaluation
* Candidate option comparison
* Computed selection
* Warning generation
* Human-review escalation

This layer helps reduce numerical hallucination by separating engineering computation from language generation.

For example, instead of relying on an LLM to merely state that a design passes, EAS can route structured values and constraints into deterministic checks that return a computed status.

---

## 10. Unit Validation Layer

Engineering calculations are highly sensitive to units.

The Unit Validation Layer checks whether mathematical expressions, variables, and outputs are dimensionally consistent.

This layer may identify issues such as:

* Missing units
* Incompatible units
* Unsupported conversions
* Invalid dimensional relationships
* Ambiguous unit usage
* Unit mismatch between constraint and computed result

When unit validation fails or is incomplete, EAS may produce warnings or trigger human review.

This helps prevent fluent but incorrect engineering output from being accepted without scrutiny.

---

## 11. Governance Gate

The Governance Gate evaluates the result of the planning, computation, unit validation, and constraint-checking stages.

Its purpose is to determine whether the advisory output can be presented as a computed result, a warning-bearing result, a failed design, or a result requiring human review.

Public-facing decision statuses include:

| Status                      | Meaning                                                                       |
| --------------------------- | ----------------------------------------------------------------------------- |
| **computed_clean**          | Deterministic computation completed without required human-review flags.      |
| **computed_selection_pass** | A valid selection was made among multiple options using computed constraints. |
| **computed_with_warnings**  | Computation completed, but warnings, assumptions, or limitations remain.      |
| **computed_with_failure**   | One or more constraints failed or the design was rejected.                    |
| **needs_human_review**      | The result requires qualified human review before reliance.                   |

The Governance Gate helps distinguish between:

* A clean computed result
* A computed result with warnings
* A failed or rejected design
* An under-specified problem
* An unsupported computation
* A safety-sensitive advisory requiring human review

---

## 12. Engineering Advisory Report Layer

The Engineering Advisory Report Layer produces the final user-facing output.

A typical EAS report may include:

* Problem summary
* Engineering mode
* Selected domain pack
* Known inputs
* Missing information
* Assumptions
* Computation summary
* Unit validation notes
* Constraint results
* Recommendation
* Risks and limitations
* Human-review status
* Suggested next validation steps

The report is designed to be structured, reviewable, and traceable.

The goal is not merely to answer the question, but to show how the answer was reached, what was computed, what assumptions were made, and whether the result should be reviewed by a qualified human.

---

## 13. Human Review Status

EAS explicitly reports whether human review is required.

Human review may be required when:

* The problem is safety-critical
* Required information is missing
* Units are invalid or ambiguous
* The computation is unsupported
* The domain is outside the system’s validated scope
* The design involves regulated engineering requirements
* The result depends on assumptions that require confirmation
* The output could affect real-world safety, compliance, construction, manufacturing, aerospace, electrical, or mechanical systems

This explicit human-review status is a key part of the EAS governance philosophy.

---

## 14. Example End-to-End Flow

A simplified design-review workflow may look like this:

```text
Input:
An engineer asks EAS to review a conveyor drive design.

Step 1:
EAS identifies the task as Review Design.

Step 2:
EAS selects the Mechanical Power Transmission domain pack.

Step 3:
EAS extracts known values such as motor speed, gear ratio, pulley diameter,
required belt speed, torque requirement, and horsepower requirement.

Step 4:
EAS identifies the required calculations and constraints.

Step 5:
Structured calculations are routed to the deterministic computation layer.

Step 6:
The deterministic layer computes belt speed, torque, horsepower, and constraint results.

Step 7:
The governance gate evaluates whether the design passes, fails, or requires review.

Step 8:
EAS produces an Engineering Advisory Report with computed results,
constraint status, recommendation, and human-review status.
```

In this workflow, the final answer is not just a generated opinion. It is the result of a structured process that combines AI reasoning, deterministic checking, and governance.

---

## 15. Public Repository Scope

This repository documents the public-safe architecture of EAS.

It may include:

* Architecture summaries
* Workflow descriptions
* Public-safe examples
* Engineering mode descriptions
* Governance status explanations
* Human-review philosophy
* Sanitized validation examples
* Glossary terms

This repository does not include private implementation details.

---

## 16. Proprietary Components Not Included

The following are not included in this repository:

* Source code
* Backend implementation
* Private prompts
* Activation prompts
* Prompt orchestration logic
* Model-routing logic
* Authentication logic
* API keys
* Environment variables
* Operational logs
* Raw engineering reports
* Database schemas
* Full deterministic computation implementation
* Full unit-validation implementation
* Internal engineering pack contents
* Carter or Synthetic OS private internals

This repository is intended to explain the EAS architecture, not provide a cloneable implementation.

---

## 17. Safety and Limitations

EAS is an engineering assistance system.

It is not:

* A licensed professional engineer
* A code-compliance authority
* A certification authority
* A safety approval system
* A substitute for qualified engineering judgment

EAS output should not be used as the sole basis for real-world engineering decisions.

Any safety-critical, regulated, construction, manufacturing, aerospace, electrical, mechanical, or code-compliance decision should be reviewed by qualified professionals.

---

## 18. Summary

EAS is a governed engineering-assistance architecture designed to make AI-supported engineering work more structured, traceable, and reviewable.

Its core architectural contribution is the combination of:

* LLM-based engineering interpretation
* Engineering mode selection
* Domain pack routing
* Deterministic computation
* Unit validation
* Constraint checking
* Governance statuses
* Explicit human-review decisions
* Structured Engineering Advisory Reports

EAS is intended to demonstrate a practical approach to AI-assisted engineering that treats reliability, reviewability, and human responsibility as core architectural requirements.
