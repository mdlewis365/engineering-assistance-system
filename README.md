# Engineering Assistance System (EAS)

**Engineering Assistance System (EAS)** is a governed AI-assisted engineering advisory framework developed by **Synthetic OS Labs**.

EAS combines large language model reasoning, structured engineering workflows, deterministic computation, unit validation, domain-oriented engineering packs, and explicit human-review gates to produce more reliable engineering advisory reports.

This repository is a **public-safe architecture and documentation repository**. It does not contain the private implementation, source code, prompts, model-routing logic, operational logs, authentication logic, or proprietary engineering pack contents used in the private Synthetic OS Labs environment.

---

## Purpose

EAS was created to explore a central question:

> How can AI systems assist with engineering analysis while reducing unchecked numerical hallucination, improving traceability, and preserving appropriate human review?

Rather than treating an LLM response as the final authority, EAS separates engineering assistance into a governed workflow:

1. The engineer provides a structured problem statement.
2. EAS identifies the engineering task type.
3. EAS selects relevant engineering domain context.
4. The language model produces a structured plan.
5. Mathematical and unit-sensitive portions are routed to deterministic computation where possible.
6. A governance layer evaluates the result.
7. EAS produces a structured Engineering Advisory Report.
8. Human-review status is explicitly shown.

The goal is not to replace engineers. The goal is to create a safer AI-assisted workflow for engineering reasoning, computation checking, and design review.

---

## Core Design Philosophy

EAS is based on several design principles:

* **AI should not be trusted blindly for engineering math.**
* **Language reasoning and deterministic computation should be separated where possible.**
* **Engineering outputs should include assumptions, limitations, and review status.**
* **Unit validation is essential for engineering reliability.**
* **Missing information should be surfaced, not hidden.**
* **Human review should be explicit, not implied.**
* **Domain context should be structured and selected intentionally.**

EAS is therefore more than a prompting pattern. It is an AI engineering architecture intended to combine stochastic reasoning with deterministic verification.

---

## High-Level Architecture

At a public-safe level, EAS consists of the following conceptual layers:

```text
Engineer Input Layer
        ↓
Mode Selection Layer
        ↓
Domain Pack Selection Layer
        ↓
LLM Planning Layer
        ↓
Deterministic Computation Layer
        ↓
Unit Validation Layer
        ↓
Governance Gate
        ↓
Engineering Advisory Report
        ↓
Human Review Decision
```

Each layer has a distinct responsibility.

The language model is used for interpretation, planning, explanation, and advisory synthesis. Deterministic computation is used where structured calculations, unit checks, pass/fail evaluations, and constraint comparisons are required.

---

## Engineering Modes

EAS supports multiple engineering assistance modes:

| Mode                       | Purpose                                                      |
| -------------------------- | ------------------------------------------------------------ |
| **Solve Problem**          | Compute or estimate an engineering result from known inputs. |
| **Diagnose Root Cause**    | Analyze symptoms and identify likely failure causes.         |
| **Review Design**          | Evaluate whether a proposed design satisfies constraints.    |
| **Suggest Improvements**   | Recommend design or system improvements.                     |
| **Explore Novel Solution** | Explore a possible engineering approach or concept.          |

These modes help EAS adapt its reasoning style, output structure, and review criteria to the engineering task.

---

## Deterministic Computation Layer

A major feature of EAS is its deterministic computation layer.

This layer is designed to reduce unchecked numerical hallucination by validating or computing mathematical portions of an engineering workflow outside of the language model whenever possible.

Public-safe capabilities include:

* Structured variable handling
* Equation dependency ordering
* Unit validation
* Unit conversion
* Constraint checking
* Pass/fail evaluation
* Selection logic
* Sensitivity notes
* Human-review escalation when computation is unsupported or under-specified

This layer is especially important because LLMs can produce plausible-looking engineering calculations that are numerically or dimensionally incorrect. EAS treats that risk as an architectural concern.

---

## Governance Gate

EAS includes a governance layer that evaluates the result before the final advisory report is presented.

Public-facing decision statuses include:

| Status                      | Meaning                                                                       |
| --------------------------- | ----------------------------------------------------------------------------- |
| **computed_clean**          | Deterministic computation completed without required human-review flags.      |
| **computed_selection_pass** | A valid selection was made among multiple options using computed constraints. |
| **computed_with_warnings**  | Computation completed, but warnings or assumptions remain.                    |
| **computed_with_failure**   | One or more constraints failed or a design was rejected.                      |
| **needs_human_review**      | The result requires engineering review before reliance.                       |

The governance gate helps EAS distinguish between a confident computed result, a warning-bearing advisory, a failed design, and an under-specified or unsupported problem.

---

## Engineering Packs

EAS uses domain-oriented engineering packs to provide structured context for different classes of engineering problems.

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

These packs help guide the workflow by identifying relevant equations, common constraints, expected inputs, output expectations, and human-review triggers.

The full internal engineering pack contents are proprietary and are not included in this repository.

---

## Engineering Advisory Report

EAS produces a structured Engineering Advisory Report rather than an unstructured chat response.

A typical report may include:

* Problem summary
* Known inputs
* Missing information
* Assumptions
* Selected engineering mode
* Selected domain pack
* Computation summary
* Unit validation notes
* Constraint results
* Recommendation
* Risks and limitations
* Human-review status
* Suggested next validation steps

This structure is intended to improve traceability, reviewability, and engineering usefulness.

---

## Example Workflow

A simplified EAS workflow may look like this:

```text
User submits:
"Review this 24 VDC control circuit and determine whether the wire size,
fuse size, and power supply are appropriate."

EAS workflow:
1. Identify mode: Review Design
2. Select domain pack: DC Controls / Power
3. Extract known values and constraints
4. Identify required calculations
5. Route calculations to deterministic computation
6. Validate units
7. Check constraints
8. Apply governance decision
9. Produce Engineering Advisory Report
10. Display human-review status
```

The result is not merely an LLM opinion. It is a governed advisory workflow that separates interpretation, computation, validation, and final reporting.

---

## Repository Contents

```text
engineering-assistance-system/
├── README.md
├── LICENSE
├── NOTICE.md
├── docs/
│   ├── architecture_overview.md
│   ├── platform_context.md
│   ├── engineer_input_workflow.md
│   ├── engineering_modes.md
│   ├── deterministic_computation_layer.md
│   ├── governance_gate.md
│   ├── engineering_packs.md
│   ├── output_report_structure.md
│   ├── workflow_example.md
│   ├── validation_examples.md
│   ├── limitations_and_human_review.md
│   └── glossary.md
└── examples/
    ├── sanitized_engineering_request.md
    ├── sanitized_advisory_report.md
    └── sanitized_validation_trace.md
```

This repository may evolve as additional public-safe documentation is prepared.

---

## What Is Included

This repository may include:

* Public-safe architecture summaries
* Conceptual workflow documentation
* Sanitized examples
* Engineering mode descriptions
* Governance status explanations
* Human-review philosophy
* Public-facing system context
* High-level validation examples

---

## What Is Not Included

This repository does **not** include:

* Private source code
* Backend implementation
* Private prompts
* Activation prompts
* Model-routing logic
* Authentication logic
* Operational logs
* API keys or environment variables
* Database schemas
* Raw engineering reports
* Full deterministic computation implementation
* Full internal engineering pack contents
* Carter or Synthetic OS private internals

The purpose of this repository is to document the public-safe architecture and design philosophy of EAS, not to provide a cloneable implementation.

---

## Relationship to Synthetic OS Labs

EAS is part of a broader private research environment developed by **Synthetic OS Labs**.

Within that environment, EAS serves as an engineering-assistance workflow focused on structured engineering reasoning, deterministic validation, and governed advisory reporting.

This public repository describes EAS only at a high level. The private Synthetic OS Labs platform, Carter-related systems, source code, model integrations, memory systems, authentication mechanisms, and internal runtime environment are not included.

---

## Safety and Limitations

EAS is an engineering assistance system. It is not a licensed professional engineer, certification authority, code-compliance authority, or safety approval system.

EAS output should not be used as the sole basis for real-world engineering decisions.

Any real-world engineering design, safety-critical decision, manufacturing decision, construction decision, aerospace decision, electrical installation, mechanical system change, or regulated engineering activity should be reviewed by qualified professionals.

EAS is designed to support engineering reasoning, not replace engineering responsibility.

---

## Development Status

EAS is an active Synthetic OS Labs research and development project.

This repository represents a public documentation snapshot of the system architecture, design intent, and engineering philosophy.

---

## Author

**Michael D. Lewis**
Founder, Synthetic OS Labs
AI Systems Engineer / Computer Science Graduate / U.S. Navy Veteran

---

## License

This repository is licensed under the **BSD 3-Clause License** for the public documentation contained here.

The underlying Engineering Assistance System, Synthetic OS Labs platform, Carter integrations, private prompts, source code, model-routing logic, deterministic computation implementation, validation logic, operational logs, authentication systems, and internal engineering packs remain proprietary.

No patent, trademark, trade secret, implementation, deployment, or commercial system rights are granted by this repository.

See `LICENSE` and `NOTICE.md` for details.
