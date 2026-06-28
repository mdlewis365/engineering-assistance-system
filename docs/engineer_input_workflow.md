# Engineer Input Workflow

## User Inputs

The current user-facing EAS workflow asks for:

- engineering problem description
- optional supporting documents
- type of help

The problem description is required. Supporting documents can include public-safe examples such as schematics, reports, drawings, notes, logs, spreadsheets, screenshots, or diagrams.

## Type of Help

The user selects one of the current engineering modes:

- solve-problem
- diagnose-root-cause
- review-design
- suggest-improvements
- explore-novel-solution

## What Happens Next

EAS uses the selected help type and available evidence to plan the analysis. If bounded computation is needed, it builds a deterministic computation plan for MCM. If computation is not useful or not possible, the workflow can proceed with a qualitative advisory path and visible limitations.

## What Is Not Included

This document does not expose backend fields, route names, prompt text, private file handling, model routing, or internal validation code.
