# Examples

This page presents representative calculation workflows for Thermo Table Bot.

The examples are intended to demonstrate how thermodynamic and psychrometric states are handled conceptually.

Numerical values shown in simplified examples are illustrative and should not be interpreted as the internal production dataset used by Thermo Table Bot.

---

## Example 1 — Water from pressure and temperature

Suppose the known properties are:

- Substance: Water
- Pressure: `P`
- Temperature: `T`

The system first compares the supplied temperature with the saturation condition at the given pressure.

Conceptually:

    Input:
    Water
    P
    T
      ↓
    Find saturation condition at P
      ↓
    Compare T with T_sat
      ↓
    Detect thermodynamic region
      ↓
    Select relevant property data
      ↓
    Direct lookup or interpolation
      ↓
    Return remaining properties

Depending on the state, the result may correspond to:

- Compressed liquid
- Saturation condition
- Superheated vapor

Once the region is known, properties such as specific volume, internal energy, enthalpy and entropy can be determined when supported.

---

## Example 2 — Superheated water requiring interpolation

Consider a water state located in the superheated-vapor region.

Suppose the requested temperature lies between two available temperature entries at the required pressure.

A simplified table region may look like:

| Temperature | Enthalpy |
|---:|---:|
| `T₁` | `h₁` |
| `T₂` | `h₂` |

with:

`T₁ < T < T₂`

The system can evaluate the requested enthalpy using interpolation:

`h = h₁ + (T - T₁) × (h₂ - h₁) / (T₂ - T₁)`

The same interpolation position can be used with other relevant properties when appropriate.

Conceptually:

    P and T
      ↓
    Superheated region detected
      ↓
    Surrounding data located
      ↓
    Interpolation
      ↓
    h, v, u, s, ...

The actual production calculation uses the scientific data associated with the selected state.

---

## Example 3 — Two-phase water state

Suppose a state lies inside the saturated liquid-vapor region.

If an appropriate mixture property `y` is known, vapor quality can be evaluated from:

`x = (y - y_f) / (y_g - y_f)`

where:

- `y_f` is the saturated-liquid value
- `y_g` is the saturated-vapor value
- `x` is vapor quality

For a valid two-phase mixture:

`0 < x < 1`

Once quality is known, another appropriate property `z` can be evaluated using:

`z = z_f + x(z_g - z_f)`

Conceptually:

    Known saturation state
            +
    Known mixture property
            ↓
      Determine quality
            ↓
    Calculate remaining
    mixture properties

This workflow is fundamentally different from ordinary interpolation between two single-phase table entries.

---

## Example 4 — Saturated liquid

Consider a state known to be saturated liquid.

At the saturated-liquid boundary:

`x = 0`

Properties correspond to the saturated-liquid values:

`v = v_f`

`u = u_f`

`h = h_f`

`s = s_f`

The system therefore uses the saturated-liquid side of the relevant saturation data.

---

## Example 5 — Saturated vapor

For a saturated-vapor state:

`x = 1`

Properties correspond to the saturated-vapor values:

`v = v_g`

`u = u_g`

`h = h_g`

`s = s_g`

This state lies at the vapor boundary of the two-phase region.

---

## Example 6 — Refrigerant calculation

Thermo Table Bot also supports refrigerants such as:

- R134a
- R410A
- Ammonia

A refrigerant workflow follows the same general scientific structure:

    Select refrigerant
          ↓
    Enter supported known properties
          ↓
    Validate input pair
          ↓
    Determine thermodynamic state
          ↓
    Select relevant property data
          ↓
    Interpolate if required
          ↓
    Return calculated properties

The exact available properties and state regions depend on the scientific data available for the selected refrigerant.

---

## Example 7 — Engineering gas calculation

Supported engineering gases include:

- Air
- Carbon dioxide
- Methane
- Nitrogen

For these substances, the calculation path depends on the available gas-property data and selected input variables.

A simplified workflow is:

    Select gas
        ↓
    Enter known state variables
        ↓
    Locate relevant property data
        ↓
    Direct lookup or interpolation
        ↓
    Return supported properties

The specific property relationships and available ranges depend on the selected gas.

---

## Example 8 — Two-dimensional interpolation

Some states require interpolation in two independent dimensions.

Suppose a property depends on pressure and temperature:

`y = f(P, T)`

and the requested state lies between four surrounding data points:

                 T₁              T₂

    P₁          y₁₁             y₁₂

    P₂          y₂₁             y₂₂

with:

`P₁ < P < P₂`

and:

`T₁ < T < T₂`

The calculation can conceptually proceed in two stages.

First, interpolate at each surrounding pressure level:

`y_A = interpolation between y₁₁ and y₁₂`

`y_B = interpolation between y₂₁ and y₂₂`

Then interpolate between the intermediate values:

`y = interpolation between y_A and y_B`

Conceptually:

    Four surrounding values
             ↓
    Interpolation in first dimension
             ↓
      Two intermediate values
             ↓
    Interpolation in second dimension
             ↓
          Final property

The production implementation determines the appropriate interpolation path from the organization of the scientific data.

---

## Example 9 — Psychrometric state from dry-bulb temperature and relative humidity

Consider humid air with known:

- Dry-bulb temperature: `T_db`
- Relative humidity: `RH`

A conceptual workflow is:

    T_db + RH
        ↓
    Determine saturation vapor pressure
        ↓
    Determine water-vapor partial pressure
        ↓
    Determine humidity ratio
        ↓
    Evaluate remaining humid-air properties
        ↓
    Psychrometric result

The resulting state may include properties such as:

- Humidity ratio
- Dew-point temperature
- Wet-bulb temperature
- Enthalpy

The exact internal calculation sequence may vary depending on the input pair.

---

## Example 10 — Dew-point calculation

Suppose the humid-air state is known from a supported pair of properties.

The system can determine the water-vapor condition and then evaluate the temperature at which that vapor content reaches saturation.

That temperature is the dew-point temperature.

Conceptually:

    Known humid-air state
            ↓
    Water-vapor partial pressure
            ↓
    Saturation condition
            ↓
       Dew-point temperature

For an ordinary unsaturated state:

`T_dp < T_db`

At saturation:

`T_dp = T_db`

---

## Example 11 — Wet-bulb calculation

Wet-bulb temperature is connected to both the thermal and moisture state of humid air.

Depending on the known input pair, its determination may require a numerical calculation rather than a single direct lookup.

Conceptually:

    Known humid-air properties
              ↓
    Psychrometric relationships
              ↓
    Numerical evaluation if required
              ↓
          T_wb

The internal numerical solver, tolerances and convergence logic are part of the private production implementation.

---

## Example 12 — Exact table value

Not every calculation requires interpolation.

If the requested state corresponds directly to an available data point:

    Requested state
          ↓
    Exact match found
          ↓
    Direct property retrieval
          ↓
         Result

This preserves the available scientific data without introducing unnecessary interpolation.

---

## Example 13 — State outside the supported range

Suppose a requested state lies outside the available scientific data.

The system should not automatically extend the property trend beyond the supported range.

Conceptually:

    User input
        ↓
    Range validation
        ↓
    Outside supported data
        ↓
    Calculation rejected

This distinction is important because interpolation and extrapolation are not the same operation.

Thermo Table Bot is designed to avoid presenting unsupported extrapolated values as validated thermodynamic results.

---

## Example 14 — Physically inconsistent psychrometric input

Consider a humid-air input combination that violates a required physical relationship.

For example, under ordinary unsaturated conditions:

`T_dp ≤ T_db`

If supplied inputs imply a dew-point temperature greater than the dry-bulb temperature, the state may be physically inconsistent within the supported model.

Conceptually:

    Input properties
          ↓
    Physical consistency checks
          ↓
    Invalid relationship detected
          ↓
    Reject unsupported state

Returning an error is preferable to generating a numerical result from an inconsistent state.

---

## What the user sees

A typical Thermo Table Bot result can contain information such as:

- Detected thermodynamic region
- Calculated properties
- Vapor quality when applicable
- Reference-table information
- Calculation method
- Interpolation information when required

The exact result depends on the selected substance and calculation mode.

---

## Example calculation philosophy

Thermo Table Bot separates engineering reasoning from repetitive property evaluation.

The intended workflow is:

    Understand the problem
            ↓
    Identify the known state variables
            ↓
    Submit the supported properties
            ↓
    Thermo Table Bot evaluates the state
            ↓
    Use the returned properties
            ↓
    Continue solving the engineering problem

The tool performs the repetitive numerical work, while interpretation of the physical system remains the responsibility of the student or engineer.

---

## Numerical examples and production data

Simplified numerical examples in this documentation are included only to explain calculation concepts.

They are not a publication of:

- Internal production tables
- Proprietary datasets
- Complete thermodynamic databases
- Internal interpolation grids
- Numerical thresholds
- Production source code

The scientific datasets used by the deployed system remain private.

---

## Related documentation

- [How It Works](./how-it-works.md)
- [Supported Fluids](./supported-fluids.md)
- [Thermodynamic Properties](./thermodynamic-properties.md)
- [Region Detection](./region-detection.md)
- [Interpolation](./interpolation.md)
- [Psychrometrics](./psychrometrics.md)
- [Validation](./validation.md)
- [Limitations](./limitations.md)
