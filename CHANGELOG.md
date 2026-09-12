# Changelog

All notable public changes to **Thermo Table Bot** are documented in this file.

This changelog tracks changes relevant to the public product, scientific capabilities, validation status and documentation.

The production source code and internal development history remain private.

---

## [1.0.0] - 2026-09-09

**Initial stable release**

Thermo Table Bot reached its intended feature-complete state with version `1.0.0`.

This release represents the final planned feature set of the project. Future updates, if required, will focus on maintenance, scientific corrections, reliability and documentation rather than feature expansion.

### Thermodynamic capabilities

- Thermodynamic property evaluation
- Automatic thermodynamic region detection
- One-dimensional interpolation
- Two-dimensional interpolation
- Saturation-state calculations
- Two-phase liquid-vapor calculations
- Vapor-quality calculations
- Refrigerant property calculations
- Engineering-gas property calculations
- Scientific input validation
- Physical consistency checking
- Reference and calculation-method reporting

### Supported substances

Version `1.0.0` includes thermodynamic property support for:

- Water
- Air
- Ammonia
- Carbon dioxide
- Methane
- Nitrogen
- R134a
- R410A

### Psychrometrics

Version `1.0.0` includes humid-air psychrometric calculations involving properties such as:

- Dry-bulb temperature
- Wet-bulb temperature
- Dew-point temperature
- Relative humidity
- Humidity ratio
- Enthalpy

### Scientific validation

The validated version `1.0.0` project snapshot reports:

- `412` automated tests passed
- `118 / 118` thermodynamic regression cases passed
- `14,000 / 14,000` psychrometric pair evaluations passed
- `10,000 / 10,000` stress-test cases passed
- `0` scientific invariant failures

Detailed methodology and validation scope are documented in [Validation](./docs/validation.md).

### Scientific data integrity

The production scientific data used by the system is tracked through an internal data manifest.

The project includes:

- Production-data file identification
- SHA-256 integrity tracking
- Scientific consistency checks
- Documented data corrections
- Regression testing against validated reference states

Additional public information is available in [Scientific References](./REFERENCES.md).

### Documentation

The public technical documentation for version `1.0.0` includes:

- Project overview
- System architecture and calculation workflow
- Supported fluids
- Thermodynamic properties
- Thermodynamic region detection
- One-dimensional and two-dimensional interpolation
- Psychrometric calculations
- Representative calculation examples
- Scientific validation
- System limitations
- Frequently asked questions
- Scientific references and data provenance
- Citation metadata
- Repository license and usage information

### Public interface

Thermo Table Bot is available through Telegram:

https://t.me/thermo_table_bot

---

## Release policy

Version `1.0.0` represents the intended final feature set of Thermo Table Bot.

No additional product features are currently planned.

Future releases, if necessary, may be issued for:

- Scientific corrections
- Bug fixes
- Reliability improvements
- Compatibility maintenance
- Documentation corrections
- Security or operational maintenance

A future maintenance release does not imply expansion of the project's intended feature set.

---

## Versioning

Public releases use semantic versioning where appropriate:

`MAJOR.MINOR.PATCH`

For the current feature-complete project, future version changes are expected primarily to represent maintenance or corrective updates rather than planned feature development.

---

## What this changelog tracks

This file may document changes to:

- Scientific behavior
- Calculation correctness
- Supported production behavior
- Validation status
- Reliability
- User-facing behavior
- Public documentation
- Public releases

---

## What this changelog does not expose

Because Thermo Table Bot is proprietary software, this changelog does not provide internal development details such as:

- Private source-code changes
- Internal scientific datasets
- Private test implementation
- Exact internal numerical tolerances
- Security-sensitive implementation details
- Server configuration
- Deployment infrastructure

---

## Related documentation

- [Project Overview](./docs/overview.md)
- [How It Works](./docs/how-it-works.md)
- [Supported Fluids](./docs/supported-fluids.md)
- [Validation](./docs/validation.md)
- [Limitations](./docs/limitations.md)
- [FAQ](./docs/faq.md)
- [Scientific References](./REFERENCES.md)
