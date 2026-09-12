# Scientific References

Thermo Table Bot uses published thermodynamic property data, established engineering relations and independently checked scientific reference cases.

This document records the scientific references that are explicitly associated with the current project implementation and validation process.

The production datasets themselves are private and are not distributed through this repository.

---

## Primary thermodynamic reference

The primary documented source for the thermodynamic property tables used by Thermo Table Bot is:

**Claus Borgnakke and Richard E. Sonntag**  
*Fundamentals of Thermodynamics*  
**8th Edition**

The source is also historically associated with the Van Wylen thermodynamics textbook series and is identified inside the project as:

> Fundamentals of Thermodynamics 8th Edition  
> (Formerly Van Wylen)

Thermo Table Bot uses structured thermodynamic data derived from the corresponding standard property-table system.

---

## Thermodynamic table structure

The production thermodynamic engine uses table identifiers consistent with the documented source structure.

Examples include:

| Table family | Application |
|---|---|
| `B.1.1` | Saturated water — temperature basis |
| `B.1.2` | Saturated water — pressure basis |
| `B.1.3` | Superheated water vapor |
| `B.1.4` | Compressed liquid water |
| `B.2.x` | Ammonia property data |
| `B.3.x` | Carbon dioxide property data |
| `B.4.x` | R410A property data |

Additional structured datasets are used for the other supported substances documented by the project.

See [Supported Fluids](./docs/supported-fluids.md).

---

## Supported thermodynamic substances

The current scientific data layer contains thermodynamic property data for:

- Water
- Air
- Ammonia
- Carbon dioxide
- Methane
- Nitrogen
- R134a
- R410A

The exact available regions and property combinations differ between substances.

---

## Psychrometric methodology

The psychrometric engine uses established moist-air engineering relations for quantities including:

- Saturation vapor pressure
- Relative humidity
- Humidity ratio
- Moist-air enthalpy
- Specific volume
- Dew-point temperature
- Wet-bulb temperature

The implementation includes a piecewise logarithmic saturation-pressure correlation over water and ice and standard moist-air mass and energy relationships.

The production source currently describes these as standard engineering psychrometric relations but does not attach a complete bibliographic citation to every implemented correlation.

For that reason, this document does not assign an unverified external reference to those equations.

See [Psychrometrics](./docs/psychrometrics.md) for the publicly documented calculation methodology.

---

## Psychrometric validation references

The automated validation suite includes independent comparisons against published engineering examples.

### Çengel psychrometric-chart reference

One validation case uses a published psychrometric-chart example associated with Çengel.

The reference state is based on:

- Dry-bulb temperature: `35 °C`
- Relative humidity: `40 %`
- Pressure: `101.325 kPa`

The automated validation compares calculated quantities including:

- Humidity ratio
- Enthalpy
- Wet-bulb temperature
- Dew-point temperature
- Specific volume

The exact edition metadata for this validation reference is not recorded in the current production source and is therefore not asserted here.

### Van Wylen adiabatic-saturation reference

Another independent validation case uses a Van Wylen worked example involving approximately:

- Dry-bulb temperature: `84 °F`
- Wet-bulb temperature: `70 °F`
- Pressure: `14.7 psia`

The calculated humidity ratio and relative humidity are checked against the published reference values.

These reference cases are part of the wider psychrometric validation process documented in [Validation](./docs/validation.md).

---

## Scientific data integrity

The thermodynamic datasets used by the production system are tracked through a scientific data manifest.

The project records:

- Production-data file identity
- File role
- File size
- SHA-256 integrity hashes
- Documented scientific corrections

This allows the scientific data used by the calculation engine to be checked for unintended modification.

The private production files and their complete integrity manifest are not published in this repository.

---

## Documented data corrections

During scientific auditing, a small number of source or transcription inconsistencies were identified and corrected before use in production.

The corrections were retained as explicit provenance records rather than being silently changed.

### Saturated water at 75 kPa

A saturated-liquid internal-energy value was corrected after the original value violated independent thermodynamic consistency relationships.

The corrected value restores consistency with relationships involving:

- Saturated internal-energy components
- Enthalpy
- Pressure
- Specific volume

### Saturated ammonia at 70 °C

A saturated-vapor entropy value was corrected after the original value violated the relationship between:

- Saturated-liquid entropy
- Entropy of vaporization
- Saturated-vapor entropy

The corrected value is also consistent with later Borgnakke table reproductions.

### Superheated water at 10 kPa and 1300 °C

A superheated-water entropy entry was corrected after the source value was identified as a transcription or extraction error.

The corrected value was independently corroborated and found to be consistent with the thermodynamic trend of the surrounding data.

Further details about the validation philosophy are available in [Validation](./docs/validation.md).

---

## Thermodynamic consistency checks

The scientific audit does not rely only on visual comparison with published tables.

Where applicable, the project also checks relationships such as:

`h = u + Pv`

and saturation-property identities involving quantities such as:

- `u_f`
- `u_g`
- `u_fg`
- `h_f`
- `h_g`
- `h_fg`
- `s_f`
- `s_g`
- `s_fg`

These checks are used to identify transcription-scale errors that may still appear numerically plausible.

---

## Interpolation

Thermo Table Bot performs interpolation between supported scientific data points when an exact tabulated state is unavailable.

The project supports:

- One-dimensional interpolation
- Two-dimensional interpolation

Interpolation does not create a new underlying thermodynamic reference source. It numerically evaluates states between the documented data points.

See [Interpolation](./docs/interpolation.md).

---

## Reference data versus validation data

Thermo Table Bot distinguishes between two different roles for external scientific material.

### Production reference data

These are the thermodynamic data used directly by the calculation engine.

### Independent validation references

These are external examples, physical identities and comparison cases used to test whether the implementation reproduces expected scientific behavior.

Keeping these roles separate helps prevent a validation case from being incorrectly presented as the source of the entire production dataset.

---

## Scientific transparency

This repository documents the scientific basis of Thermo Table Bot without publishing proprietary production assets.

Publicly documented information includes:

- Primary thermodynamic reference
- Table families
- Supported substances
- Property definitions
- Calculation methodology
- Region-detection methodology
- Interpolation methodology
- Psychrometric methodology
- Validation results
- Known limitations
- Documented data-quality procedures

Private information includes:

- Production spreadsheets
- Complete internal data manifest
- Internal source code
- Exact implementation thresholds
- Private automated tests
- Deployment infrastructure

---

## Citation of Thermo Table Bot

For academic or educational work involving Thermo Table Bot itself, use the citation metadata provided in:

[`CITATION.cff`](./CITATION.cff)

---

## Related documentation

- [Project Overview](./docs/overview.md)
- [Supported Fluids](./docs/supported-fluids.md)
- [Thermodynamic Properties](./docs/thermodynamic-properties.md)
- [Interpolation](./docs/interpolation.md)
- [Psychrometrics](./docs/psychrometrics.md)
- [Validation](./docs/validation.md)
- [Limitations](./docs/limitations.md)
