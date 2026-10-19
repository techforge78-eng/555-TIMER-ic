# 555 Timer Traffic Light Controller: 2-Layer PCB

A traffic light controller built around the IC 555 timer, designed as a 2-layer PCB in KiCad, fabricated externally, and demonstrated at college. The project's main lesson was debugging a real hardware fault: **overheating caused by under-sized power traces**, fixed using IPC-2221 trace-width sizing.

**Type:** College project
**Tools:** KiCad · IC 555 · IPC-2221 · multimeter / oscilloscope

---

## Overview

The circuit uses a 555 timer to sequence `[number]` LEDs through red, yellow, and green phases.

- **Timing:** `[astable/monostable setup, approximate durations per phase]`
- **Sequencing:** `[how phases are driven, e.g. counter IC such as CD4017, transistors]`
- **Supply:** `[voltage and source]`

## Hardware

| Item | Details |
|------|---------|
| Timer | NE555 `[or equivalent]` |
| LEDs | `[count, colours, current per LED]` |
| Supporting parts | `[resistors, capacitors, transistors, etc.]` |
| PCB | 2-layer, KiCad, fabricated externally |

### Schematic

![Schematic](images/schematic.png)

### PCB layout

![PCB](images/pcb_layout.png)

### Finished board

![Finished board](images/board_photo.jpg)

## The debugging story: overheating traces

**Symptom.** During the college demonstration, the board ran hot near the power path.

**Root cause.** The power traces were too narrow for the load current, so they dissipated excess heat.

**Fix.** I recalculated the required trace width from the load current using the **IPC-2221** standard.

| Quantity | Value |
|----------|-------|
| Load current | `[X A]` |
| Copper weight | `[1 oz/ft²]` |
| Allowed temperature rise | `[X °C]` |
| Original trace width | `[X mm]` |
| Required width (IPC-2221) | `[X mm]` |

**Verification.** I also checked the resistor values by hand calculation and confirmed them with a multimeter, so the LED currents matched the design.

**Lesson learned.** Size power traces from the actual current *before* layout, not after. Trace width is a design parameter, not a cosmetic choice.

## What I'd do differently

- Calculate trace widths during schematic review and set them as KiCad net classes
- Run DRC with proper clearance and width rules for power nets
- Add test points for current and voltage measurement
- Use wider copper pours on power nets

## Repository structure

```
555-traffic-light-pcb/
├── hardware/      # KiCad project files
├── images/        # schematic, layout, photos
├── docs/          # calculations (IPC-2221, resistor values)
└── README.md
```

## Acknowledgements

Board fabrication was arranged with guidance from Code Core.

## Author

**Dharineesh T A**, Embedded Hardware & IoT Engineer (fresher)
[LinkedIn](https://linkedin.com/in/dharineesh-thangavel) · [GitHub](https://github.com/techforge78-eng)
