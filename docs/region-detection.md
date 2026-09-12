# Region Detection

Before thermodynamic properties can be evaluated correctly, the system must determine which physical region contains the requested state.

Region detection is especially important for substances that can exist as compressed liquid, saturated liquid, two-phase mixture, saturated vapor or superheated vapor.

A numerical result without correct region identification may be physically meaningless even if the arithmetic itself is correct.

---

## Why region detection matters

Thermodynamic property relationships depend on the physical region of the substance.

For example, the same pressure may correspond to:

- A compressed-liquid state
- A saturated state
- A two-phase liquid-vapor mixture
- A superheated-vapor state

The system therefore does not treat all states with the same calculation path.

A simplified workflow is:

    Known properties
          ↓
    Compare with saturation conditions
          ↓
    Identify physical region
          ↓
    Select relevant property data
          ↓
    Continue calculation

---

## Saturation boundary

The saturation boundary separates single-phase liquid and vapor regions from the two-phase liquid-vapor region.

At a given saturation pressure, there is a corresponding saturation temperature.

Likewise, at a given saturation temperature, there is a corresponding saturation pressure.

These relationships are used as important reference points during state classification.

---

## Pressure-temperature classification

When pressure and temperature are both known, the state can conceptually be compared with the saturation temperature at the given pressure.

Let:

`T_sat = saturation temperature at pressure P`

Then:

`T < T_sat  →  Compressed liquid`

`T = T_sat  →  Saturation condition`

`T > T_sat  →  Superheated vapor`

The equality case requires additional information because a pressure-temperature pair on the saturation line does not uniquely determine vapor quality.

A saturated state may represent:

- Saturated liquid
- A two-phase mixture
- Saturated vapor

depending on the additional state information.

---

## Temperature-pressure classification

The same reasoning can be expressed in terms of saturation pressure.

Let:

`P_sat = saturation pressure at temperature T`

Then:

`P > P_sat  →  Compressed liquid`

`P = P_sat  →  Saturation condition`

`P < P_sat  →  Superheated vapor`

Both forms describe the same physical relationship from different input perspectives.

---

## Property-based region detection

Region detection is not limited to pressure-temperature input pairs.

Other property combinations may also be used to determine whether a state lies below, inside or above the saturation region.

For a property `y`, the system may conceptually compare the supplied value with the saturated-liquid and saturated-vapor limits:

`y_f = saturated-liquid value`

`y_g = saturated-vapor value`

Then:

`y < y_f  →  liquid-side state`

`y_f < y < y_g  →  two-phase mixture`

`y > y_g  →  vapor-side state`

The exact interpretation depends on the property being used and on the thermodynamic data available for that substance.

---

## Two-phase region

A state lies inside the saturated liquid-vapor region when the relevant property is between the saturated-liquid and saturated-vapor values.

For an appropriate specific property `y`:

`y_f < y < y_g`

The vapor quality can then be determined from:

`x = (y - y_f) / (y_g - y_f)`

where:

- `x` is vapor quality
- `y` is the mixture property
- `y_f` is the saturated-liquid value
- `y_g` is the saturated-vapor value

For a valid two-phase mixture:

`0 < x < 1`

Once quality is known, other mixture properties can be evaluated using:

`z = z_f + x(z_g - z_f)`

where `z` represents another appropriate specific property.

---

## Saturated liquid

At the saturated-liquid boundary:

`x = 0`

The state is entirely liquid but is at the point where vaporization can begin.

For an appropriate property:

`y = y_f`

---

## Saturated vapor

At the saturated-vapor boundary:

`x = 1`

The state is entirely vapor but is at the point where condensation can begin.

For an appropriate property:

`y = y_g`

---

## Compressed-liquid region

A compressed-liquid state exists on the liquid side of the saturation boundary.

In a pressure-temperature representation, this generally corresponds to:

`T < T_sat at the given pressure`

or equivalently:

`P > P_sat at the given temperature`

The calculation path for compressed-liquid states differs from the calculation path used for two-phase or superheated-vapor states.

---

## Superheated-vapor region

A superheated-vapor state exists on the vapor side of the saturation boundary.

In a pressure-temperature representation, this generally corresponds to:

`T > T_sat at the given pressure`

or equivalently:

`P < P_sat at the given temperature`

The system then uses the property data associated with the superheated region.

---

## Region detection with interpolation

The saturation state required for comparison may not correspond exactly to an available data point.

For example, a requested pressure may lie between two available saturation entries.

In that case, saturation properties may first need to be interpolated before the region can be classified.

Conceptually:

    Input state
        ↓
    Required saturation value available exactly?
       ↙                           ↘
     Yes                           No
      ↓                             ↓
    Direct value              Interpolate saturation data
       ↘                           ↙
          Compare state with boundary
                     ↓
              Identify region

This is one reason region detection and interpolation are closely related.

---

## Region detection from different property pairs

Different supported property pairs may require different classification logic.

Examples may include:

- Pressure and temperature
- Pressure and enthalpy
- Pressure and entropy
- Pressure and specific volume
- Temperature and vapor quality
- Pressure and vapor quality

The system selects the relevant comparison method according to the available inputs and scientific property data.

Not every possible property pair is supported for every substance.

---

## Saturation-line ambiguity

Pressure and temperature are not independent within the two-phase region.

If a state lies exactly on the saturation line, pressure and temperature alone are insufficient to determine where the state lies between saturated liquid and saturated vapor.

Additional information such as vapor quality or another independent property is required.

This is an important thermodynamic constraint rather than a software limitation.

---

## Boundary handling

Real numerical calculations involve finite precision.

Values very close to saturation boundaries may therefore require careful numerical comparison.

Thermo Table Bot includes internal handling for boundary conditions and floating-point comparisons.

Implementation-specific numerical tolerances and thresholds are part of the private production system and are not published in this repository.

---

## Invalid or unsupported states

Region detection also helps identify states that cannot be evaluated safely.

A calculation may be rejected when:

- The supplied properties are physically inconsistent
- The state falls outside the supported property-data range
- The selected property pair cannot uniquely define the state
- Required scientific data is unavailable
- The requested calculation would require unsupported extrapolation

In these cases, rejecting the state is preferable to returning an unsupported numerical value.

---

## Relationship with interpolation

Region detection should generally occur before property interpolation across a thermodynamic table.

The simplified order is:

    Inputs
      ↓
    Validation
      ↓
    Saturation comparison
      ↓
    Region detection
      ↓
    Relevant property dataset
      ↓
    Interpolation if required
      ↓
    Final properties

This avoids interpolating between data that belong to physically different thermodynamic regions.

---

## Scientific interpretation

Automatic region detection does not remove the need to understand phase behavior.

Its purpose is to automate the repetitive classification and table-selection work that would otherwise be performed manually.

The user should still understand why a state is classified as:

- Compressed liquid
- Saturated liquid
- Two-phase mixture
- Saturated vapor
- Superheated vapor

Thermo Table Bot performs the numerical workflow, while the physical interpretation remains part of thermodynamic analysis.

---

## Scope of this documentation

This page describes the public scientific logic used for thermodynamic region identification.

The following remain private:

- Production source code
- Internal scientific datasets
- Exact search algorithms
- Numerical tolerances
- Boundary thresholds
- Implementation-specific fallback logic

---

## Related documentation

- [Thermodynamic Properties](./thermodynamic-properties.md)
- [Interpolation](./interpolation.md)
- [Supported Fluids](./supported-fluids.md)
- [How It Works](./how-it-works.md)
- [Examples](./examples.md)
- [Validation](./validation.md)
- [Limitations](./limitations.md)
