# Validation

Scientific software should not be trusted simply because it produces a numerical result.

Thermo Table Bot is developed with automated testing, regression testing, psychrometric validation, stress testing and scientific consistency checks intended to detect numerical, physical and implementation errors before they reach the user.

This page summarizes the public validation evidence for the current documented system without exposing the private production source code or internal scientific datasets.

---

## Validation summary

The validated project snapshot used for this documentation reported:

| Validation category | Result |
|---|---:|
| Automated test suite | `412 passed` |
| Thermodynamic regression cases | `118 / 118 passed` |
| Psychrometric pair evaluations | `14,000 / 14,000 passed` |
| Stress-test cases | `10,000 / 10,000 passed` |
| Scientific invariant failures | `0` |

These results describe the validated project snapshot and should not be interpreted as a claim that scientific software can never contain defects.

Validation reduces risk; it does not eliminate the need for engineering judgment.

---

## Validation philosophy

Thermo Table Bot is tested at multiple levels because different classes of errors require different forms of verification.

A simplified validation structure is:

    Scientific data
          ↓
    Property calculations
          ↓
    Region detection
          ↓
    Interpolation
          ↓
    Psychrometric relationships
          ↓
    Physical consistency checks
          ↓
    Regression tests
          ↓
    Stress tests
          ↓
    User-facing result

A calculation can be numerically executable while still being physically invalid.

For this reason, the validation process includes both software-oriented tests and thermodynamic consistency checks.

---

## Automated test suite

The validated project snapshot reported:

`412 passed`

with no failed tests in the recorded test run.

The automated test suite covers multiple parts of the system rather than testing only the Telegram interface.

The purpose of these tests is to detect unintended changes in calculation behavior, data handling and supporting system logic.

---

## Thermodynamic regression validation

Thermodynamic calculations are protected by regression testing.

The validated snapshot reported:

`118 / 118 thermodynamic regression cases passed`

Regression tests are important because a software change that appears unrelated to a scientific calculation can still alter numerical behavior.

A regression suite provides a set of previously validated cases that can be recalculated after changes to the system.

Conceptually:

    Validated reference case
             ↓
       System changes
             ↓
       Recalculate case
             ↓
    Compare with expected behavior
          ↙          ↘
       Match        Mismatch
         ↓              ↓
       Pass         Investigate

This helps detect unintended changes before deployment.

---

## Psychrometric validation

The psychrometric engine is validated separately from the ordinary thermodynamic property-table workflow.

The validated project snapshot reported:

`14,000 / 14,000 psychrometric pair evaluations passed`

These evaluations exercise supported humid-air property relationships across a large collection of calculation cases.

Psychrometric validation is particularly important because different known-property pairs may reach the same physical state through different calculation paths.

The system should therefore maintain consistency between equivalent representations of the same humid-air condition.

---

## Cross-property consistency

Psychrometric properties are not independent numerical outputs.

They are physically related.

Examples include relationships between:

- Dry-bulb temperature
- Wet-bulb temperature
- Dew-point temperature
- Relative humidity
- Humidity ratio
- Enthalpy

Validation therefore considers whether calculated properties remain mutually consistent rather than checking each output only in isolation.

For ordinary unsaturated states, examples of expected physical relationships include:

`T_dp ≤ T_db`

and:

`T_wb ≤ T_db`

At saturation, the relevant psychrometric properties should approach their physically consistent limiting relationships.

---

## Scientific invariants

A scientific invariant is a relationship or condition that should remain true when the calculated state is physically valid within the supported model.

The validated project snapshot reported:

`0 scientific invariant failures`

Invariant checks provide another layer of protection beyond ordinary expected-value tests.

Instead of asking only:

"Did the software reproduce a stored number?"

an invariant test can also ask:

"Does the calculated state still obey the required physics?"

This distinction is important in scientific computing.

---

## Thermodynamic region consistency

Region detection affects which scientific data and calculation method should be used.

Validation therefore includes consistency between the supplied state and the detected thermodynamic region.

Relevant regions may include:

- Compressed liquid
- Saturated liquid
- Two-phase liquid-vapor mixture
- Saturated vapor
- Superheated vapor

For example, a valid two-phase state should produce a vapor quality within the physical interval:

`0 ≤ x ≤ 1`

A state classified outside the two-phase region should not be treated as an ordinary liquid-vapor mixture.

---

## Saturation consistency

Saturation relationships are central to both region detection and two-phase calculations.

Validation checks are intended to detect inconsistencies involving:

- Saturation pressure
- Saturation temperature
- Saturated-liquid properties
- Saturated-vapor properties
- Vapor quality
- Phase-boundary behavior

Special attention is required near saturation boundaries because small numerical differences can change the classification of a state.

---

## Interpolation validation

Interpolation introduces calculated values between available scientific data points.

Validation therefore considers more than whether the interpolation formula can be executed.

Relevant checks include:

- Correct surrounding data selection
- Valid interpolation interval
- Boundary behavior
- Exact-point behavior
- Numerical consistency
- Prevention of unsupported extrapolation

When an exact property-data point exists, unnecessary interpolation should be avoided.

When the requested state lies outside the supported data range, the system should not silently present an extrapolated value as a validated table result.

---

## One-dimensional interpolation

For one-dimensional interpolation, the system evaluates a target value between two surrounding data points.

A representative linear relationship is:

`y = y₁ + (x - x₁) × (y₂ - y₁) / (x₂ - x₁)`

Validation must ensure that the target lies within the intended interval and that the surrounding values belong to the correct scientific region.

---

## Two-dimensional interpolation

Two-dimensional interpolation requires correct handling of surrounding data in two independent dimensions.

Validation therefore needs to consider:

- Selection of the correct surrounding data region
- Interpolation along the first dimension
- Interpolation along the second dimension
- Behavior at exact boundaries
- Consistency with neighboring states

This is especially important because a numerically valid interpolation using the wrong surrounding data can still produce a scientifically incorrect result.

---

## Stress testing

The validated project snapshot reported:

`10,000 / 10,000 stress-test cases passed`

Stress testing complements ordinary functional tests by repeatedly exercising the system across a large number of calculations.

Its purpose is not to prove that every possible thermodynamic state has been tested.

Instead, it helps identify failures that may appear only under repeated or broader execution.

---

## Input validation

Scientific validation begins before the calculation itself.

Inputs may need to be rejected when:

- Required values are missing
- A property pair is unsupported
- Values fall outside supported ranges
- The supplied state is physically inconsistent
- A calculation would require unsupported extrapolation
- The requested state cannot be represented by the available scientific data

Rejecting an unsupported state is preferable to returning a plausible-looking but scientifically unjustified number.

---

## Scientific data integrity

The production project maintains structured scientific data used by the thermodynamic calculation system.

Data integrity is treated as part of validation rather than as a separate administrative concern.

The internal project includes mechanisms for tracking scientific data and detecting unintended changes.

The production data manifest includes cryptographic SHA-256 information for controlled data assets.

This provides a mechanism for identifying unexpected modifications to validated scientific data.

---

## Documented data corrections

Scientific source material can contain transcription or publication errors.

When a source value is identified as inconsistent, silently changing it without documentation would weaken reproducibility.

The production project therefore records controlled data corrections together with their scientific rationale.

The validated project snapshot includes a documented correction associated with a superheated-water entropy value after the source entry was identified as thermodynamically inconsistent.

The public repository does not distribute the internal dataset or correction manifest, but the correction process is documented here to make the validation philosophy explicit.

---

## Why data corrections matter

A scientific software system should distinguish between:

- Copying a source value
- Detecting a physically inconsistent value
- Correcting a verified source or transcription issue
- Recording why the correction was made

This creates a more defensible scientific workflow than silently modifying a dataset until tests pass.

Validation should test both software behavior and the integrity of the scientific information on which that software depends.

---

## Numerical precision

Thermodynamic and psychrometric calculations involve floating-point arithmetic.

Exact binary equality is therefore not appropriate for every numerical comparison.

The production system uses internal numerical handling appropriate to its calculation workflow.

Exact tolerance values, comparison thresholds and implementation-specific numerical policies are intentionally not published in this documentation.

Keeping these implementation details private does not change the underlying validation principle: numerical comparisons must be strict enough to detect meaningful errors while accounting for legitimate floating-point behavior.

---

## Validation versus verification

In scientific software, two different questions are important:

1. Is the calculation implemented as intended?
2. Does the resulting state remain consistent with the relevant physical relationships?

Thermo Table Bot uses automated testing and scientific consistency checks to address both types of questions.

A successful software test alone is not sufficient evidence of physical correctness, and a physically plausible output alone is not sufficient evidence of correct implementation.

---

## Reproducibility and private implementation

The production source code and internal scientific datasets are not publicly released.

As a result, this repository does not claim full source-level reproducibility of the deployed service.

Instead, the public repository documents:

- Calculation methodology
- Supported scientific behavior
- Validation categories
- Recorded validation results
- Scientific consistency principles
- Known limitations

This distinction is intentional.

---

## What these results do not prove

The validation results should not be interpreted as proof that:

- Every possible thermodynamic state is supported
- Every possible input combination has been tested
- The system is free from all software defects
- The underlying engineering problem has been formulated correctly by the user
- Thermo Table Bot can replace engineering judgment
- Results should be used outside the documented scope without verification

Validation provides evidence about tested behavior, not a guarantee about every possible use case.

---

## Recommended engineering practice

For educational and engineering work, users should still:

- Check units
- Confirm the selected substance
- Verify that the chosen properties define the intended state
- Review the detected thermodynamic region
- Consider whether the result is physically reasonable
- Independently verify results when required by the importance of the application

Thermo Table Bot is a scientific calculation tool, not a substitute for thermodynamic understanding or professional engineering responsibility.

---

## Scope of public validation information

This page intentionally does not publish:

- Production source code
- Internal scientific datasets
- Complete test files
- Private reference cases
- Exact numerical tolerances
- Internal correction manifests
- Server or deployment configuration
- Security-sensitive operational information

Additional validation evidence may be documented publicly in future releases without exposing the private production implementation.

---

## Related documentation

- [Project Overview](./overview.md)
- [How It Works](./how-it-works.md)
- [Thermodynamic Properties](./thermodynamic-properties.md)
- [Region Detection](./region-detection.md)
- [Interpolation](./interpolation.md)
- [Psychrometrics](./psychrometrics.md)
- [Examples](./examples.md)
- [Limitations](./limitations.md)
- [FAQ](./faq.md)
