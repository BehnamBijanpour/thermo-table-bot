# Psychrometrics

Thermo Table Bot includes a dedicated psychrometric calculation system for evaluating the properties of humid air.

Psychrometrics describes the thermodynamic behavior of mixtures of dry air and water vapor and is widely used in HVAC, air-conditioning, drying, ventilation and environmental engineering calculations.

Instead of manually navigating a psychrometric chart or repeatedly solving coupled humid-air relationships, the user can provide a supported pair of known properties and obtain the remaining state information.

---

## Humid-air properties

The psychrometric system works with commonly used humid-air properties such as:

| Symbol | Property | Typical unit |
|---|---|---|
| `T_db` | Dry-bulb temperature | `°C` |
| `T_wb` | Wet-bulb temperature | `°C` |
| `T_dp` | Dew-point temperature | `°C` |
| `RH` | Relative humidity | `%` |
| `ω` | Humidity ratio | `kg water/kg dry air` |
| `h` | Specific enthalpy of humid air | `kJ/kg dry air` |

The exact calculation path depends on the pair of known properties supplied by the user.

---

## Dry-bulb temperature

Dry-bulb temperature, `T_db`, is the ordinary air temperature measured without intentionally introducing evaporative cooling at the temperature sensor.

It is one of the most common independent variables used in psychrometric calculations.

Dry-bulb temperature alone does not determine the moisture content of the air, so another independent humid-air property is required to define the state.

---

## Wet-bulb temperature

Wet-bulb temperature, `T_wb`, is associated with the combined effects of temperature and moisture content.

It is commonly used together with dry-bulb temperature to determine other humid-air properties.

For an ordinary unsaturated humid-air state:

`T_wb ≤ T_db`

The relationship between wet-bulb temperature and the remaining psychrometric properties depends on pressure and the thermodynamic relationships used for humid air.

---

## Dew-point temperature

Dew-point temperature, `T_dp`, is the temperature at which humid air becomes saturated when cooled under the appropriate psychrometric conditions.

At the dew point, water vapor begins to condense.

For an ordinary unsaturated humid-air state:

`T_dp ≤ T_db`

As the air approaches saturation, the dew-point temperature approaches the dry-bulb temperature.

At saturation:

`T_dp = T_db`

---

## Relative humidity

Relative humidity describes how close the water-vapor content of the air is to saturation at the same temperature.

A common representation is:

`RH = 100 × p_v / p_ws`

where:

- `p_v` is the partial pressure of water vapor
- `p_ws` is the saturation pressure of water vapor at the same temperature

For ordinary unsaturated or saturated humid-air states:

`0% ≤ RH ≤ 100%`

At saturation:

`RH = 100%`

Relative humidity is strongly temperature-dependent and should not be interpreted as a direct measure of the total mass of water vapor in the air.

---

## Humidity ratio

Humidity ratio, represented here by `ω`, expresses the mass of water vapor relative to the mass of dry air.

Its typical unit is:

`kg water/kg dry air`

For an ideal-gas treatment of the dry-air and water-vapor mixture, a commonly used psychrometric relationship is:

`ω = 0.621945 × p_v / (P - p_v)`

where:

- `p_v` is the partial pressure of water vapor
- `P` is the total pressure of the humid-air mixture

Humidity ratio is different from relative humidity.

Relative humidity describes proximity to saturation, while humidity ratio represents the amount of water vapor relative to dry air.

---

## Humid-air enthalpy

The specific enthalpy of humid air accounts for contributions from both dry air and water vapor.

It is commonly expressed per unit mass of dry air:

`kJ/kg dry air`

Humid-air enthalpy depends primarily on temperature and moisture content under the assumptions used in standard psychrometric analysis.

Thermo Table Bot can determine enthalpy as part of a supported humid-air state calculation.

---

## Defining a psychrometric state

A humid-air state cannot generally be determined from only one property.

The calculation requires a supported combination of independent state information.

Conceptually:

    Known humid-air properties
               ↓
        Input validation
               ↓
    Psychrometric state evaluation
               ↓
    Required intermediate quantities
               ↓
       Remaining properties
               ↓
        Consistency checks
               ↓
              Result

Different input combinations may require different calculation paths.

---

## Property relationships

Psychrometric properties are interconnected.

For example:

    Dry-bulb temperature
             +
      Relative humidity
             ↓
    Water-vapor state
             ↓
      Humidity ratio
             ↓
       Dew point
             ↓
        Enthalpy
             ↓
    Other supported properties

A different known pair may enter the calculation from another point in this relationship network.

The system therefore does not rely on a single fixed calculation sequence for every psychrometric problem.

---

## Saturation

Saturation is a central concept in psychrometrics.

At saturation, the partial pressure of water vapor reaches the saturation vapor pressure corresponding to the air temperature.

Conceptually:

`p_v = p_ws`

and therefore:

`RH = 100%`

At this condition, the dry-bulb and dew-point temperatures coincide.

Under the corresponding psychrometric definition, the wet-bulb temperature also approaches the dry-bulb temperature.

---

## Physical consistency

A numerical combination of psychrometric inputs does not automatically represent a physically meaningful humid-air state.

The calculation system therefore includes consistency checks.

Examples of physically relevant relationships include:

`T_dp ≤ T_db`

and, for ordinary unsaturated states:

`T_wb ≤ T_db`

Relative humidity should also remain within the supported physical range for the calculation.

Inputs that violate required physical relationships may be rejected rather than used to generate an unsupported result.

---

## Intermediate calculations

Some requested psychrometric properties cannot be obtained directly from a single explicit relationship.

A calculation may require intermediate quantities such as:

- Water-vapor partial pressure
- Saturation vapor pressure
- Humidity ratio
- Intermediate temperature-dependent properties

These intermediate quantities allow the system to connect different combinations of known and unknown humid-air properties.

---

## Numerical solution

Some psychrometric input combinations may lead to equations that are not most conveniently evaluated through a single direct expression.

In such cases, numerical methods may be required to determine an intermediate or final property.

The public documentation describes the scientific behavior of the system but does not expose implementation-specific numerical algorithms, convergence criteria or internal tolerances.

---

## Psychrometric calculations and charts

Traditional psychrometric analysis is often performed using a psychrometric chart.

The chart provides a graphical representation of relationships between humid-air properties.

Thermo Table Bot performs the numerical property evaluation directly rather than requiring the user to estimate values graphically from a chart.

The underlying physical relationships remain the same type of relationships studied in psychrometrics.

The tool is intended to automate repetitive calculation work, not replace understanding of the psychrometric chart or humid-air thermodynamics.

---

## Result generation

Depending on the supplied inputs and supported calculation path, a psychrometric result may include properties such as:

- Dry-bulb temperature
- Wet-bulb temperature
- Dew-point temperature
- Relative humidity
- Humidity ratio
- Enthalpy

The exact output depends on the state information provided by the user.

---

## Range and input handling

Psychrometric relationships are valid within defined physical and numerical ranges.

A requested state may be rejected when:

- Required inputs are missing
- The input pair is unsupported
- The supplied values are physically inconsistent
- A required quantity falls outside the supported calculation range
- A valid numerical solution cannot be obtained within the supported model

Rejecting unsupported states is preferable to returning a numerical value without sufficient scientific basis.

---

## Validation

The psychrometric engine is tested separately from the ordinary thermodynamic property-table workflow.

Validation includes evaluation of supported input combinations, physical consistency and agreement between calculated humid-air properties.

Detailed validation information is provided in:

[Validation](./validation.md)

---

## Engineering applications

Psychrometric calculations are widely used in engineering applications involving humid air, including:

- Heating and cooling
- Air conditioning
- Ventilation
- Dehumidification
- Humidification
- Drying processes
- Environmental control

Thermo Table Bot focuses on evaluating the humid-air properties required for these types of analyses.

The engineering process or system itself must still be interpreted and solved by the user.

---

## Scope of this documentation

This page describes the public scientific principles and behavior of the Thermo Table Bot psychrometric system.

The following remain private:

- Production source code
- Internal numerical algorithms
- Exact convergence criteria
- Numerical tolerances
- Internal fallback logic
- Production infrastructure

---

## Related documentation

- [Project Overview](./overview.md)
- [How It Works](./how-it-works.md)
- [Thermodynamic Properties](./thermodynamic-properties.md)
- [Examples](./examples.md)
- [Validation](./validation.md)
- [Limitations](./limitations.md)
- [FAQ](./faq.md)
