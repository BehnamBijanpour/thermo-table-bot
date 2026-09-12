# How It Works

Thermo Table Bot is structured as a scientific calculation system with a Telegram interface on top.

The user interacts with the bot through Telegram, while the underlying system handles state identification, data selection, interpolation, thermodynamic calculations and psychrometric relationships.

---

## High-level architecture

The system can be represented by the following logical layers:

    User
      ↓
    Telegram Interface
      ↓
    Calculation Workflow
      ↓
    Thermodynamic Engine / Psychrometric Engine
      ↓
    Scientific Data Layer
      ↓
    Validation and Consistency Checks
      ↓
    Result Generation

Each layer has a different role in the calculation process.

---

## Telegram interface

Telegram provides the user-facing interface of Thermo Table Bot.

Through the bot, the user can:

- Select the type of calculation
- Select a working substance
- Choose known thermodynamic properties
- Enter numerical values
- Receive calculated properties
- View information about the calculation method
- View the reference data used for the result

The Telegram interface is separated conceptually from the scientific calculation logic.

This allows the thermodynamic and psychrometric engines to remain focused on scientific calculations rather than user-interface behavior.

---

## Calculation workflow

A typical thermodynamic calculation follows a sequence similar to:

    User selects calculation type
              ↓
    User selects substance
              ↓
    User selects known properties
              ↓
    User enters numerical values
              ↓
    Input validation
              ↓
    Thermodynamic state identification
              ↓
    Region detection
              ↓
    Relevant property data selection
              ↓
    Direct lookup or interpolation
              ↓
    Remaining properties calculated
              ↓
    Consistency checks
              ↓
    Result returned to the user

The exact calculation path depends on the selected substance, known property pair and thermodynamic region.

---

## Thermodynamic engine

The thermodynamic engine handles property calculations for the supported substances.

Its responsibilities include:

- Interpreting the supplied state variables
- Determining whether the selected property pair can define a valid state
- Identifying the relevant thermodynamic region
- Selecting the appropriate property data
- Performing interpolation when required
- Calculating the remaining thermodynamic properties
- Checking the physical consistency of the result

The calculation process may differ significantly between compressed-liquid, saturation and superheated-vapor regions.

---

## Psychrometric engine

Humid-air calculations are handled through a dedicated psychrometric calculation path.

The psychrometric engine works with relationships between properties such as:

- Dry-bulb temperature
- Wet-bulb temperature
- Dew-point temperature
- Relative humidity
- Humidity ratio
- Enthalpy

A valid combination of known humid-air properties is used to determine the remaining quantities.

Psychrometric calculations are documented separately.

See:

[Psychrometrics](./psychrometrics.md)

---

## Scientific data layer

Thermodynamic calculations depend on structured scientific property data.

The scientific data layer provides the property information required by the calculation engines.

Depending on the substance and state, the system may need data associated with:

- Saturation conditions
- Compressed-liquid states
- Superheated-vapor states
- Refrigerant properties
- Gas properties
- Humid-air relationships

The internal production datasets are not publicly distributed in this repository.

This public documentation focuses on the scientific methodology and observable behavior of the system.

---

## Region detection

For substances that may exist in different thermodynamic regions, the system must determine the physical region before selecting the calculation path.

A simplified conceptual process is:

    Known state variables
            ↓
    Saturation boundary evaluation
            ↓
    State comparison
            ↓
    Region identified
            ↓
    Appropriate data selected

Possible regions may include:

- Compressed liquid
- Saturated liquid
- Two-phase liquid-vapor mixture
- Saturated vapor
- Superheated vapor

More details are available in:

[Region Detection](./region-detection.md)

---

## Interpolation

Property data is available at discrete states, but user inputs may fall between those states.

When required, Thermo Table Bot performs interpolation rather than restricting calculations to exact tabulated values.

Depending on the structure of the relevant data, this may involve:

- One-dimensional interpolation
- Two-dimensional interpolation

Interpolation is performed only after the correct thermodynamic region and relevant data range have been identified.

More details are available in:

[Interpolation](./interpolation.md)

---

## Direct lookup versus interpolation

Not every calculation requires interpolation.

If the requested state corresponds directly to an available property-data point, the value can be retrieved directly.

Conceptually:

    Requested state
          ↓
    Exact data available?
       ↙          ↘
     Yes          No
      ↓            ↓
    Lookup     Interpolation
       ↘          ↙
          Result

Avoiding unnecessary interpolation helps preserve the original tabulated value when an exact state is available.

---

## Validation and consistency checks

Scientific calculations should not rely only on producing a numerical result.

Thermo Table Bot includes internal validation and consistency checks intended to detect invalid, unsupported or physically inconsistent states.

These checks may involve:

- Input-range validation
- Property-pair compatibility
- Thermodynamic-region consistency
- Interpolation-range checks
- Numerical consistency
- Physical plausibility of calculated states

The detailed validation methodology is documented separately.

See:

[Validation](./validation.md)

---

## Result generation

Once the scientific calculation has been completed, the result is prepared for presentation through Telegram.

Depending on the calculation, the output may contain:

- Thermodynamic region
- Calculated thermodynamic properties
- Vapor quality, where applicable
- Reference-table information
- Calculation or interpolation method

The intention is not only to return a number, but also to provide enough context for the user to understand how the state was evaluated.

---

## Error handling

Not every combination of inputs represents a valid or supported calculation.

The system may reject a calculation when, for example:

- Required inputs are missing
- A value is outside the supported range
- A property pair is not supported
- The requested state cannot be represented by the available scientific data
- The supplied properties are physically inconsistent

In these situations, returning no result is preferable to presenting an unsupported numerical estimate.

---

## Design principle

Thermo Table Bot is designed to automate repetitive thermodynamic table work without removing the engineering reasoning from the problem.

The intended workflow is:

    Student or engineer
           ↓
    Understand the physical problem
           ↓
    Define the thermodynamic state
           ↓
    Use Thermo Table Bot for repetitive property evaluation
           ↓
    Continue the engineering analysis

The system is therefore intended as a calculation tool rather than a replacement for learning thermodynamics.

---

## Separation of public documentation and private implementation

This repository documents:

- Scientific concepts used by the system
- Supported capabilities
- Calculation workflows
- Validation methodology
- Examples
- Known limitations

It does not expose:

- Production source code
- Internal scientific datasets
- Server configuration
- Deployment infrastructure
- Internal operational tools
- Implementation-specific thresholds and numerical tolerances

This separation allows the scientific methodology and project behavior to be documented publicly while the production implementation remains private.

---

## Related documentation

- [Project Overview](./overview.md)
- [Supported Fluids](./supported-fluids.md)
- [Thermodynamic Properties](./thermodynamic-properties.md)
- [Region Detection](./region-detection.md)
- [Interpolation](./interpolation.md)
- [Psychrometrics](./psychrometrics.md)
- [Examples](./examples.md)
- [Validation](./validation.md)
- [Limitations](./limitations.md)
