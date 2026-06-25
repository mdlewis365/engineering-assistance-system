# Engineer Input Workflow

## Engineering Assistance System (EAS)

The **Engineer Input Workflow** defines how an engineering request enters the Engineering Assistance System (EAS) and is transformed into a structured advisory process.

EAS is designed to support engineering reasoning, computation, design review, root-cause analysis, improvement suggestions, and human-review decisions. To do this reliably, the system requires the engineering request to be interpreted in a structured way before computation or report generation occurs.

The input workflow is based on a simple principle:

> Better engineering input produces better engineering advisory output.

---

## 1. Purpose of the Input Workflow

The purpose of the Engineer Input Workflow is to help EAS identify:

* What engineering problem is being asked
* Which engineering mode applies
* Which domain context is relevant
* What information is known
* What information is missing
* Which calculations may be required
* Which units and constraints must be checked
* Whether deterministic computation is possible
* Whether human review may be required

The workflow helps convert a natural-language engineering request into a structured engineering analysis process.

---

## 2. Input Workflow Overview

At a public-safe level, the input workflow follows this sequence:

```text id="i9jwzk"
Engineer Request
      ↓
Problem Statement Extraction
      ↓
Engineering Mode Identification
      ↓
Domain Context Identification
      ↓
Known Values and Units Extraction
      ↓
Unknown Values Identification
      ↓
Constraint Identification
      ↓
Safety and Human-Review Screening
      ↓
Structured Planning
      ↓
Deterministic Computation Request, if applicable
      ↓
Engineering Advisory Report
```

This workflow allows EAS to move from an informal engineering question toward a structured and reviewable advisory report.

---

## 3. Required Input Categories

An engineering request does not always need to include every possible detail, but EAS benefits when the input contains the following categories.

### 3.1 Problem Statement

The problem statement describes what the engineer wants EAS to do.

Examples:

```text id="xwco30"
Review this 24 VDC control circuit and determine whether the wire size,
fuse size, and power supply are appropriate.
```

```text id="b5r4nh"
Diagnose why a hydraulic press fixture is producing lower clamp force
than expected.
```

```text id="8m34zv"
Determine whether this cantilever bracket satisfies the stress and
deflection requirements.
```

A clear problem statement helps EAS select the correct engineering mode and domain context.

---

### 3.2 Engineering Mode

The engineering mode describes the type of assistance being requested.

EAS supports the following public-facing modes:

| Mode                       | Description                                                         |
| -------------------------- | ------------------------------------------------------------------- |
| **Solve Problem**          | Compute or estimate a result from known engineering inputs.         |
| **Diagnose Root Cause**    | Identify likely causes of a failure, symptom, or performance issue. |
| **Review Design**          | Evaluate whether a proposed design satisfies constraints.           |
| **Suggest Improvements**   | Recommend improvements to an existing system or design.             |
| **Explore Novel Solution** | Explore a possible engineering concept or alternative architecture. |

The user must explicitly choose a mode.

---

### 3.3 Engineering Domain

The engineering domain identifies the type of system or problem being analyzed.

Public-safe examples include:

* DC controls and power
* Industrial exhaust and airflow
* Compressed air and pneumatics
* Fluid pump loops
* Structural and mechanical brackets
* Thermal enclosure cooling
* Aerospace preliminary design
* Aerospace aerodynamics
* Mechanical power transmission

The domain helps EAS select relevant engineering context, expected variables, typical equations, constraints, and human-review triggers.

---

### 3.4 Known Values

Known values are the numerical or descriptive facts provided by the engineer.

Examples:

```text id="pl6bum"
Supply voltage: 24 VDC
Load current: 6 A
Wire length: 40 ft
Fuse size: 10 A
Power supply rating: 8 A
```

```text id="oiljak"
Pump flow requirement: 25 gpm
Pipe length: 150 ft
Fluid: water
Required discharge pressure: 45 psi
```

Known values should include units whenever possible.

---

### 3.5 Unknown Values

Unknown values are the results the engineer wants EAS to determine.

Examples:

* Required wire gauge
* Voltage drop
* Required pump head
* Belt speed
* Tip deflection
* Heat load
* Safety margin
* Root cause likelihood
* Pass/fail design status

Identifying unknown values helps EAS determine what calculations or reasoning steps are required.

---

### 3.6 Units

Units are essential to engineering reliability.

EAS expects units to be stated clearly whenever possible.

Examples:

```text id="ks311q"
Voltage: V
Current: A
Length: ft or m
Flow: gpm or L/min
Pressure: psi, Pa, or bar
Power: W, hp, or kW
Temperature: °C or °F
Force: lbf or N
Torque: lb-ft or N-m
```

If units are missing, ambiguous, incompatible, or unsupported, EAS may generate warnings or require human review.

---

### 3.7 Constraints

Constraints define the acceptance criteria for the engineering problem.

Examples:

```text id="wtu4f7"
Voltage drop must be less than 5%.
Belt speed must be between 75 and 85 ft/min.
Tip deflection must be less than L/180.
Power supply load must not exceed 80% of rated capacity.
Pump option must satisfy flow and pressure requirements.
```

Constraints allow EAS to perform pass/fail checks and produce more reviewable recommendations.

---

### 3.8 Candidate Options

Some engineering tasks involve selecting among multiple options.

Examples:

```text id="wvmuux"
Option A: Pipe A with Pump P-1
Option B: Pipe B with Pump P-2
Option C: Pipe C with Pump P-3
```

Candidate options may include cost, performance, capacity, dimensional data, or other design attributes.

When options are provided, EAS may attempt a computed selection if the information is sufficient.

---

### 3.9 Symptoms or Failure Conditions

For diagnostic tasks, the input should describe symptoms or observed behavior.

Examples:

```text id="pvmv5x"
The hydraulic press is producing low clamp force.
The motor is overheating under normal load.
The enclosure temperature exceeds the target limit.
The conveyor is running slower than required.
The airflow system is not meeting capture velocity.
```

The more specific the symptom, the better EAS can identify likely causes and recommended checks.

---

### 3.10 Safety-Critical or Regulated Context

The engineer should identify when the request involves safety-critical or regulated systems.

Examples:

* Aerospace systems
* Electrical installations
* Pressure systems
* Lifting devices
* Structural supports
* Human-occupied spaces
* Fire or life-safety systems
* Regulated industrial equipment

EAS may require human review for these cases even if calculations can be performed.

---

## 4. Recommended Input Template

A strong EAS request can use the following structure:

```text id="f4sk8y"
Engineering Mode:
[solve problem / diagnose root cause / review design / suggest improvements / explore novel solution]

Engineering Domain:
[system type or domain]

Problem Statement:
[clear description of the engineering task]

Known Values:
- [value 1 with unit]
- [value 2 with unit]
- [value 3 with unit]

Unknowns / Desired Outputs:
- [what should be solved, reviewed, diagnosed, or recommended]

Constraints:
- [acceptance criterion 1]
- [acceptance criterion 2]

Candidate Options, if applicable:
- [option A]
- [option B]
- [option C]

Safety or Review Notes:
- [any safety-critical, regulated, or uncertain context]

Desired Output:
[calculation / recommendation / design review / diagnostic ranking / advisory report]
```

This template is not required, but it helps EAS produce a more structured and useful advisory report.

---

## 5. Example Inputs

### 5.1 Design Review Example

```text id="k9mppp"
Engineering Mode:
Review Design

Engineering Domain:
DC Controls / Power

Problem Statement:
Review a 24 VDC control circuit and determine whether the wire size,
fuse size, and power supply are appropriate.

Known Values:
- Supply voltage: 24 VDC
- Load current: 6 A
- One-way wire length: 40 ft
- Proposed fuse: 10 A
- Power supply rating: 8 A

Unknowns / Desired Outputs:
- Voltage drop
- Wire suitability
- Fuse suitability
- Power supply loading
- Pass/fail recommendation

Constraints:
- Voltage drop should be less than 5%
- Power supply should not exceed 80% continuous loading

Safety or Review Notes:
- Advisory only; final electrical design should be reviewed by qualified personnel.
```

---

### 5.2 Root-Cause Diagnostic Example

```text id="2bmc3j"
Engineering Mode:
Diagnose Root Cause

Engineering Domain:
Fluid Power / Hydraulics

Problem Statement:
Diagnose why a hydraulic press fixture is producing lower clamp force
than expected.

Known Values:
- Pump pressure appears normal at the pump outlet
- Clamp force is low at the fixture
- Directional valve was recently replaced
- System has normal reservoir level
- No major external leaks are visible

Unknowns / Desired Outputs:
- Most likely root causes
- Recommended inspection order
- Whether additional pressure measurements are needed

Constraints:
- Do not assume a single cause without evidence
- Identify measurements needed to confirm the diagnosis

Safety or Review Notes:
- Hydraulic systems can be hazardous; troubleshooting should be performed by qualified personnel.
```

---

### 5.3 Candidate Selection Example

```text id="hl0j53"
Engineering Mode:
Review Design

Engineering Domain:
Fluid Pump Loop

Problem Statement:
Select the lowest-cost pump and pipe configuration that satisfies the
required flow and pressure constraints.

Known Values:
- Required flow: 50 gpm
- Required discharge pressure: 60 psi
- Fluid: water
- Pipe length: 200 ft

Candidate Options:
- Option A: Pipe A + Pump P-1, cost $4,800
- Option B: Pipe B + Pump P-2, cost $5,220
- Option C: Pipe C + Pump P-3, cost $5,700

Unknowns / Desired Outputs:
- Which option passes all constraints
- Lowest-cost passing option
- Rejected options and reasons

Constraints:
- Must satisfy required flow
- Must satisfy required pressure
- Prefer lowest cost among passing options
```

---

## 6. Handling Incomplete Inputs

Engineering requests are often incomplete.

When information is missing, EAS may:

* Make a clearly stated assumption
* Ask for the missing value
* Produce a partial advisory
* Mark the result as warning-bearing
* Require human review
* Refuse to compute unsupported or unsafe results

Examples of missing information include:

* Unknown units
* Missing load values
* Missing geometry
* Missing material properties
* Missing environmental conditions
* Missing safety factors
* Missing design constraints

EAS should not silently fill critical gaps with unsupported assumptions.

---

## 7. Input Quality and Output Reliability

Input quality directly affects output reliability.

A vague request may produce a high-level advisory, while a structured request with values, units, and constraints may allow deterministic computation and stronger governance status.

Example of weak input:

```text id="rqsvlz"
Is this pump okay?
```

Example of stronger input:

```text id="nphw4v"
Review this pump selection for a water loop requiring 50 gpm at 60 psi.
Pipe length is 200 ft. Compare three candidate pump/pipe options and
select the lowest-cost option that satisfies flow and pressure requirements.
```

The stronger input gives EAS enough context to identify the domain, mode, variables, constraints, and selection criteria.

---

## 8. Human-Review Triggers at Input Stage

EAS may identify human-review triggers before computation begins.

Common input-stage human-review triggers include:

* Safety-critical system
* Regulated engineering context
* Missing critical values
* Ambiguous units
* Unsupported domain
* Conflicting constraints
* Insufficient design information
* Request for certification or approval
* Real-world deployment decision
* High consequence of failure

When these triggers are present, EAS may still provide advisory support, but the final report should clearly state that qualified human review is required.

---

## 9. Public Repository Boundary

This document describes the public-safe EAS input workflow.

It does not include:

* Private prompt templates
* Activation schemas
* Backend route definitions
* UI implementation details
* Authentication logic
* Model-provider configuration
* Internal parsing logic
* Source code
* Operational logs
* Private engineering pack contents

The goal is to explain the engineering input philosophy and workflow without exposing private implementation details.

---

## 10. Summary

The Engineer Input Workflow is the entry point into EAS.

It helps transform an engineering request into a structured process involving:

* Problem interpretation
* Mode identification
* Domain selection
* Known-value extraction
* Unknown-value identification
* Unit handling
* Constraint identification
* Safety screening
* Deterministic computation routing
* Governance evaluation
* Structured advisory reporting

The workflow reflects the core EAS philosophy:

> AI-assisted engineering should be structured, unit-aware, constraint-aware, reviewable, and explicit about when human judgment is required.
