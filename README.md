# Thermo Table Bot

A scientific thermodynamics and psychrometrics tool by **B-Logic**, available directly in Telegram.

Thermo Table Bot helps engineering students and practitioners retrieve thermodynamic properties, perform interpolation, identify thermodynamic states, and solve humid-air calculations without manually navigating multiple property tables.

> This repository contains the public technical documentation of Thermo Table Bot.  
> The production source code and internal scientific datasets are not publicly released.

---

## What does Thermo Table Bot do?

Thermo Table Bot is designed to handle the repetitive numerical part of thermodynamic table work while keeping the user focused on the engineering problem itself.

It can:

- Calculate thermodynamic properties from two independent inputs
- Automatically determine the thermodynamic region
- Perform one-dimensional and two-dimensional interpolation
- Work with water, refrigerants, gases and air
- Perform psychrometric calculations for humid air
- Report the reference table used in the calculation
- Show the calculation method used to obtain the result

---

## Supported properties

Depending on the selected substance and calculation mode, the bot works with properties such as:

- Pressure — `P`
- Temperature — `T`
- Specific volume — `v`
- Internal energy — `u`
- Enthalpy — `h`
- Entropy — `s`
- Vapor quality — `x`

---

## Supported substances

Thermo Table Bot currently supports thermodynamic calculations for:

- Water
- Air
- Ammonia
- Carbon dioxide
- Methane
- Nitrogen
- R134a
- R410A

Psychrometric calculations are also available for humid air.

---

## How it works

A typical calculation follows this workflow:

1. Select the calculation type
2. Select the working substance
3. Select two independent properties
4. Enter the known values
5. The system identifies the thermodynamic state
6. The required table and calculation method are selected
7. Interpolation is performed when necessary
8. The calculated properties are returned to the user

More technical details will be available in the documentation.

---

## Example output

A typical result may include:

- Thermodynamic region
- Specific volume
- Internal energy
- Enthalpy
- Entropy
- Reference table
- Interpolation method

Detailed calculation examples are available in the documentation.

---

## Documentation

Technical documentation is organized in the [`docs`](./docs) directory.

Topics include:

- Project overview
- System workflow
- Supported fluids
- Thermodynamic properties
- Region detection
- Interpolation
- Psychrometrics
- Calculation examples
- Validation
- Limitations
- Frequently asked questions

---

## Use Thermo Table Bot

Thermo Table Bot is available on Telegram:

**https://t.me/thermo_table_bot**

Official B-Logic website:

**https://b-logic.me/**

---

## Project status

Thermo Table Bot is an actively maintained scientific software project.

The public documentation is currently being expanded.

---

## Source code

The production source code, internal scientific datasets, server configuration and deployment infrastructure are proprietary and are not included in this repository.

This repository is intended for:

- Technical documentation
- Scientific methodology
- Validation results
- Usage examples
- Project information

---

## B-Logic

Thermo Table Bot is developed as part of **B-Logic**, an educational and scientific software project focused on mathematics, physics and engineering tools.
