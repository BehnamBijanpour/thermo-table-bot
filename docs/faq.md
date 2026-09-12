# Frequently Asked Questions

This page answers common questions about Thermo Table Bot, its scientific scope, calculation methods and public documentation.

---

## What is Thermo Table Bot?

Thermo Table Bot is a scientific thermodynamics and psychrometrics tool developed by B-Logic and available through Telegram.

It is designed to reduce repetitive work involving thermodynamic property tables, interpolation, state identification and humid-air calculations.

The user provides supported state information, and the system evaluates the corresponding thermodynamic or psychrometric properties.

---

## Is Thermo Table Bot just a Telegram bot?

Telegram is the user interface, not the entire scientific system.

Behind the interface, the project includes separate calculation and data-processing components for:

- Thermodynamic property evaluation
- Psychrometric calculations
- Region detection
- Interpolation
- Scientific data handling
- Validation and consistency checking

The Telegram interface provides access to these capabilities without requiring the user to install scientific software locally.

---

## What substances are supported?

The currently documented thermodynamic substances are:

- Water
- Air
- Ammonia
- Carbon dioxide
- Methane
- Nitrogen
- R134a
- R410A

Humid-air psychrometric calculations are also supported.

See:

[Supported Fluids](./supported-fluids.md)

---

## What thermodynamic properties can the bot work with?

Depending on the selected substance, state and calculation mode, supported properties include:

- Pressure — `P`
- Temperature — `T`
- Specific volume — `v`
- Internal energy — `u`
- Enthalpy — `h`
- Entropy — `s`
- Vapor quality — `x`

Not every property combination is necessarily available for every substance or thermodynamic region.

---

## Can Thermo Table Bot detect the thermodynamic region automatically?

Yes.

Where applicable, the system evaluates the supplied state information and determines the relevant thermodynamic region before continuing with the property calculation.

Possible regions include:

- Compressed liquid
- Saturated liquid
- Two-phase liquid-vapor mixture
- Saturated vapor
- Superheated vapor

See:

[Region Detection](./region-detection.md)

---

## Why does region detection matter?

Different thermodynamic regions require different scientific data and calculation methods.

A state in the two-phase region, for example, cannot be treated in the same way as a superheated-vapor state.

Correct region identification therefore needs to occur before the appropriate property calculation can be selected.

---

## Does the bot perform interpolation?

Yes.

When the requested state lies between available property-data points, Thermo Table Bot can perform interpolation where supported.

The system supports:

- One-dimensional interpolation
- Two-dimensional interpolation

When an exact data point is available, unnecessary interpolation can be avoided.

See:

[Interpolation](./interpolation.md)

---

## Does the bot extrapolate beyond the available data?

Unsupported extrapolation should not be treated as ordinary interpolation.

If a requested state lies outside the supported scientific data range, the calculation may be rejected rather than extended beyond the validated data.

See:

[Limitations](./limitations.md)

---

## What is the difference between interpolation and extrapolation?

Interpolation estimates a value between known surrounding data points.

Extrapolation estimates a value outside the available data range.

Conceptually:

    ●---------x---------●
          interpolation

    ●-------------------●---------x
                              extrapolation

Thermo Table Bot is designed to distinguish between these two situations rather than treating them as equivalent operations.

---

## What happens if my state is exactly in the table?

If the requested state corresponds directly to an available scientific data point, the system can use the available value directly.

Interpolation is not required simply because the system supports interpolation.

---

## Can the bot calculate vapor quality?

Vapor quality `x` is supported where it is physically meaningful.

It describes the mass fraction of vapor in a saturated liquid-vapor mixture.

For the two-phase region:

`0 < x < 1`

At saturated liquid:

`x = 0`

At saturated vapor:

`x = 1`

Vapor quality is not an ordinary property of compressed-liquid or superheated-vapor states.

---

## Why are pressure and temperature sometimes not enough?

For a simple compressible substance, two independent intensive properties can generally define the state.

However, pressure and temperature are not independent inside the saturated liquid-vapor region.

On the saturation line, pressure and temperature are linked by the saturation relationship.

Therefore, `P` and `T` alone cannot determine where the state lies between saturated liquid and saturated vapor.

Another independent property is required.

---

## Does Thermo Table Bot support psychrometric calculations?

Yes.

The project includes a dedicated psychrometric calculation system for humid air.

Supported psychrometric quantities include properties such as:

- Dry-bulb temperature
- Wet-bulb temperature
- Dew-point temperature
- Relative humidity
- Humidity ratio
- Enthalpy

See:

[Psychrometrics](./psychrometrics.md)

---

## Does the bot replace a psychrometric chart?

Thermo Table Bot can numerically evaluate humid-air properties without requiring the user to estimate values graphically from a psychrometric chart.

However, the chart remains useful for understanding psychrometric processes and relationships.

The bot automates numerical property evaluation; it does not make the underlying psychrometric concepts unnecessary.

---

## Does Thermo Table Bot replace thermodynamic tables?

It replaces much of the repetitive manual lookup and interpolation work for supported calculations.

It does not make thermodynamic tables irrelevant.

Understanding how property tables are structured, how regions are identified and how interpolation works remains important for learning thermodynamics and interpreting the results correctly.

A useful way to think about the tool is:

    Learn the method
          ↓
    Understand the state
          ↓
    Let the tool handle repetitive evaluation
          ↓
    Continue solving the engineering problem

---

## Is Thermo Table Bot intended only for students?

No.

The project is designed primarily around educational and engineering property calculations, so it can be useful to:

- Engineering students
- Instructors
- Researchers
- Engineers
- Anyone working with supported thermodynamic or psychrometric property calculations

The appropriate level of independent verification depends on the application.

---

## Is the result always correct if the bot returns a number?

No scientific software should be interpreted that way.

A returned result should still be evaluated in the context of the engineering problem.

Users should verify:

- Substance selection
- Input values
- Units
- Thermodynamic region
- Physical plausibility
- Applicability of the supported model

Validation reduces the probability of errors but does not remove the need for engineering judgment.

---

## How has the system been validated?

The validated project snapshot documented by this repository reported:

| Validation category | Result |
|---|---:|
| Automated test suite | `412 passed` |
| Thermodynamic regression cases | `118 / 118 passed` |
| Psychrometric pair evaluations | `14,000 / 14,000 passed` |
| Stress-test cases | `10,000 / 10,000 passed` |
| Scientific invariant failures | `0` |

These results describe tested behavior in the validated project snapshot and are not a guarantee that every possible input or future version is error-free.

See:

[Validation](./validation.md)

---

## What is a scientific invariant?

A scientific invariant is a physical relationship or condition expected to remain true for a valid calculated state.

Instead of checking only whether the software reproduces a stored numerical value, invariant testing can also check whether the result continues to obey required physical relationships.

This provides an additional layer of scientific validation.

---

## Why might the bot reject my inputs?

A calculation may be rejected for several reasons, including:

- Missing required information
- Unsupported property pair
- Value outside the supported range
- Physically inconsistent inputs
- Insufficient information to define the state
- Unsupported extrapolation
- Scientific data unavailable for the requested condition

Rejecting a state can be the scientifically correct behavior.

Producing a number is not always preferable to producing an error.

---

## Why can values near saturation be sensitive?

The saturation boundary separates different thermodynamic regions.

A small change in pressure, temperature or another state property can therefore change the physical classification of a state near that boundary.

Numerical precision must also be considered when comparing values very close to saturation.

See:

[Region Detection](./region-detection.md)

---

## Why might my manual answer differ slightly from the bot?

Small differences may occur because of:

- Different property-table editions
- Different source data
- Rounding
- Number of displayed decimal places
- Manual interpolation
- Numerical interpolation
- Intermediate-value precision

A small numerical difference does not automatically indicate that either result is wrong.

The calculation method, source data and units should be compared before drawing a conclusion.

---

## Are more decimal places always more accurate?

No.

Displayed precision and physical accuracy are not the same thing.

The meaningful accuracy of a result depends on factors such as:

- Accuracy of the underlying scientific data
- Interpolation
- Numerical precision
- Input precision
- Physical assumptions

Displaying additional digits cannot create information that was not present in the original scientific data.

---

## Does the bot solve the entire thermodynamics problem for me?

Not necessarily.

Thermo Table Bot focuses on thermodynamic property evaluation and psychrometric calculations.

A complete engineering problem may still require:

- Mass balances
- Energy balances
- Entropy analysis
- Process equations
- Efficiency calculations
- Heat-transfer analysis
- Fluid-mechanics calculations
- Engineering assumptions

The bot helps obtain the properties required for that analysis.

The user still solves and interprets the engineering problem.

---

## Can I use Thermo Table Bot in an exam?

That depends entirely on the rules of the course, instructor or examination.

The existence of the tool does not imply that its use is permitted in an academic assessment.

Always follow the applicable exam rules.

---

## Can I use the results in engineering work?

Thermo Table Bot can assist with scientific and engineering calculations within its documented scope.

The required level of independent verification depends on the application.

For professional, regulated or safety-critical work, appropriate reference data, approved engineering procedures and independent verification should be used.

See:

[Limitations](./limitations.md)

---

## Is the source code open source?

No.

The production source code is not publicly released.

This repository is a public technical documentation repository, not the production source repository.

It documents:

- Scientific methodology
- Supported capabilities
- Calculation workflows
- Validation results
- Examples
- Limitations
- Project information

---

## Why is the source code private?

Thermo Table Bot is maintained as a production scientific software project.

The public documentation is intended to make its scientific scope and behavior understandable without publishing the proprietary production implementation.

Private components include:

- Production source code
- Internal scientific datasets
- Complete internal tests
- Deployment infrastructure
- Server configuration
- Security-sensitive operational information

---

## Can I reproduce the complete deployed bot from this repository?

No.

The repository intentionally does not contain the production source code or internal scientific datasets.

It is therefore not a complete reproducible distribution of the deployed service.

---

## Are the scientific datasets public?

The production scientific datasets used by the deployed system are not distributed through this repository.

The documentation describes their role in the calculation workflow and the validation approach without publishing the complete internal data.

---

## Does the project check scientific data integrity?

Yes.

Scientific data integrity is part of the project's validation workflow.

The production project includes controlled data tracking, including cryptographic SHA-256 information for scientific data assets.

Documented corrections can also be maintained when a source or transcription issue is scientifically identified.

See:

[Validation](./validation.md)

---

## Can the bot be used without Telegram?

The currently documented public user interface is the Telegram bot.

The internal scientific engine is conceptually separated from the Telegram interface, but this repository does not distribute a standalone local version of the production calculation system.

---

## Where can I use Thermo Table Bot?

Thermo Table Bot is available on Telegram:

https://t.me/thermo_table_bot

---

## Where can I learn more about the project?

The main documentation pages are:

- [Project Overview](./overview.md)
- [How It Works](./how-it-works.md)
- [Supported Fluids](./supported-fluids.md)
- [Thermodynamic Properties](./thermodynamic-properties.md)
- [Region Detection](./region-detection.md)
- [Interpolation](./interpolation.md)
- [Psychrometrics](./psychrometrics.md)
- [Examples](./examples.md)
- [Validation](./validation.md)
- [Limitations](./limitations.md)

The official B-Logic website is:

https://b-logic.me/

---

## What should I include when reporting an unexpected result?

Useful information includes:

- Selected substance
- Selected input properties
- Numerical input values
- Units
- Thermodynamic region reported by the bot
- Calculated properties
- Reference information displayed with the result
- A short description of what result was expected

A screenshot of the calculation can also make the issue easier to investigate.

Do not include private account information or unrelated personal data.

---

## Is the project still being developed?

Yes.

Thermo Table Bot is an actively maintained scientific software project.

The scientific engine, validation process, documentation and user experience may continue to evolve over time.

Changes to publicly documented behavior can be recorded in the project documentation and release history.

---

## B-Logic

Thermo Table Bot is developed as part of B-Logic, an educational and scientific software project focused on mathematics, physics and engineering tools.

Official website:

https://b-logic.me/
