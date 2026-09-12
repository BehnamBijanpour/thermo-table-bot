# Changelog

All notable public changes to **Thermo Table Bot** will be documented in this file.

This changelog tracks changes relevant to the public product, scientific capabilities, validation status and documentation.

The production source code and internal development history remain private.

---

## [Unreleased]

### Scientific capabilities

- Thermodynamic property evaluation for supported substances
- Automatic thermodynamic region detection
- One-dimensional interpolation
- Two-dimensional interpolation
- Saturation-state calculations
- Two-phase liquid-vapor calculations
- Vapor-quality calculations
- Refrigerant property calculations
- Engineering-gas property calculations
- Humid-air psychrometric calculations
- Scientific input validation
- Physical consistency checking

### Supported substances

The documented thermodynamic system currently includes:

- Water
- Air
- Ammonia
- Carbon dioxide
- Methane
- Nitrogen
- R134a
- R410A

### Validation

The currently documented validated project snapshot reports:

- `412` automated tests passed
- `118 / 118` thermodynamic regression cases passed
- `14,000 / 14,000` psychrometric pair evaluations passed
- `10,000 / 10,000` stress-test cases passed
- `0` scientific invariant failures

Detailed methodology and scope are documented in [Validation](./docs/validation.md).

### Documentation

Added public technical documentation for:

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

### Repository

- Established the public Thermo Table Bot documentation repository
- Added project branding and repository hero image
- Added direct navigation to Telegram, documentation and B-Logic
- Added a documentation map to the main README
- Added public scientific validation summary
- Documented the separation between public technical documentation and the private production implementation

---

## Versioning policy

Future public releases may use semantic versioning where appropriate:

`MAJOR.MINOR.PATCH`

In general:

- **MAJOR** — significant changes that alter documented behavior or compatibility
- **MINOR** — new supported capabilities, fluids, calculation modes or substantial features
- **PATCH** — fixes, validation improvements, documentation corrections or minor behavior changes

A version number will only be recorded here when a corresponding public project version is intentionally identified.

---

## What this changelog tracks

This file may document changes to:

- Supported substances
- Supported property combinations
- Thermodynamic calculation capabilities
- Region-detection behavior
- Interpolation capabilities
- Psychrometric calculations
- Scientific validation status
- User-facing behavior
- Public documentation
- Public project releases

---

## What this changelog does not expose

Because Thermo Table Bot is proprietary software, this changelog does not provide internal development details such as:

- Private source-code changes
- Internal architecture details not included in the public documentation
- Security-related changes that should remain confidential
- Deployment credentials or infrastructure details
- Internal scientific datasets
- Private test implementation
- Exact internal numerical tolerances

Public entries are intended to describe meaningful product and scientific changes without exposing the private production implementation.

---

## Related documentation

- [Project Overview](./docs/overview.md)
- [How It Works](./docs/how-it-works.md)
- [Supported Fluids](./docs/supported-fluids.md)
- [Validation](./docs/validation.md)
- [Limitations](./docs/limitations.md)
- [FAQ](./docs/faq.md)
