# Thermodynamic Properties

Thermo Table Bot works with the thermodynamic properties commonly used to define and analyze equilibrium states.

Depending on the selected substance, thermodynamic region and available input pair, the system can determine additional properties from the known state variables.

---

## Supported properties

The main thermodynamic properties used by the system are:

| Symbol | Property | Typical unit |
|---|---|---|
| `P` | Pressure | `kPa` |
| `T` | Temperature | `°C` |
| `v` | Specific volume | `m³/kg` |
| `u` | Specific internal energy | `kJ/kg` |
| `h` | Specific enthalpy | `kJ/kg` |
| `s` | Specific entropy | `kJ/(kg·K)` |
| `x` | Vapor quality | Dimensionless |

The exact properties available depend on the selected substance and thermodynamic state.

---

## Pressure — P

Pressure is one of the primary state variables used in thermodynamic property calculations.

For substances with liquid-vapor phase-change data, pressure can also be used to locate saturation conditions and help determine the thermodynamic region.

---

## Temperature — T

Temperature is another primary state variable.

Together with another independent property, temperature can be used to define a thermodynamic state and determine the remaining properties.

For phase-change calculations, temperature may also be compared with saturation conditions during region identification.

---

## Specific volume — v

Specific volume represents the volume occupied per unit mass:

`v = V / m`

It is commonly expressed in:

`m³/kg`

Specific volume can be useful for identifying the state of a substance and distinguishing between liquid, two-phase and vapor regions.

---

## Specific internal energy — u

Specific internal energy represents the internal energy stored per unit mass of a substance.

It is commonly expressed in:

`kJ/kg`

Internal energy is frequently used in closed-system energy analysis and thermodynamic property calculations.

---

## Specific enthalpy — h

Specific enthalpy is related to internal energy, pressure and specific volume by:

`h = u + Pv`

It is commonly expressed in:

`kJ/kg`

Enthalpy is especially important in steady-flow devices and engineering systems such as turbines, compressors, pumps, heat exchangers and nozzles.

---

## Specific entropy — s

Specific entropy is commonly expressed in:

`kJ/(kg·K)`

Entropy is used extensively in second-law analysis and in the evaluation of thermodynamic processes and cycles.

---

## Vapor quality — x

Vapor quality describes the mass fraction of vapor in a saturated liquid-vapor mixture.

It is defined as:

`x = m_vapor / (m_liquid + m_vapor)`

For a two-phase mixture:

`0 < x < 1`

At the saturated-liquid boundary:

`x = 0`

At the saturated-vapor boundary:

`x = 1`

Vapor quality is only meaningful within the saturation region and at its boundaries.

---

## Two independent properties

For a simple compressible substance in equilibrium, the thermodynamic state can generally be fixed by two independent intensive properties.

Thermo Table Bot therefore uses supported pairs of known properties to determine the state and calculate the remaining quantities.

A conceptual workflow is:

    Two known properties
            ↓
    State definition
            ↓
    Region detection
            ↓
    Relevant property data
            ↓
    Interpolation if required
            ↓
    Remaining properties

Not every pair of properties is independent in every thermodynamic region.

For example, pressure and temperature are not independent within a saturated liquid-vapor mixture because saturation pressure and saturation temperature are directly related.

---

## Properties in the two-phase region

Within the saturated liquid-vapor region, a property can often be related to vapor quality using the general relation:

`y = y_f + x(y_g - y_f)`

where:

- `y` is the mixture property
- `y_f` is the saturated-liquid value
- `y_g` is the saturated-vapor value
- `x` is the vapor quality

This relationship can be applied to appropriate specific properties such as:

- Specific volume
- Internal energy
- Enthalpy
- Entropy

The exact calculation path depends on the known input properties.

---

## Determining vapor quality

If an appropriate mixture property is known, vapor quality may be determined from:

`x = (y - y_f) / (y_g - y_f)`

This relationship is valid only within the saturated liquid-vapor region and its boundaries.

A calculated value outside:

`0 ≤ x ≤ 1`

indicates that the state should not be interpreted as an ordinary two-phase mixture under that saturation condition.

---

## Saturated-liquid properties

At the saturated-liquid boundary:

`x = 0`

and the corresponding specific properties are:

`v = v_f`

`u = u_f`

`h = h_f`

`s = s_f`

This state represents liquid at the point where vaporization can begin.

---

## Saturated-vapor properties

At the saturated-vapor boundary:

`x = 1`

and the corresponding specific properties are:

`v = v_g`

`u = u_g`

`h = h_g`

`s = s_g`

This state represents vapor at the point where condensation can begin.

---

## Property combinations

Different combinations of known properties may require different calculation paths.

Examples include combinations involving:

- Pressure and temperature
- Pressure and enthalpy
- Pressure and entropy
- Pressure and specific volume
- Temperature and vapor quality
- Pressure and vapor quality

The availability of a specific input pair depends on the selected substance and the scientific data available to the system.

Not every mathematically possible pair is necessarily supported.

---

## Pressure and temperature

Pressure and temperature are among the most common known-property combinations.

Outside the saturation region, they can often be used together to determine a unique state.

For a fluid with liquid-vapor phase behavior, the supplied pressure and temperature may first be compared with the saturation condition.

Conceptually:

    P + T
      ↓
    Saturation comparison
      ↓
    Region detection
      ↓
    Relevant property data
      ↓
    Remaining properties

Within the two-phase region, pressure and temperature are linked by the saturation relationship and do not independently determine vapor quality.

---

## Pressure and vapor quality

If pressure and vapor quality are known for a saturated mixture, the system can use the saturation properties at that pressure and apply mixture relations.

Conceptually:

    P + x
      ↓
    Saturation data at P
      ↓
    y = y_f + x(y_g - y_f)
      ↓
    Mixture properties

The same principle can be applied to appropriate specific properties.

---

## Temperature and vapor quality

A similar calculation can be performed when temperature and vapor quality define a saturated state.

Conceptually:

    T + x
      ↓
    Saturation data at T
      ↓
    Mixture-property relations
      ↓
    Remaining properties

This calculation path applies only where vapor quality is physically meaningful.

---

## Region-dependent behavior

Thermodynamic properties cannot be interpreted independently of the state region.

The same input property may lead to a different calculation workflow depending on whether the substance is:

- Compressed liquid
- Saturated liquid
- Two-phase mixture
- Saturated vapor
- Superheated vapor

For this reason, region detection is a central part of the calculation process.

See:

[Region Detection](./region-detection.md)

---

## Interpolation

Thermodynamic property data is available at discrete states.

When a requested state lies between available data points, interpolation may be required before the remaining properties can be determined.

Thermo Table Bot supports:

- One-dimensional interpolation
- Two-dimensional interpolation

where applicable.

See:

[Interpolation](./interpolation.md)

---

## Exact data points

Interpolation is not required when the requested state corresponds directly to an available scientific data point.

Conceptually:

    Requested state
          ↓
    Exact data point found
          ↓
    Direct property retrieval

Using the exact available value avoids unnecessary numerical interpolation.

---

## Units and interpretation

Users should always verify the units shown by the bot when entering or interpreting thermodynamic properties.

A numerically correct value entered with an incorrect unit represents a different physical state and may therefore produce an invalid or unintended calculation.

Important examples include:

- Pressure units
- Temperature units
- Specific-energy units
- Specific-volume units
- Entropy units

Specific quantities are also defined on a mass basis, so their units must be interpreted accordingly.

---

## Property values and physical accuracy

The number of displayed decimal places should not be confused with physical accuracy.

Thermodynamic property values may be influenced by:

- Resolution of the scientific source data
- Rounding
- Interpolation
- Numerical precision
- Input precision

Displaying additional digits does not create additional physical information.

---

## Valid and unsupported states

A supported property name does not guarantee that every numerical value or property combination can be evaluated.

A calculation may be rejected when:

- The state lies outside the supported data range
- The property pair is unsupported
- The supplied properties are physically inconsistent
- The state cannot be uniquely determined
- The calculation would require unsupported extrapolation

Rejecting an unsupported state is preferable to returning a numerical value without sufficient scientific basis.

---

## Thermodynamic properties versus engineering analysis

Thermo Table Bot evaluates thermodynamic properties.

These properties are often inputs to larger engineering calculations.

For example:

- Enthalpy may be used in an energy balance
- Entropy may be used in second-law analysis
- Specific volume may be used in mass-flow or volume calculations
- Internal energy may be used in closed-system energy analysis

The bot does not automatically solve the entire engineering system simply because the required properties have been calculated.

The user remains responsible for applying the appropriate engineering equations and assumptions.

---

## Scientific interpretation

Thermodynamic properties should be interpreted as part of a physical state rather than as isolated numbers.

A useful workflow is:

    Known state information
              ↓
    Determine physical region
              ↓
    Evaluate thermodynamic properties
              ↓
    Check physical consistency
              ↓
    Use properties in engineering analysis

Thermo Table Bot automates the property-evaluation stage while preserving the need for physical interpretation.

---

## Scope of this documentation

This page describes the thermodynamic properties and public calculation principles used by Thermo Table Bot.

The following remain private:

- Production source code
- Internal scientific datasets
- Exact lookup algorithms
- Numerical thresholds
- Internal fallback logic
- Implementation-specific tolerances

---

## Related documentation

- [Project Overview](./overview.md)
- [How It Works](./how-it-works.md)
- [Supported Fluids](./supported-fluids.md)
- [Region Detection](./region-detection.md)
- [Interpolation](./interpolation.md)
- [Psychrometrics](./psychrometrics.md)
- [Examples](./examples.md)
- [Validation](./validation.md)
- [Limitations](./limitations.md)
- [FAQ](./faq.md)
