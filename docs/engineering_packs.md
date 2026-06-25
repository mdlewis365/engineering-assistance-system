# Engineering Packs

## Engineering Assistance System (EAS)

The **Engineering Assistance System (EAS)** uses engineering packs to provide structured domain context for engineering advisory workflows.

Engineering packs help EAS behave less like a general-purpose chatbot and more like a governed engineering-assistance system. They provide public-safe domain framing, expected variables, typical constraints, calculation categories, failure modes, report expectations, and human-review triggers.

The guiding principle is:

> Engineering AI assistance should be domain-aware, mode-aware, unit-aware, and explicit about review requirements.

This document describes EAS engineering packs at a public-safe conceptual level. It does not include private pack contents, source code, prompts, schemas, routing logic, or implementation details.

---

## 1. Purpose of Engineering Packs

Engineering problems vary widely by domain.

A voltage-drop problem, pump-loop problem, structural bracket problem, thermal enclosure problem, aerospace problem, and software systems engineering problem require different assumptions, variables, units, constraints, validation concerns, and human-review expectations.

Engineering packs help EAS identify:

* Which technical context applies
* What variables may be relevant
* Which units are expected, when applicable
* Which calculations may be required
* Which constraints should be checked
* Which failure modes may matter
* Which outputs are appropriate
* When deterministic computation may be useful
* When human review should be required

Packs are intended to make EAS output more structured, traceable, and engineering-aware.

---

## 2. Pack Role in the EAS Workflow

At a public-safe level, engineering packs fit into the EAS workflow as follows:

```text
Engineer Input
    ↓
Submitted Engineering Mode
    ↓
Domain Pack Selection
    ↓
LLM Planning Layer
    ↓
Deterministic Computation Layer / MCM, when applicable
    ↓
Unit Validation, when applicable
    ↓
Constraint Checking
    ↓
Governance Gate
    ↓
Engineering Advisory Report
```

A mode is submitted with every EAS request. If the engineer does not manually select a mode, the submitted mode defaults to **Solve Problem**.

Engineering packs provide domain-specific context after the submitted mode is known.

For example:

```text
Submitted mode: Review Design
Selected domain pack: Mechanical Power Transmission
```

This combination indicates that EAS should evaluate a proposed mechanical power-transmission design against relevant constraints.

Another example:

```text
Submitted mode: Diagnose Root Cause
Selected domain pack: Software Systems Engineering
```

This combination indicates that EAS should reason about software symptoms, system behavior, failure modes, likely causes, diagnostic steps, and validation evidence.

---

## 3. Current Public-Safe Pack Inventory

The current EAS engineering pack inventory includes ten packs.

### Domain Pack Location

The following packs are currently present under the private EAS domain-pack location:

```text
aerospace_preliminary_design_pack.md
compressed_air_pneumatics_pack.md
dc_controls_power_pack.md
industrial_exhaust_airflow_pack.md
software_systems_engineering_pack.md
```

### Engineering Pack Location

The following packs are currently present under the private EAS engineering-pack location:

```text
aerospace_aerodynamics_pack.md
fluid_pump_loop_pack.md
mechanical_power_transmission_pack.md
structural_mechanical_bracket_pack.md
thermal_enclosure_cooling_pack.md
```

This public repository does not include the private contents of these packs. The filenames are listed only to document the public-safe pack inventory and conceptual system scope.

---

## 4. Types of Packs

At a public-safe conceptual level, EAS may use several kinds of engineering context.

### 4.1 Core Engineering Context

The core engineering context provides general EAS behavior, report discipline, safety posture, deterministic-validation philosophy, and human-review expectations.

It helps ensure that all EAS outputs remain structured, advisory, and review-aware.

---

### 4.2 Engineering Mode Context

Engineering mode context helps adapt the report to the submitted task type.

Public-facing modes include:

```text
Solve Problem
Diagnose Root Cause
Review Design
Suggest Improvements
Explore Novel Solution
```

The submitted mode influences report emphasis.

Examples:

* **Solve Problem** emphasizes calculation and result.
* **Diagnose Root Cause** emphasizes evidence and likely causes.
* **Review Design** emphasizes constraints and pass/fail evaluation.
* **Suggest Improvements** emphasizes tradeoffs and practical changes.
* **Explore Novel Solution** emphasizes feasibility, unknowns, and validation path.

---

### 4.3 Domain and Engineering Packs

Domain and engineering packs provide technical context for specific problem classes.

Public-safe current EAS packs include:

```text
industrial_exhaust_airflow_pack
dc_controls_power_pack
compressed_air_pneumatics_pack
fluid_pump_loop_pack
structural_mechanical_bracket_pack
thermal_enclosure_cooling_pack
aerospace_preliminary_design_pack
aerospace_aerodynamics_pack
mechanical_power_transmission_pack
software_systems_engineering_pack
```

The full private contents of these packs are proprietary and are not included in this public repository.

---

### 4.4 Secondary Support Context

Some engineering problems involve more than one domain.

For example, a thermal enclosure cooling problem may also involve airflow and electrical power. A pump-loop problem may involve mechanical power. A conveyor problem may involve power transmission, motor loading, and controls. A software systems problem may involve reliability, architecture, observability, security, data flow, deployment, and performance.

In these cases, EAS may conceptually use a primary pack and one or more supporting domain contexts.

This public document describes that idea only at a high level.

---

## 5. Current Pack Overview

| Pack                                | Public-Facing Purpose                                                                                                                           |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Industrial Exhaust / Airflow**    | Supports airflow, capture velocity, duct area, face velocity, and ventilation-style advisory tasks.                                             |
| **DC Controls / Power**             | Supports low-voltage DC control circuits, voltage drop, fuse sizing, power supply loading, and electrical review.                               |
| **Compressed Air / Pneumatics**     | Supports pneumatic flow, pressure, actuator force, air consumption, and compressed-air troubleshooting.                                         |
| **Fluid Pump Loop**                 | Supports pump, pipe, flow, pressure, head, and pump/pipe option review.                                                                         |
| **Structural / Mechanical Bracket** | Supports bracket loading, stress, deflection, safety factor, and structural design-review tasks.                                                |
| **Thermal Enclosure Cooling**       | Supports enclosure heat load, cooling requirements, ambient assumptions, and thermal design review.                                             |
| **Aerospace Preliminary Design**    | Supports early aerospace sizing, feasibility framing, assumptions, and review requirements.                                                     |
| **Aerospace Aerodynamics**          | Supports aerodynamic estimates, flow conditions, lift/drag concepts, and preliminary analysis.                                                  |
| **Mechanical Power Transmission**   | Supports belt speed, shaft speed, torque, horsepower, gear ratio, and drive-system review.                                                      |
| **Software Systems Engineering**    | Supports software architecture, system design, debugging, reliability, integration, deployment, observability, and AI/software workflow review. |

---

## 6. Industrial Exhaust / Airflow Pack

### Purpose

The **Industrial Exhaust / Airflow** pack supports airflow-related engineering advisory tasks.

It may be used for problems involving:

* Airflow rate
* Duct area
* Face velocity
* Capture velocity
* Exhaust flow
* Ventilation performance
* Air movement constraints

### Typical Inputs

Examples:

```text
Airflow rate: cfm
Face velocity: ft/min
Duct diameter: in
Duct area: ft²
Capture velocity target: ft/min
```

### Typical Outputs

Possible outputs include:

* Required area
* Estimated velocity
* Flow comparison
* Constraint pass/fail result
* Improvement recommendations
* Human-review status

### Validation Concerns

Important validation concerns include:

* Unit consistency
* Area and velocity relationship
* Flow-rate assumptions
* Duct geometry assumptions
* Whether real-world industrial hygiene review is required

### Human-Review Triggers

Human review may be required when:

* Air quality, worker safety, fumes, dust, or hazardous exhaust are involved
* Regulatory ventilation requirements apply
* Capture velocity is safety-critical
* Real-world installation or code compliance is involved

---

## 7. DC Controls / Power Pack

### Purpose

The **DC Controls / Power** pack supports low-voltage DC electrical-control advisory tasks.

It may be used for problems involving:

* 24 VDC control circuits
* Voltage drop
* Wire sizing review
* Fuse sizing review
* Power supply loading
* Current draw
* Continuous-load constraints

### Typical Inputs

Examples:

```text
Supply voltage: VDC
Load current: A
Wire length: ft or m
Wire gauge: AWG
Fuse size: A
Power supply rating: A or W
Voltage drop limit: %
Continuous loading limit: %
```

### Typical Outputs

Possible outputs include:

* Voltage drop estimate
* Power supply load percentage
* Fuse suitability notes
* Wire suitability notes
* Constraint pass/fail result
* Design review recommendation
* Human-review status

### Validation Concerns

Important validation concerns include:

* Voltage and current units
* One-way versus round-trip wire length
* Continuous versus peak loading
* Fuse purpose and protection assumptions
* Manufacturer derating data
* Applicable electrical codes or standards

### Human-Review Triggers

Human review may be required when:

* The circuit affects safety-critical equipment
* Code compliance is involved
* Fuse/wire coordination affects fire or equipment protection
* Installation details are incomplete
* Real-world electrical work is being performed

---

## 8. Compressed Air / Pneumatics Pack

### Purpose

The **Compressed Air / Pneumatics** pack supports pneumatic-system advisory tasks.

It may be used for problems involving:

* Actuator force
* Air pressure
* Flow demand
* Pressure drop
* Cylinder sizing
* Air consumption
* Pneumatic troubleshooting

### Typical Inputs

Examples:

```text
Supply pressure: psi or bar
Cylinder bore: in or mm
Stroke length: in or mm
Cycle rate: cycles/min
Required force: lbf or N
Airflow: scfm
```

### Typical Outputs

Possible outputs include:

* Cylinder force estimate
* Air consumption estimate
* Pressure adequacy review
* Constraint pass/fail result
* Diagnostic recommendations
* Human-review status

### Validation Concerns

Important validation concerns include:

* Gauge versus absolute pressure assumptions
* Supply pressure at source versus actuator
* Flow losses and restrictions
* Duty cycle
* Safety factors
* Pneumatic component ratings

### Human-Review Triggers

Human review may be required when:

* Pneumatic motion can injure people
* Stored energy hazards are present
* Actuators interact with tooling, clamps, guards, or fixtures
* Pressure ratings are uncertain
* Lockout/tagout or safety procedures are involved

---

## 9. Fluid Pump Loop Pack

### Purpose

The **Fluid Pump Loop** pack supports pump, pipe, flow, pressure, and fluid-loop advisory tasks.

It may be used for problems involving:

* Pump selection
* Pipe selection
* Flow requirements
* Pressure requirements
* Head estimates
* Pressure drop
* Pump/pipe option comparison
* Flow-loop diagnostics

### Typical Inputs

Examples:

```text
Required flow: gpm or L/min
Required pressure: psi or bar
Pipe length: ft or m
Pipe diameter: in or mm
Fluid type: water, coolant, oil, etc.
Candidate pump options
Candidate pipe options
Cost data
```

### Typical Outputs

Possible outputs include:

* Flow adequacy result
* Pressure/head adequacy result
* Pump/pipe option comparison
* Lowest-cost passing selection
* Rejected options and reasons
* Diagnostic recommendations
* Human-review status

### Validation Concerns

Important validation concerns include:

* Fluid properties
* Pipe length and fittings
* Static head
* Pressure-drop assumptions
* Pump curve availability
* Operating point uncertainty
* Candidate option completeness

### Human-Review Triggers

Human review may be required when:

* Pressure systems create safety hazards
* Pump curves or fluid properties are missing
* Chemical or hot fluids are involved
* Pipe/fitting losses are under-specified
* The system affects production, safety, or regulated equipment

---

## 10. Structural / Mechanical Bracket Pack

### Purpose

The **Structural / Mechanical Bracket** pack supports bracket, cantilever, stress, and deflection review tasks.

It may be used for problems involving:

* Cantilever brackets
* Support arms
* Bolted brackets
* Mechanical mounting supports
* Bending stress
* Tip deflection
* Safety factor
* Load path review

### Typical Inputs

Examples:

```text
Load: lbf or N
Arm length: in or mm
Material yield strength: psi or MPa
Section dimensions
Moment of inertia
Allowable deflection
Safety factor
Mounting conditions
```

### Typical Outputs

Possible outputs include:

* Bending moment estimate
* Stress estimate
* Deflection estimate
* Safety-factor review
* Constraint pass/fail result
* Design rejection or advisory recommendation
* Human-review status

### Validation Concerns

Important validation concerns include:

* Load case completeness
* Material properties
* Boundary conditions
* Dynamic versus static loading
* Fatigue concerns
* Welds, fasteners, and mounting details
* Safety factor assumptions

### Human-Review Triggers

Human review may be required when:

* The bracket supports people, overhead loads, vehicles, machinery, or safety-critical equipment
* Real-world structural installation is involved
* Material data is missing
* Load cases are incomplete
* Failure could cause injury, damage, or regulatory concerns

---

## 11. Thermal Enclosure Cooling Pack

### Purpose

The **Thermal Enclosure Cooling** pack supports enclosure heat-load and cooling advisory tasks.

It may be used for problems involving:

* Electronics enclosure heat load
* Internal temperature rise
* Ambient temperature
* Cooling requirement
* Fan or airflow evaluation
* Thermal improvement suggestions
* Enclosure design review

### Typical Inputs

Examples:

```text
Internal heat load: W
Ambient temperature: °C or °F
Maximum internal temperature: °C or °F
Enclosure dimensions
Fan airflow: cfm
Cooling device capacity: W or BTU/hr
Solar loading
Derating data
```

### Typical Outputs

Possible outputs include:

* Heat-load estimate
* Cooling requirement estimate
* Temperature-margin review
* Fan or cooling-device suitability notes
* Improvement options
* Human-review status

### Validation Concerns

Important validation concerns include:

* Ambient assumptions
* Internal heat-source estimates
* Solar loading
* Enclosure material and surface area
* Fan derating
* Cooling device ratings
* Environmental conditions

### Human-Review Triggers

Human review may be required when:

* Overheating could damage critical equipment
* Electrical safety is involved
* Environmental ratings are required
* Manufacturer derating data is missing
* The enclosure supports industrial or regulated operation

---

## 12. Aerospace Preliminary Design Pack

### Purpose

The **Aerospace Preliminary Design** pack supports early-stage aerospace feasibility and sizing discussions.

It may be used for problems involving:

* Conceptual sizing
* Weight estimates
* Performance tradeoffs
* Mission constraints
* Early feasibility framing
* Preliminary configuration review

### Typical Inputs

Examples:

```text
Estimated mass
Payload
Mission duration
Range
Speed
Power requirement
Lift requirement
Environmental assumptions
Configuration constraints
```

### Typical Outputs

Possible outputs include:

* Preliminary feasibility notes
* Approximate sizing relationships
* Key assumptions
* Risk areas
* Required validation steps
* Human-review status

### Validation Concerns

Important validation concerns include:

* High uncertainty in early design
* Incomplete mission requirements
* Missing aerodynamic, structural, propulsion, or control data
* Sensitivity to assumptions
* Regulatory and safety implications

### Human-Review Triggers

Human review is expected when:

* Any real aircraft, drone, flight vehicle, or aerospace hardware is involved
* Flight safety is affected
* Regulatory compliance is involved
* The design moves beyond conceptual discussion
* Physical testing, manufacturing, or deployment is considered

---

## 13. Aerospace Aerodynamics Pack

### Purpose

The **Aerospace Aerodynamics** pack supports preliminary aerodynamic advisory tasks.

It may be used for problems involving:

* Lift
* Drag
* Airspeed
* Wing area
* Dynamic pressure
* Coefficient assumptions
* Preliminary aerodynamic comparison

### Typical Inputs

Examples:

```text
Airspeed: m/s, ft/s, knots, or mph
Air density
Wing area
Lift coefficient
Drag coefficient
Weight
Angle-of-attack context
Reynolds number context
```

### Typical Outputs

Possible outputs include:

* Preliminary lift estimate
* Preliminary drag estimate
* Dynamic-pressure estimate
* Required coefficient estimate
* Feasibility notes
* Human-review status

### Validation Concerns

Important validation concerns include:

* Air density assumptions
* Unit consistency
* Coefficient validity
* Reynolds number effects
* Stall behavior
* Compressibility effects
* Flight envelope limitations
* Wind-tunnel or simulation validation needs

### Human-Review Triggers

Human review is expected when:

* The result affects real flight hardware
* Safety-of-flight decisions are involved
* Aerodynamic coefficients are assumed
* Flight testing or manufacturing is contemplated
* Regulatory or airworthiness issues may apply

---

## 14. Mechanical Power Transmission Pack

### Purpose

The **Mechanical Power Transmission** pack supports drive-system, speed, torque, horsepower, and power-transmission review tasks.

It may be used for problems involving:

* Conveyor drives
* Belt speed
* Gear ratios
* Shaft speed
* Pulley diameter
* Motor horsepower
* Torque requirement
* Drive selection
* Mechanical speed mismatch

### Typical Inputs

Examples:

```text
Motor speed: rpm
Gear ratio
Pulley diameter: in or mm
Required belt speed: ft/min or m/s
Torque requirement: lb-ft or N-m
Motor horsepower: hp or kW
Service factor
Load condition
```

### Typical Outputs

Possible outputs include:

* Belt speed calculation
* Shaft speed calculation
* Torque review
* Horsepower review
* Constraint pass/fail result
* Design rejection or recommendation
* Human-review status

### Validation Concerns

Important validation concerns include:

* Gear ratio interpretation
* Pulley diameter units
* Speed conversion
* Torque and horsepower relationship
* Service factor assumptions
* Duty cycle
* Start-up load
* Guarding and mechanical safety

### Human-Review Triggers

Human review may be required when:

* Moving machinery can create safety hazards
* Guarding or lockout/tagout is involved
* Torque loads are uncertain
* Failure could damage equipment or injure people
* The design is being used for real-world machinery

---

## 15. Software Systems Engineering Pack

### Purpose

The **Software Systems Engineering** pack supports software architecture, system design, reliability, debugging, integration, deployment, and AI/software workflow review.

It may be used for problems involving:

* Software architecture review
* Backend system design
* API design
* Data flow and state management
* Failure diagnosis
* Reliability and fault tolerance
* Logging and observability
* Deployment and runtime behavior
* Security and access-control considerations
* AI system orchestration
* Human-in-the-loop workflow design
* Software quality and maintainability

### Typical Inputs

Examples:

```text
Application architecture
Runtime environment
Framework or language
API endpoints or interfaces
Database or storage approach
Error logs or symptoms
Expected behavior
Observed behavior
Performance requirements
Security or access-control requirements
Deployment constraints
Reliability requirements
```

### Typical Outputs

Possible outputs include:

* Architecture review
* Root-cause diagnostic hypotheses
* Failure-mode analysis
* Suggested implementation improvements
* Integration risk notes
* Observability recommendations
* Security and access-control considerations
* Test and validation recommendations
* Human-review status

### Validation Concerns

Important validation concerns include:

* Incomplete system context
* Missing logs or traces
* Ambiguous runtime behavior
* Unclear data ownership or state transitions
* Incomplete security model
* Missing error handling
* Missing test coverage
* Deployment/environment mismatch
* AI model behavior uncertainty
* Privacy or sensitive-data handling

### Human-Review Triggers

Human review may be required when:

* The system handles sensitive data
* Security or access control is involved
* The software controls physical equipment
* The software affects safety-critical workflows
* The system is production-facing
* The output could affect data integrity, compliance, or business-critical operations
* AI model decisions require oversight or auditability

---

## 16. Pack Selection Concepts

Engineering pack selection helps EAS determine the most relevant technical context.

Pack selection may consider:

* Keywords in the engineering request
* Submitted engineering mode
* Domain-specific variables
* Units, when applicable
* Candidate options
* Constraint types
* Failure symptoms
* Desired output
* Safety context
* Software architecture or runtime context, when applicable

Examples:

```text
Request mentions voltage, current, fuse, and power supply.
Likely domain pack: DC Controls / Power
```

```text
Request mentions pump, flow, pressure, pipe, and gpm.
Likely domain pack: Fluid Pump Loop
```

```text
Request mentions pulley diameter, gear ratio, rpm, and belt speed.
Likely domain pack: Mechanical Power Transmission
```

```text
Request mentions API endpoints, backend state, runtime errors, and logs.
Likely domain pack: Software Systems Engineering
```

Pack selection should be treated as advisory routing, not proof that the problem is fully understood.

If a request spans multiple domains, EAS may identify a primary pack and supporting domain characteristics.

---

## 17. Pack and Mode Interaction

Engineering mode and engineering pack work together.

The mode describes the task type.

The pack describes the technical context.

Examples:

| Submitted Mode             | Selected Pack                   | Workflow Meaning                                                                                    |
| -------------------------- | ------------------------------- | --------------------------------------------------------------------------------------------------- |
| **Solve Problem**          | DC Controls / Power             | Compute values such as voltage drop or power loading.                                               |
| **Diagnose Root Cause**    | Fluid Pump Loop                 | Analyze symptoms such as low flow or low pressure.                                                  |
| **Review Design**          | Mechanical Power Transmission   | Check whether a drive design satisfies speed, torque, or horsepower constraints.                    |
| **Suggest Improvements**   | Thermal Enclosure Cooling       | Recommend ways to improve cooling performance.                                                      |
| **Explore Novel Solution** | Structural / Mechanical Bracket | Explore an alternative bracket concept or geometry.                                                 |
| **Diagnose Root Cause**    | Software Systems Engineering    | Analyze software failures, logs, state transitions, or runtime behavior.                            |
| **Review Design**          | Software Systems Engineering    | Review architecture, integration design, reliability posture, or security-sensitive design choices. |

This separation helps EAS avoid confusing the purpose of the request with the engineering domain.

---

## 18. Engineering Packs and MCM

Engineering packs provide domain context. The **Math Computation Module (MCM)** provides deterministic computation support where possible.

For example, a domain pack may help identify that a conveyor problem involves belt speed. MCM may then support deterministic calculation and constraint checking if the required values and units are available.

Conceptually:

```text
Engineering Pack:
Identifies relevant engineering context.

MCM:
Performs or validates supported structured calculations where applicable.

Governance Gate:
Interprets computation results, warnings, failures, and human-review triggers.
```

Not every pack or request requires numeric deterministic computation. For example, software systems engineering requests may rely more heavily on architecture review, debugging logic, failure-mode analysis, test planning, and governance reasoning. In those cases, MCM may be less central unless the request involves measurable performance, capacity, latency, throughput, error rates, cost estimates, or other numeric constraints.

This separation helps EAS combine domain-aware reasoning with deterministic validation when deterministic validation is applicable.

---

## 19. Pack-Driven Report Expectations

A selected engineering pack may influence the final Engineering Advisory Report.

For example:

* A DC controls report may emphasize voltage drop, current loading, fuse suitability, and electrical review.
* A pump-loop report may emphasize flow, pressure, head, pump/pipe selection, and rejected options.
* A structural bracket report may emphasize load, stress, deflection, safety factor, and review requirements.
* A thermal enclosure report may emphasize heat load, temperature margin, cooling capacity, and environmental assumptions.
* An aerospace report may emphasize preliminary nature, assumptions, feasibility, and qualified review requirements.
* A software systems report may emphasize architecture, failure modes, logs, state transitions, observability, security, test coverage, deployment context, and validation steps.

This makes EAS reports more domain-specific and more useful to review.

---

## 20. Pack Warnings and Human Review

Engineering packs may contribute human-review warnings.

Examples:

* Electrical installation may require qualified electrical review.
* Structural supports may require qualified structural review.
* Aerospace concepts may require qualified aerospace review.
* Pressure systems may require qualified mechanical or fluid-power review.
* Moving machinery may require guarding, safety, and operational review.
* Thermal designs may require manufacturer data or environmental validation.
* Software systems may require security review, privacy review, production-readiness review, or qualified engineering review.
* AI-enabled software workflows may require human oversight, auditability, and validation against unacceptable failure modes.

These warnings are passed forward to the Governance Gate.

---

## 21. Public Repository Boundary

This document describes EAS engineering packs at a public-safe conceptual level.

It does not include:

* Full internal pack contents
* Source code
* Private prompt text
* Activation prompts
* Pack registry implementation
* Pack-selection implementation
* Internal scoring logic
* Model-routing logic
* Full equation lists
* Full constraint libraries
* Internal validation rules
* Operational logs
* Raw engineering reports
* Carter or Synthetic OS private internals

The purpose of this document is to explain how engineering packs function in the EAS architecture without exposing proprietary implementation details.

---

## 22. Implementation Status Note

This document describes the public-facing architecture and design intent of EAS engineering packs.

Specific pack contents, supported calculations, domain handlers, unit conversions, constraints, routing behavior, and software systems engineering review behavior should be validated against the private EAS implementation and test suite.

The public repository should avoid presenting untested behavior as a guaranteed implementation property.

---

## 23. Summary

Engineering packs are a key part of EAS.

They provide domain-aware context that helps EAS interpret engineering requests, select relevant technical framing, identify expected variables, support deterministic computation where applicable, and produce structured advisory reports.

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

Together with submitted engineering modes, the Math Computation Module, unit validation, and the Governance Gate, engineering packs help EAS support a more structured and reviewable form of AI-assisted engineering.

The core belief is:

> Engineering AI should not only answer the question. It should understand the engineering domain, expose assumptions, check what can be checked, and identify when human review is required.
