# Thermodynamic Region Detection

Thermo Table Bot automatically identifies the thermodynamic region of a state when region detection is required for the selected calculation.

This step is essential because the same pair of input properties may require different property data and calculation paths depending on the physical state of the substance.

---

## Why region detection matters

Thermodynamic property data is organized according to physical regions.

For a substance undergoing liquid-vapor phase change, a state may belong to one of several regions:

- Compressed liquid
- Saturated liquid
- Two-phase liquid-vapor mixture
- Saturated vapor
- Superheated vapor

The system must identify the appropriate region before selecting property data or performing interpolation.

---

## Conceptual workflow

At a high level, region detection follows this sequence:

```text
Known properties
      ↓
Input validation
      ↓
Locate relevant saturation boundary
      ↓
Compare the state with boundary data
      ↓
Identify thermodynamic region
      ↓
Select the appropriate property data
      ↓
Continue calculation
