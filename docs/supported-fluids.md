# Supported Fluids

Thermo Table Bot currently supports thermodynamic property calculations for eight substances, covering water, refrigerants and common engineering gases.

The available calculation modes and properties depend on the selected substance and the thermodynamic data available for that substance.

---

## Supported substances

| Substance | Formula / Designation | Category |
|---|---:|---|
| Water | H₂O | Water / Steam |
| Air | Air | Gas |
| Ammonia | NH₃ | Refrigerant |
| Carbon dioxide | CO₂ | Gas |
| Methane | CH₄ | Gas |
| Nitrogen | N₂ | Gas |
| R134a | R134a | Refrigerant |
| R410A | R410A | Refrigerant |

---

## Water

Water is supported across the thermodynamic regions required for steam-table calculations.

Depending on the supplied state variables, the system can work with states including:

- Compressed liquid
- Saturated liquid
- Two-phase liquid-vapor mixture
- Saturated vapor
- Superheated vapor

Water calculations may involve properties such as pressure, temperature, specific volume, internal energy, enthalpy, entropy and vapor quality.

When an exact state is not directly available in the underlying property data, interpolation may be used.

---

## Refrigerants

Thermo Table Bot currently supports the following refrigerants:

- Ammonia (NH₃)
- R134a
- R410A

The system selects the appropriate thermodynamic data according to the refrigerant, known properties and identified state.

Interpolation is applied when required by the available property data.

---

## Engineering gases

The currently supported gases include:

- Air
- Carbon dioxide (CO₂)
- Methane (CH₄)
- Nitrogen (N₂)

Available properties and calculation paths depend on the selected gas and input variables.

---

## Humid air

Psychrometric calculations are handled separately from the standard thermodynamic property-table workflow.

The psychrometric system is designed for humid-air states and relationships between properties such as:

- Dry-bulb temperature
- Relative humidity
- Humidity ratio
- Enthalpy
- Dew-point temperature
- Wet-bulb temperature

For more information, see:

[Psychrometrics](./psychrometrics.md)

---

## Property availability

Not every property combination is necessarily available for every substance or thermodynamic region.

The calculation workflow depends on:

1. The selected substance
2. The supplied independent properties
3. The identified thermodynamic region
4. The available scientific property data
5. Whether interpolation is required

This prevents the system from treating all substances as if they shared an identical property model.

---

## Units

Input and output units depend on the selected calculation and property.

Users should always verify the displayed units when entering values and interpreting results.

Unit handling is part of the calculation workflow and is documented alongside the relevant calculation examples.

---

## Data and implementation

The production thermodynamic datasets used by Thermo Table Bot are maintained privately and are not distributed through this documentation repository.

This public documentation describes the supported substances and scientific behavior of the system without exposing the internal datasets or production implementation.

---

## Related documentation

- [Thermodynamic Properties](./thermodynamic-properties.md)
- [Region Detection](./region-detection.md)
- [Interpolation](./interpolation.md)
- [Psychrometrics](./psychrometrics.md)
- [Examples](./examples.md)
- [Validation](./validation.md)
