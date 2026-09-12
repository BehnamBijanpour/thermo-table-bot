# Limitations

Thermo Table Bot is designed to automate thermodynamic property evaluation and psychrometric calculations within its supported scientific scope.

Like any scientific software, it has defined boundaries.

Understanding these boundaries is essential for interpreting results correctly and avoiding unsupported use of the system.

---

## Supported substances only

Thermo Table Bot currently provides thermodynamic calculations for the substances documented by the project:

- Water
- Air
- Ammonia
- Carbon dioxide
- Methane
- Nitrogen
- R134a
- R410A

A substance not included in the supported scientific data should not be assumed to behave as an interchangeable substitute for one of these fluids.

The list of supported substances may expand in future versions.

See:

[Supported Fluids](./supported-fluids.md)

---

## Supported property combinations

Not every mathematical combination of thermodynamic properties is necessarily available as an input pair.

A calculation requires a combination that:

- Is scientifically meaningful
- Can define the required state
- Is supported by the available property data
- Is implemented by the corresponding calculation path

A pair may therefore be rejected even when both individual properties are supported elsewhere in the system.

---

## Two independent properties

For a simple compressible substance in equilibrium, two independent intensive properties can generally define the thermodynamic state.

However, not every pair remains independent in every region.

A particularly important example occurs on the saturation line.

Pressure and temperature are related by the saturation condition and therefore do not independently determine vapor quality within the two-phase region.

Additional state information is required.

This is a thermodynamic constraint, not a software error.

---

## Finite property-data ranges

The scientific property data used by the system covers defined ranges.

Thermo Table Bot should not be assumed to calculate arbitrary states outside those ranges.

A state may be rejected when the required data lies outside the supported domain.

The presence of a mathematical interpolation or fitting method does not justify extending a thermodynamic dataset indefinitely.

---

## Interpolation is not extrapolation

Thermo Table Bot supports interpolation where appropriate.

Interpolation estimates a value between supported surrounding data points.

Extrapolation attempts to estimate a value outside the available data range.

These are fundamentally different operations.

Conceptually:

    Known data       Known data
        ●----------------●
             ↑
        Interpolation

    Known data       Known data
        ●----------------●----------?
                                   ↑
                              Extrapolation

A calculation requiring unsupported extrapolation may therefore be rejected rather than returned as a validated property value.

---

## Region-dependent calculations

Thermodynamic properties must be interpreted within the correct physical region.

Possible regions include:

- Compressed liquid
- Saturated liquid
- Two-phase liquid-vapor mixture
- Saturated vapor
- Superheated vapor

A relationship valid in one region should not automatically be applied to another.

Region detection is therefore part of the scientific calculation workflow.

See:

[Region Detection](./region-detection.md)

---

## Saturation-boundary sensitivity

States near a phase boundary require careful numerical treatment.

Small changes in pressure, temperature or another state property may move a state from one thermodynamic region to another.

Floating-point calculations also introduce finite numerical precision.

The production system includes internal handling for these conditions, but users should still interpret states extremely close to a phase boundary with appropriate engineering care.

---

## Vapor quality

Vapor quality `x` is meaningful only for saturated liquid-vapor states and their boundaries.

For the two-phase region:

`0 < x < 1`

At saturated liquid:

`x = 0`

At saturated vapor:

`x = 1`

Vapor quality should not be interpreted as an ordinary state property for compressed-liquid or superheated-vapor states.

---

## Numerical precision

Thermodynamic calculations involve floating-point arithmetic, interpolation and numerical comparisons.

Displayed values may therefore be affected by:

- Numerical precision
- Rounding
- Interpolation
- Precision of the underlying scientific data
- Conversion or representation of units

More displayed decimal places do not automatically imply greater physical accuracy.

---

## Source-data limitations

Scientific software depends on the quality and scope of its underlying scientific data.

Property data may originate from established engineering references and structured datasets, but any tabulated or digitized scientific source can be affected by issues such as:

- Finite tabulation resolution
- Rounding
- Transcription errors
- Source-specific conventions
- Limited state ranges

The Thermo Table Bot development workflow includes data-integrity controls and documented correction procedures, but no finite scientific dataset should be interpreted as universally exact.

See:

[Validation](./validation.md)

---

## Psychrometric model scope

Psychrometric calculations are performed within the humid-air model supported by Thermo Table Bot.

The system evaluates relationships between properties such as:

- Dry-bulb temperature
- Wet-bulb temperature
- Dew-point temperature
- Relative humidity
- Humidity ratio
- Enthalpy

The model should not automatically be generalized to every possible gas-vapor mixture or environmental condition.

Humid-air calculations outside the supported model or numerical range may require a different engineering treatment.

---

## Psychrometric input consistency

Not every numerical combination of humid-air properties represents a physically valid state.

For ordinary unsaturated humid air, relationships such as:

`T_dp ≤ T_db`

and:

`T_wb ≤ T_db`

should remain physically consistent.

Relative humidity must also remain within the supported physical range.

The system may reject property combinations that violate the assumptions or physical relationships of the supported psychrometric model.

---

## Atmospheric and operating conditions

Psychrometric properties can depend on total pressure.

Users should not assume that a humid-air result obtained under one set of operating conditions is automatically valid under a different pressure condition.

The interpretation of the result must remain consistent with the conditions used by the calculation.

---

## Units

A numerically valid input with the wrong unit represents the wrong physical state.

For example, the numerical value of a pressure has no useful thermodynamic meaning unless its unit is known.

Users should therefore verify:

- Input units
- Output units
- Property definitions
- Unit basis for specific quantities

The bot cannot correct an engineering interpretation that begins with the wrong physical unit.

---

## Equilibrium-state assumption

Thermodynamic property-table calculations describe states according to the scientific models represented by the available data.

They should not automatically be interpreted as complete models of strongly non-equilibrium, transient or spatially varying physical systems.

A real engineering system may require additional analysis involving:

- Heat transfer
- Fluid mechanics
- Mass transfer
- Chemical reactions
- Transient behavior
- Spatial gradients

Thermo Table Bot provides property information; it does not replace a complete physical model of the engineering system.

---

## Property calculation is not system simulation

Thermo Table Bot evaluates thermodynamic and psychrometric properties.

It is not a general-purpose simulator for complete engineering equipment or processes.

For example, obtaining inlet and outlet enthalpies does not automatically determine:

- Turbine efficiency
- Compressor performance
- Heat-exchanger effectiveness
- Pressure losses
- Heat-transfer coefficients
- Equipment dimensions

Those quantities require additional equations, assumptions and engineering analysis.

---

## Educational use

Thermo Table Bot can reduce repetitive table lookup and interpolation work.

It is not intended to remove the need to understand:

- Thermodynamic states
- Phase behavior
- Property relationships
- Vapor quality
- Interpolation
- Psychrometric concepts
- Energy and entropy balances

The recommended use is to understand the method first and use the tool to accelerate repetitive property evaluation.

---

## Engineering judgment

A calculated value should always be interpreted in the context of the physical problem.

Users remain responsible for checking whether:

- The correct substance was selected
- The correct input properties were used
- Units are consistent
- The detected state is physically reasonable
- The result belongs to the intended engineering problem

A plausible-looking number is not automatically a correct engineering answer.

---

## Safety-critical applications

Thermo Table Bot is an educational and scientific calculation tool.

It should not be treated as the sole authority for safety-critical design, regulatory compliance, medical systems, hazardous industrial operation or other applications where an incorrect result could create significant risk.

Such applications require appropriate independent verification, approved engineering procedures and domain-specific professional review.

---

## Internet and Telegram availability

The deployed user interface is provided through Telegram.

Availability can therefore depend on factors outside the scientific calculation engine, including:

- Internet connectivity
- Telegram availability
- Server availability
- Maintenance
- Infrastructure interruptions

Loss of access to the Telegram interface does not represent a thermodynamic calculation failure, but it may temporarily prevent use of the deployed service.

---

## Private implementation

The public repository documents the scientific behavior of Thermo Table Bot but does not publish the production implementation.

The following remain private:

- Production source code
- Internal scientific datasets
- Complete test suite
- Exact numerical tolerances
- Internal search and fallback logic
- Server configuration
- Deployment infrastructure
- Security-sensitive operational information

As a result, the deployed service cannot be fully reproduced from this documentation repository alone.

---

## Validation does not eliminate limitations

Thermo Table Bot has undergone automated, regression, psychrometric, stress and scientific-consistency testing.

These tests provide evidence that the validated system behaves as intended across the tested cases.

They do not prove that:

- Every possible state is supported
- Every possible input has been tested
- Every scientific source is error-free
- Every future software version will behave identically
- Every user input represents the intended engineering problem

Validation and limitations should therefore be considered together.

---

## Reporting unexpected results

An unexpected result should not automatically be assumed to be either a software error or a correct physical result.

Useful information for investigating a calculation includes:

- Selected substance
- Known property pair
- Input values
- Units
- Reported thermodynamic region
- Returned properties
- Reference information shown by the bot

Providing this context makes scientific investigation of unexpected behavior significantly more effective.

---

## Scope of this page

This page describes the major known boundaries of the publicly documented Thermo Table Bot system.

It is not intended to enumerate every implementation-specific restriction.

Supported capabilities and limitations may evolve as the scientific engine, datasets and documentation are updated.

---

## Related documentation

- [Project Overview](./overview.md)
- [How It Works](./how-it-works.md)
- [Supported Fluids](./supported-fluids.md)
- [Thermodynamic Properties](./thermodynamic-properties.md)
- [Region Detection](./region-detection.md)
- [Interpolation](./interpolation.md)
- [Psychrometrics](./psychrometrics.md)
- [Examples](./examples.md)
- [Validation](./validation.md)
- [FAQ](./faq.md)
