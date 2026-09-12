# Interpolation

Thermodynamic property tables contain values at discrete states, while engineering problems frequently require properties at states that fall between the listed data points.

Thermo Table Bot uses interpolation when the requested state is not directly available in the relevant thermodynamic property data.

Depending on the structure of the data and the known properties, the calculation may require one-dimensional or two-dimensional interpolation.

---

## Why interpolation is required

Consider a property table containing values at two temperatures:

    T₁  →  y₁
    T₂  →  y₂

If the required temperature `T` lies between `T₁` and `T₂`, the corresponding property `y` may need to be estimated from the surrounding values.

The same principle applies to pressure and other supported independent variables.

---

## One-dimensional interpolation

One-dimensional interpolation is used when the required value lies between two known data points along one independent variable.

For two points:

    (x₁, y₁)
    (x₂, y₂)

and a target value `x` between `x₁` and `x₂`, linear interpolation can be written as:

`y = y₁ + (x - x₁) × (y₂ - y₁) / (x₂ - x₁)`

Conceptually:

    Known point 1
          ↓
      Target state
          ↓
    Known point 2

Thermo Table Bot can apply this process when the requested state falls between available property values.

---

## Example of one-dimensional interpolation

Suppose a table contains:

| Temperature | Enthalpy |
|---:|---:|
| 100 °C | 2676 kJ/kg |
| 120 °C | 2716 kJ/kg |

For a target temperature of `110 °C`, the interpolation fraction is:

`(110 - 100) / (120 - 100) = 0.5`

The interpolated enthalpy is therefore:

`h = 2676 + 0.5 × (2716 - 2676)`

which gives:

`h = 2696 kJ/kg`

This simplified example demonstrates the interpolation principle. It is not intended to represent a specific production dataset used by Thermo Table Bot.

---

## Two-dimensional interpolation

Some thermodynamic states fall between available values along two independent dimensions.

A common conceptual example is a property that depends on both pressure and temperature:

`y = f(P, T)`

If neither the requested pressure nor temperature corresponds directly to an available data point, interpolation may be required in both dimensions.

A simplified data region may look like:

                  T₁              T₂

    P₁           y₁₁             y₁₂

    P₂           y₂₁             y₂₂

with the requested state located somewhere inside the surrounding data region.

---

## Conceptual two-dimensional workflow

A two-dimensional interpolation can be understood as a sequence of one-dimensional interpolation steps.

For example:

    y₁₁ ───────── y₁₂
           ↓
          y_A

    y₂₁ ───────── y₂₂
           ↓
          y_B

          y_A
           │
           │  second interpolation
           ↓
           y
           ↑
           │
          y_B

The system first determines the relevant surrounding data points and then evaluates the target property within that region.

The exact interpolation path depends on the organization of the property data and the supplied independent variables.

---

## Interpolation and region detection

Interpolation is not performed independently of thermodynamic state classification.

The general workflow is:

    User inputs
         ↓
    Input validation
         ↓
    Region detection
         ↓
    Relevant property data
         ↓
    Exact value available?
       ↙              ↘
     Yes              No
      ↓                ↓
    Direct lookup    Interpolation
       ↘              ↙
          Result

This prevents values from being interpolated across thermodynamic regions that require different physical treatment.

---

## Saturation data

Interpolation may also be required when locating saturation conditions.

For example, the requested pressure or temperature may lie between two available saturation entries.

In such cases, the required saturation properties can be evaluated between the surrounding data points before the calculation continues.

This can affect both:

- Region detection
- Final property calculation

---

## Two-phase calculations

Inside the saturated liquid-vapor region, mixture properties are related to vapor quality.

For an appropriate specific property `y`:

`y = y_f + x(y_g - y_f)`

where:

- `y_f` is the saturated-liquid value
- `y_g` is the saturated-vapor value
- `x` is vapor quality

If the mixture property is known and quality is required:

`x = (y - y_f) / (y_g - y_f)`

These relationships are distinct from ordinary table interpolation, although interpolation may first be required to determine the saturation properties at the requested pressure or temperature.

---

## Exact table values

Interpolation is unnecessary when the requested state corresponds directly to an available property-data point.

Conceptually:

    Requested state
          ↓
    Exact data point found
          ↓
    Direct property retrieval

This avoids introducing unnecessary numerical operations when an exact tabulated state is already available.

---

## Range checking

Interpolation is intended for states located between supported data points.

The system distinguishes interpolation from extrapolation.

A requested state outside the supported property-data range may therefore be rejected rather than estimated beyond the available data.

This behavior helps prevent unsupported numerical results from being presented as valid thermodynamic properties.

---

## Numerical handling

Interpolation involves floating-point calculations and comparisons between numerical values.

Thermo Table Bot includes internal numerical handling and consistency checks as part of the calculation workflow.

Implementation-specific tolerances, internal thresholds and production algorithms are not exposed in this public documentation.

---

## Result transparency

Where applicable, Thermo Table Bot can report information about the calculation method used to obtain a result.

This helps distinguish between values obtained through direct property lookup and values requiring interpolation.

Reference-table information may also be presented with the calculated result.

---

## Scope of this documentation

This page describes the interpolation principles and public behavior of Thermo Table Bot.

The production interpolation implementation, internal datasets, numerical thresholds and source code remain private.

---

## Related documentation

- [Thermodynamic Properties](./thermodynamic-properties.md)
- [Region Detection](./region-detection.md)
- [Supported Fluids](./supported-fluids.md)
- [Examples](./examples.md)
- [Validation](./validation.md)
- [Limitations](./limitations.md)
