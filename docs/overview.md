# Overview

Thermo Table Bot is a scientific thermodynamics and psychrometrics tool developed by **B-Logic** and delivered through a Telegram interface.

Its purpose is to reduce the repetitive numerical work involved in thermodynamic property tables, interpolation, state identification and humid-air calculations, while keeping the user focused on the actual engineering problem.

The project is designed primarily for engineering students, educators and practitioners who work with thermodynamic properties and psychrometric relationships.

---

## Core idea

Traditional thermodynamics problem solving often requires several repeated steps:

1. Identify the thermodynamic state.
2. Select the correct property table.
3. Locate the surrounding tabulated values.
4. Perform interpolation when the exact state is not listed.
5. Extract the required properties.
6. Continue with the engineering analysis.

Thermo Table Bot automates much of this repetitive workflow.

The goal is not to replace the understanding of thermodynamics or table reading. Instead, the tool acts as a scientific calculator for tasks that would otherwise require repeated table navigation and manual interpolation.

---

## Main capabilities

Thermo Table Bot currently provides:

- Thermodynamic property calculations from two independent inputs
- Automatic thermodynamic region detection
- One-dimensional interpolation
- Two-dimensional interpolation
- Property calculations for multiple fluids and gases
- Psychrometric calculations for humid air
- Reporting of the reference table used in the calculation
- Reporting of the calculation or interpolation method used

---

## Supported substances

The current system supports:

- Water
- Air
- Ammonia
- Carbon dioxide
- Methane
- Nitrogen
- R134a
- R410A

Psychrometric calculations are also available for humid air.

---

## Thermodynamic properties

Depending on the selected substance and state, the system can work with properties including:

| Symbol | Property |
|---|---|
| `P` | Pressure |
| `T` | Temperature |
| `v` | Specific volume |
| `u` | Specific internal energy |
| `h` | Specific enthalpy |
| `s` | Specific entropy |
| `x` | Vapor quality |

---

## System concept

Thermo Table Bot can be viewed as several logical layers working together:

```text
Telegram Interface
        ↓
Calculation Workflow
        ↓
Thermodynamic / Psychrometric Engine
        ↓
Scientific Data Layer
        ↓
Validation and Consistency Checks
