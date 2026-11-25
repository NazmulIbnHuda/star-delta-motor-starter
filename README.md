# Star-Delta Motor Starter Panel

A hardware prototype of an automatic **star-delta (wye-delta) starter** for a three-phase squirrel-cage induction motor, built with magnetic contactors, an on-delay timer relay, a thermal overload relay, and push-button control.

Developed by Group 4 for **EEE206** at the Department of EEE, **Bangladesh University of Engineering and Technology (BUET)**, 2026.


## Why this project

Starting a large induction motor directly across the line (DOL) draws 5 to 7 times its rated current. That inrush stresses the windings, causes voltage dips on the supply, and can trip protection devices.

A star-delta starter connects the windings in **star** during start-up and then automatically switches them to **delta** for normal running. This reduces the starting line current and starting torque to roughly **one-third** of their DOL values.

## Key idea

| Quantity | Star (start) | Delta (run) |
|---|---|---|
| Voltage across each winding | V_L / √3 | V_L |
| Line current at start | ≈ 1/3 of DOL | Rated |
| Starting torque | ≈ 1/3 of DOL | Rated |

Because torque scales with voltage squared, (1/√3)² = 1/3. Phase current falls by 1/√3 in star, and star line current equals phase current while delta line current is √3 × phase current, so the combined reduction in line current is also 1/3.

## Features

- Automatic star → delta changeover using an adjustable on-delay timer (typically 5 to 10 s)
- Three contactors: main (KM1), star (KM2), delta (KM3)
- Electrical interlocking (NC auxiliary contacts) so star and delta can never close together, plus a mechanical interlock kit as backup
- Thermal overload protection
- Illuminated Start (green) and Stop (red) push buttons
- Colour-coded wiring: red for power, orange for control, with crimped lugs

## Operating sequence

1. **Start**: pressing Start energises KM1 (main) and KM2 (star). The motor runs with its windings in star.
2. **Star running**: the motor accelerates at reduced voltage while the on-delay timer counts.
3. **Changeover**: when the preset time elapses, the timer drops out KM2 and, after a short safety gap, energises KM3 (delta).
4. **Delta running**: the motor runs at full line voltage and rated torque.
5. **Stop / overload**: Stop or an overload trip de-energises the whole control circuit.

## Hardware

| Component | Qty | Purpose |
|---|---|---|
| LS GMC-22 magnetic contactor | 3 | Main, star, delta switching |
| Thermal overload relay | 1 | Motor protection |
| On-delay timer relay + 8-pin base | 1 | Star → delta changeover |
| MCCB / circuit breaker (3-phase and 1-phase) | 2 | Isolation and protection |
| Terminal connector block | 1 | Incoming and outgoing wiring |
| Illuminated push buttons (Start / Stop) | 2 | Operator control |
| Control and power wire, cable lugs, cable ties | - | Wiring |

### Cost breakdown (BDT)

| Item | Cost |
|---|---|
| Magnetic contactors (3 × 500) | 1,500 |
| Thermal overload relay | 600 |
| Timer relay + base | 700 |
| 3-phase CB | 500 |
| 1-phase CB | 300 |
| Terminal block | 200 |
| Push buttons | 60 |
| Wires and cable lugs | 500 |
| Cable ties and miscellaneous | 380 |
| **Total** | **≈ 4,740** |

## Build process

1. Mount the breaker, contactors, overload relay, and timer on the panel base.
2. Wire the power circuit: supply → breaker → overload relay → contactors.
3. Wire the control circuit: push buttons → interlock → timer → contactor coils.
4. Dress the wiring with cable ties and double-check every termination before powering on.

## Test setup

> Fill these in with your actual values.

| Parameter | Value |
|---|---|
| Motor | `[kW / HP, voltage, frequency]` |
| Supply | `[e.g. 3-phase 400 V, 50 Hz]` |
| Timer setting | `[ s ]` |
| Overload relay setting | `[ A ]` |

## Design analysis (calculated, not measured)

A separate design study sized the starter for an **assumed** 5.5 kW, 400 V, 50 Hz motor (pf 0.85, η 0.87, locked-rotor ratio 6.5). All figures below are calculations from typical values, not measurements from the prototype.

| Quantity | DOL | Star-delta |
|---|---|---|
| Full-load current | ≈ 10.8 A | ≈ 10.8 A |
| Starting line current | ≈ 70.2 A | ≈ 23.4 A |
| Starting torque (% of full load) | ≈ 150% | ≈ 50% |

Other design points in the report: AC-3 rated 20 A contactors, overload set to about 1.15 × full-load current, 2.5 mm² power conductors, and a failure-mode check showing that no single fault closes star and delta together.

## Safety

- Isolate and lock out the supply before any wiring or testing.
- Verify with a multimeter that no live voltage is present before touching terminals.
- Keep power and control wiring separated and colour-coded.
- Torque all terminal screws correctly. Loose connections overheat and arc.
- Never bypass the overload relay or omit the interlock during testing.

## Applications

Industrial pumps and compressors, conveyors and material handling, HVAC blowers and fans, crushers and mills, water treatment plants, and installations with supply-current restrictions.

Star-delta starting suits loads that do not need full torque at standstill. It is a poor fit for loaded conveyors or crushers that must start under heavy load.


## Team (Group 4, EEE206)

| ID | Name |
|---|---|
| 2306119 | Aritra Dash |
| 2306120 | Md. Shoyaib Ishtiyak |
| 2306121 | Nayeb Hossain |
| 2306122 | Bijoy Sarker |
| 2306123 | Nazmul Ibn Huda |
| 2306124 | Khadija Rahman |

## References

1. B. L. Theraja and A. K. Theraja, *A Textbook of Electrical Technology, Vol. II: AC & DC Machines*, S. Chand.
2. S. Chapman, *Electric Machinery Fundamentals*, McGraw-Hill.
3. IEC 60947-4-1, *Low-voltage switchgear and controlgear: Contactors and motor-starters*.
4. LS Electric, *GMC Series Magnetic Contactor* catalogue and datasheet.

## License

Released for educational use. Add a license file (for example MIT) if you want others to reuse it.
