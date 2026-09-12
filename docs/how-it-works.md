# How It Works

Thermo Table Bot is structured as a scientific calculation system with a Telegram interface on top.

The user interacts with the bot through Telegram, while the underlying system handles state identification, data selection, interpolation, thermodynamic calculations and psychrometric relationships.

---

## High-level architecture

The system can be represented by the following logical layers:

```text
User
  ↓
Telegram Interface
  ↓
Calculation Workflow
  ↓
Thermodynamic Engine / Psychrometric Engine
  ↓
Scientific Data Layer
  ↓
Validation and Consistency Checks
