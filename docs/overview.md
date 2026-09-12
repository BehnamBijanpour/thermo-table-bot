# Project Overview

Thermo Table Bot is a scientific thermodynamics and psychrometrics tool developed by **B-Logic** and made available through Telegram.

The project is designed to reduce repetitive thermodynamic table work while keeping the user focused on the engineering problem itself.

Instead of manually searching through multiple property tables, identifying the correct region, performing repeated interpolation and transferring values back into a calculation, the user can provide supported state information and let the system handle the property-evaluation workflow.

This repository contains the public technical documentation of Thermo Table Bot.

The production source code, internal scientific datasets and deployment infrastructure are not publicly released.

---

## Core idea

Thermodynamic problem solving often contains two different kinds of work:

1. Understanding and modeling the physical problem
2. Repetitive property lookup and numerical evaluation

Thermo Table Bot focuses on the second part.

The intended workflow is:

    Understand the engineering problem
                ↓
    Identify the known state properties
                ↓
    Submit the supported properties
                ↓
    Thermo Table Bot evaluates the state
                ↓
    Use the calculated properties
                ↓
    Continue the engineering analysis

The goal is not to remove thermodynamic reasoning.

The goal is to reduce the repetitive numerical work surrounding it.

---

## Main capabilities

Thermo Table Bot currently provides functionality for:

- Thermodynamic property evaluation
- Automatic thermodynamic region detection
- One-dimensional interpolation
- Two-dimensional interpolation
- Saturation-state calculations
- Two-phase calculations
- Vapor-quality calculations
- Refrigerant property calculations
- Engineering-gas property calculations
- Humid-air psychrometric calculations
- Scientific input validation
- Physical consistency checking
- Reference and calculation-method reporting

The exact calculation path depends on the selected substance, known properties and physical state.

---

## Supported substances

The currently documented substances are:

| Substance | Category |
|---|---|
| Water | Pure substance |
| Air | Engineering gas |
| Ammonia | Refrigerant / thermodynamic fluid |
| Carbon dioxide | Engineering gas |
| Methane | Engineering gas |
| Nitrogen | Engineering gas |
| R134a | Refrigerant |
| R410A | Refrigerant |

Humid-air calculations are handled through the psychrometric system.

For additional details, see:

[Supported Fluids](./supported-fluids.md)

---

## Thermodynamic properties

Depending on the substance and calculation mode, Thermo Table Bot works with properties such as:

| Symbol | Property |
|---|---|
| `P` | Pressure |
| `T` | Temperature |
| `v` | Specific volume |
| `u` | Specific internal energy |
| `h` | Specific enthalpy |
| `s` | Specific entropy |
| `x` | Vapor quality |

Not every property combination is available for every substance or thermodynamic region.

See:

[Thermodynamic Properties](./thermodynamic-properties.md)

---

## System concept

Thermo Table Bot is more than a Telegram conversation interface.

The public system concept can be represented as:

    User
      ↓
    Telegram Interface
      ↓
    Input and Calculation Workflow
      ↓
    ┌───────────────────────────────┐
    │ Thermodynamic Engine          │
    │ Psychrometric Engine          │
    └───────────────────────────────┘
      ↓
    Scientific Data Layer
      ↓
    Region Detection and Interpolation
      ↓
    Validation and Consistency Checks
      ↓
    Result Generation
      ↓
    Telegram Interface
      ↓
    User

Telegram provides the interaction layer, while the scientific calculation workflow is handled by the underlying system.

More details are available in:

[How It Works](./how-it-works.md)

---

## Thermodynamic calculation workflow

A typical thermodynamic calculation begins with two supported known properties.

The system then determines the appropriate scientific calculation path.

Conceptually:

    Select substance
          ↓
    Select known properties
          ↓
    Enter values
          ↓
    Validate inputs
          ↓
    Identify thermodynamic region
          ↓
    Select relevant property data
          ↓
    Exact value available?
       ↙              ↘
     Yes              No
      ↓                ↓
    Lookup         Interpolation
       ↘              ↙
        Calculate remaining
             properties
                ↓
       Consistency checks
                ↓
             Result

This workflow allows the system to distinguish between direct property retrieval and states that require additional numerical evaluation.

---

## Thermodynamic region detection

For fluids with liquid-vapor phase behavior, identifying the correct region is essential.

Depending on the state, the system may classify a condition as:

- Compressed liquid
- Saturated liquid
- Two-phase liquid-vapor mixture
- Saturated vapor
- Superheated vapor

The detected region determines which scientific data and calculation path should be used.

See:

[Region Detection](./region-detection.md)

---

## Interpolation

Engineering problems frequently request states that do not correspond exactly to available property-data points.

Thermo Table Bot supports interpolation where appropriate.

Depending on the structure of the relevant data, the calculation may require:

- One-dimensional interpolation
- Two-dimensional interpolation

Interpolation is performed within supported data ranges and should not be confused with unsupported extrapolation.

See:

[Interpolation](./interpolation.md)

---

## Psychrometrics

Thermo Table Bot includes a dedicated calculation path for humid air.

The psychrometric system works with properties such as:

- Dry-bulb temperature
- Wet-bulb temperature
- Dew-point temperature
- Relative humidity
- Humidity ratio
- Enthalpy

A supported combination of known humid-air properties can be used to determine the remaining state information.

See:

[Psychrometrics](./psychrometrics.md)

---

## Scientific data

Thermodynamic calculations depend on structured scientific property data.

The production system maintains the scientific data required by the supported calculation paths.

The internal datasets themselves are not distributed through this repository.

Public documentation instead describes:

- Supported substances
- Supported properties
- Calculation methodology
- Region-detection principles
- Interpolation behavior
- Psychrometric methodology
- Validation approach
- Known limitations

This provides technical transparency without publishing the proprietary production implementation.

---

## Validation

Thermo Table Bot is developed as scientific software rather than as a simple numerical lookup interface.

The project includes multiple forms of testing and scientific validation.

The validated project snapshot documented by this repository reported:

| Validation category | Result |
|---|---:|
| Automated test suite | `412 passed` |
| Thermodynamic regression cases | `118 / 118 passed` |
| Psychrometric pair evaluations | `14,000 / 14,000 passed` |
| Stress-test cases | `10,000 / 10,000 passed` |
| Scientific invariant failures | `0` |

These results provide evidence for tested behavior but do not imply that every possible thermodynamic state or input combination is supported.

Detailed information is available in:

[Validation](./validation.md)

---

## Scientific consistency

A calculation is not considered meaningful simply because it produces a number.

The system includes checks intended to identify conditions such as:

- Unsupported property combinations
- Values outside supported ranges
- Physically inconsistent states
- Invalid thermodynamic-region relationships
- Unsupported extrapolation
- Inconsistent psychrometric states

Where a scientifically supported result cannot be produced, rejecting the calculation is preferable to returning an unjustified numerical estimate.

---

## Result transparency

Where applicable, Thermo Table Bot can provide information beyond the final numerical properties.

A result may include:

- Detected thermodynamic region
- Calculated properties
- Vapor quality
- Reference-table information
- Calculation method
- Interpolation information

This helps the user understand how the state was evaluated rather than receiving an unexplained number.

---

## Design philosophy

Thermo Table Bot is not intended to replace learning thermodynamics.

Students should still understand:

- How thermodynamic states are defined
- How property tables are organized
- Why different thermodynamic regions exist
- How interpolation works
- What vapor quality represents
- How psychrometric properties are related
- How calculated properties are used in engineering analysis

Once these concepts are understood, repeatedly searching tables and performing the same interpolation arithmetic becomes mechanical work.

Thermo Table Bot is designed to automate that mechanical part.

A useful analogy is a calculator: learning arithmetic remains necessary even when a calculator is available, but repeatedly performing routine arithmetic by hand is not always the best use of engineering time.

---

## Intended users

Thermo Table Bot can be useful for:

- Engineering students
- Thermodynamics students
- Instructors
- Researchers
- Engineers
- Users working with supported thermodynamic property calculations
- Users working with humid-air psychrometric calculations

The appropriate level of independent verification depends on the application.

---

## What Thermo Table Bot is not

Thermo Table Bot is not intended to be:

- A replacement for thermodynamics education
- A complete engineering-system simulator
- A general CFD solver
- A heat-transfer simulation package
- A substitute for engineering judgment
- The sole authority for safety-critical engineering decisions

Its primary role is thermodynamic and psychrometric property evaluation within the documented scientific scope.

---

## Public documentation

This repository is designed as a technical documentation and scientific-validation repository.

It contains information about:

- Project architecture
- Scientific methodology
- Supported substances
- Thermodynamic properties
- Region detection
- Interpolation
- Psychrometrics
- Calculation examples
- Validation
- Limitations
- Frequently asked questions

The repository intentionally does not contain the production application source code.

---

## Private implementation

The following components remain private:

- Production source code
- Internal scientific datasets
- Complete internal test suite
- Exact numerical tolerances
- Internal fallback logic
- Server configuration
- Deployment infrastructure
- Security-sensitive operational information

This separation allows the project's scientific behavior to be documented publicly while protecting the production implementation.

---

## Project status

Thermo Table Bot is an actively maintained scientific software project.

Its scientific capabilities, validation process, documentation and user experience may continue to evolve.

Public documentation can be updated as supported behavior changes.

---

## Documentation map

The main technical documentation is organized as follows:

| Document | Description |
|---|---|
| [How It Works](./how-it-works.md) | System architecture and calculation workflow |
| [Supported Fluids](./supported-fluids.md) | Supported substances and calculation scope |
| [Thermodynamic Properties](./thermodynamic-properties.md) | Property definitions and state variables |
| [Region Detection](./region-detection.md) | Thermodynamic state classification |
| [Interpolation](./interpolation.md) | One-dimensional and two-dimensional interpolation |
| [Psychrometrics](./psychrometrics.md) | Humid-air calculations |
| [Examples](./examples.md) | Representative calculation workflows |
| [Validation](./validation.md) | Testing and scientific validation |
| [Limitations](./limitations.md) | Scientific and numerical boundaries |
| [FAQ](./faq.md) | Frequently asked questions |

---

## Use Thermo Table Bot

Thermo Table Bot is available through Telegram:

https://t.me/thermo_table_bot

B-Logic:

https://b-logic.me/

---

## Related documentation

- [How It Works](./how-it-works.md)
- [Supported Fluids](./supported-fluids.md)
- [Thermodynamic Properties](./thermodynamic-properties.md)
- [Region Detection](./region-detection.md)
- [Interpolation](./interpolation.md)
- [Psychrometrics](./psychrometrics.md)
- [Examples](./examples.md)
- [Validation](./validation.md)
- [Limitations](./limitations.md)
- [FAQ](./faq.md)
