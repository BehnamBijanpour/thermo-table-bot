# Thermodynamic Properties

Thermo Table Bot works with the thermodynamic properties commonly used to define and analyze equilibrium states.

Depending on the selected substance, thermodynamic region and available input pair, the system can determine additional properties from the known state variables.

---

## Supported properties

The main thermodynamic properties used by the system are:

| Symbol | Property | Typical unit |
|---|---|---|
| `P` | Pressure | kPa |
| `T` | Temperature | °C |
| `v` | Specific volume | m³/kg |
| `u` | Specific internal energy | kJ/kg |
| `h` | Specific enthalpy | kJ/kg |
| `s` | Specific entropy | kJ/(kg·K) |
| `x` | Vapor quality | dimensionless |

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

\[
v = \frac{V}{m}
\]

It is commonly expressed in:

\[
m^3/kg
\]

Specific volume can be useful for identifying the state of a substance and distinguishing between liquid, two-phase and vapor regions.

---

## Specific internal energy — u

Specific internal energy represents the internal energy stored per unit mass of a substance.

It is commonly expressed in:

\[
kJ/kg
\]

Internal energy is frequently used in closed-system energy analysis and thermodynamic property calculations.

---

## Specific enthalpy — h

Specific enthalpy is defined by:

\[
h = u + Pv
\]

It is commonly expressed in:

\[
kJ/kg
\]

Enthalpy is especially important in steady-flow devices and engineering systems such as turbines, compressors, pumps, heat exchangers and nozzles.

---

## Specific entropy — s

Specific entropy is commonly expressed in:

\[
kJ/(kg \cdot K)
\]

Entropy is used extensively in second-law analysis and in the evaluation of thermodynamic processes and cycles.

---

## Vapor quality — x

Vapor quality describes the mass fraction of vapor in a saturated liquid-vapor mixture.

It is defined as:

\[
x = \frac{m_{vapor}}{m_{liquid} + m_{vapor}}
\]

For a two-phase mixture:

\[
0 < x < 1
\]

At the saturated-liquid boundary:

\[
x = 0
\]

At the saturated-vapor boundary:

\[
x = 1
\]

Vapor quality is only meaningful within the saturation region and at its boundaries.

---

## Two independent properties

For a simple compressible substance in equilibrium, the thermodynamic state can generally be fixed by two independent intensive properties.

Thermo Table Bot therefore uses supported pairs of known properties to determine the state and calculate the remaining quantities.

A conceptual workflow is:

```text
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
