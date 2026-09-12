# Thermo Table Bot Roadmap

This roadmap describes the current development direction of **Thermo Table Bot**.

It is intended to communicate project priorities without treating planned or experimental features as completed functionality.

Items listed here may change as the scientific scope, validation requirements and user needs evolve.

---

## Current foundation

The current documented system provides the scientific foundation for Thermo Table Bot.

### Thermodynamic calculations

- [x] Thermodynamic property evaluation
- [x] Automatic thermodynamic region detection
- [x] Saturation-state calculations
- [x] Two-phase liquid-vapor calculations
- [x] Vapor-quality calculations
- [x] One-dimensional interpolation
- [x] Two-dimensional interpolation

### Supported substances

- [x] Water
- [x] Air
- [x] Ammonia
- [x] Carbon dioxide
- [x] Methane
- [x] Nitrogen
- [x] R134a
- [x] R410A

### Psychrometrics

- [x] Humid-air property calculations
- [x] Relative-humidity calculations
- [x] Humidity-ratio calculations
- [x] Enthalpy calculations
- [x] Dew-point calculations
- [x] Wet-bulb calculations

### Scientific reliability

- [x] Automated scientific testing
- [x] Thermodynamic regression testing
- [x] Psychrometric validation
- [x] Stress testing
- [x] Scientific consistency checks
- [x] Production-data integrity tracking
- [x] Documented scientific data corrections

### Documentation

- [x] Project overview
- [x] Architecture and calculation workflow
- [x] Supported-fluid documentation
- [x] Thermodynamic-property documentation
- [x] Region-detection documentation
- [x] Interpolation documentation
- [x] Psychrometric documentation
- [x] Calculation examples
- [x] Validation documentation
- [x] Limitations
- [x] FAQ
- [x] Scientific references and data provenance
- [x] Citation metadata
- [x] Public changelog

---

## Near-term priorities

The next stage focuses primarily on improving scientific coverage, documentation quality and user experience.

### Documentation and transparency

- [ ] Continue improving technical documentation
- [ ] Expand representative calculation examples
- [ ] Add more visual explanations of calculation workflows
- [ ] Add selected diagrams for thermodynamic state and interpolation logic
- [ ] Improve documentation navigation as the repository grows

### Scientific validation

- [ ] Expand independent reference comparisons
- [ ] Add additional documented validation cases
- [ ] Continue regression testing as scientific capabilities evolve
- [ ] Extend boundary-condition testing
- [ ] Continue auditing scientific data provenance

### User experience

- [ ] Improve result readability
- [ ] Improve explanation of detected thermodynamic regions
- [ ] Improve communication of interpolation methods
- [ ] Improve handling and explanation of unsupported inputs
- [ ] Continue refining the Telegram interaction workflow

---

## Potential scientific expansion

The following directions are under consideration.

They are **not promises of future functionality** and should not be interpreted as currently supported features.

### Additional fluids

Potential expansion may include additional engineering fluids or refrigerants where reliable scientific data and adequate validation can be established.

Any new substance should pass the same general process:

    Scientific reference
            ↓
    Structured data preparation
            ↓
    Data integrity checks
            ↓
    Calculation integration
            ↓
    Regression testing
            ↓
    Independent validation
            ↓
    Public documentation

A substance should not be considered supported merely because property data can be obtained for it.

---

## Potential calculation capabilities

Future research may investigate additional thermodynamic calculation modes where they fit the scope of the project.

Possible directions include:

- Additional supported property pairs
- Broader thermodynamic state coverage
- Additional saturation-related workflows
- Expanded psychrometric state combinations
- Improved numerical treatment near difficult region boundaries

Each capability would require scientific validation before being documented as supported.

---

## Visualization

Visual scientific output is a potential area of future development.

Possible directions include:

- Thermodynamic state visualization
- Property-diagram integration
- Psychrometric visualization
- Visual indication of calculated states
- Graphical representation of interpolation

These features remain exploratory unless explicitly documented as released.

---

## Educational integration

Thermo Table Bot is designed around the principle that automation should support thermodynamics education rather than replace it.

Potential educational development may include:

- More worked examples
- Explanations of state identification
- Interpolation demonstrations
- Thermodynamic-table reading guides
- Psychrometric calculation guides
- Connections between bot results and engineering problem solving

Educational material may be published through the Thermo Table Bot documentation or B-Logic.

---

## Platform development

Telegram is currently the primary public interface to Thermo Table Bot.

Other interfaces may be evaluated in the future if they provide meaningful educational or engineering value.

No additional platform should be considered officially supported unless it is explicitly documented by the project.

---

## Scientific development principle

New features are not considered complete simply when they produce numerical output.

The preferred development path is:

    Scientific basis
          ↓
    Implementation
          ↓
    Automated testing
          ↓
    Physical consistency checks
          ↓
    Independent validation
          ↓
    Documentation
          ↓
    Public support

This principle is intended to keep scientific reliability ahead of feature count.

---

## What is not on the public roadmap

Some internal development work is intentionally excluded from this document.

This may include:

- Security-related changes
- Private infrastructure
- Deployment architecture
- Internal monitoring
- Private test implementation
- Exact numerical thresholds
- Internal scientific-data processing
- Proprietary implementation details

The public roadmap focuses on capabilities that are meaningful to users and to the scientific documentation of the project.

---

## Roadmap status

This document describes direction rather than a fixed delivery schedule.

There are currently no public deadlines attached to the items listed above.

A roadmap item becomes part of the documented current feature set only after it has been implemented, scientifically evaluated and reflected in the appropriate project documentation.

---

## Follow project changes

Publicly documented changes are recorded in:

[CHANGELOG.md](./CHANGELOG.md)

Technical documentation is available in:

[docs/](./docs)

Thermo Table Bot:

https://t.me/thermo_table_bot

B-Logic:

https://b-logic.me/
