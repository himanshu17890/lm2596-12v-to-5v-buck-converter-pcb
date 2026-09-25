# LM2596 12 V to 5 V Buck Converter PCB

A two-layer PCB for converting a 12 V DC input into a regulated 5 V DC output using an LM2596S-5 switching regulator.

<img width="1447" height="852" alt="image" src="https://github.com/user-attachments/assets/0308cf2c-251b-46f2-9d53-f1cea19619a3" />

## Features

- 12 V DC input through a 2-pin screw terminal
- Fixed 5 V DC output through a 2-pin screw terminal
- LM2596S-5 buck regulator
- Up to 3 A regulator rating; final usable current depends on cooling, copper area, and component ratings
- Two-layer layout with F.Cu and B.Cu ground pours
- Two M2 mounting holes and rounded board corners

## Connections

| Terminal | Pin 1 | Pin 2 |
|---|---|---|
| J3 input | IN+ / +12 V | IN- / GND |
| J4 output | OUT+ / +5 V | OUT- / GND |

Use DC input only. Do **not** connect AC mains. Confirm the output is approximately 5.0 V with a multimeter before connecting a load, and never reverse the input polarity.

## Main Components

| Reference | Component | Value / requirement |
|---|---|---|
| U1 | LM2596S-5 | Fixed 5 V buck regulator, TO-263-5 package |
| C1 | Polarized electrolytic capacitor | 680 uF, 25 V |
| C2 | Low-ESR polarized electrolytic capacitor | 220 uF, 10 V |
| L1 | Power inductor | 33 uH, at least 3 A saturation current |
| D1 | Schottky diode | 1N5824 or equivalent |
| J3, J4 | Screw terminals | 2-pin, 5.00 mm pitch |

## Project Files

Place the KiCad files in this repository root:

- `LM2596_Buck_Converter.kicad_pro`
- `LM2596_Buck_Converter.kicad_sch`
- `LM2596_Buck_Converter.kicad_pcb`

<img width="1197" height="701" alt="image" src="https://github.com/user-attachments/assets/02dc4c7e-5bcc-4374-9780-0a58a9bd3168" />

<img width="1282" height="747" alt="image" src="https://github.com/user-attachments/assets/7daa2bef-5bb5-4800-9b3a-d890f6a2a7f0" />

<img width="1667" height="902" alt="image" src="https://github.com/user-attachments/assets/eb781ba0-9c36-457a-8ad2-4cf720311741" />

## Simulation

The design was verified in KiCad's built-in ngspice simulator using Texas Instruments' official transient SPICE model for the LM2596-5.0 (`LM2596_5P0_TRANS.LIB`, released by TI's Analog eLab Design Center), loaded via U1's Simulation Model dialog in place of a generic model.

**Setup:** 12 V input, 33 uH inductor, 220 uF output capacitor, 5 ohm (1 A) resistive load. Transient analysis, 50 ns time step, initial conditions enabled (`uic`) so the simulation starts from 0 V rather than an artificial DC operating point.

**Startup and settling — output ramps from 0 V through a stepped soft-start to ~5.0 V in about 1 ms:**

![Startup and settling](sim/screenshots/startup_and_settling.png)

**Zoomed output ripple (3.25-3.41 ms window):**

![Output ripple](sim/screenshots/output_ripple_zoom.png)

**Results:**

- Output regulates to **~5.0 V**, matching the datasheet's 4.8-5.2 V spec at this load.
- Soft-start ramp from 0 V to regulation in **~1 ms**, matching the LM2596's internal soft-start behavior.
- With an ideal (zero-ESR) output capacitor, the loop rings at roughly 15 kHz with ~80 mV peak-to-peak swing, as shown above. Adding a realistic ESR of 0.05-0.1 ohm in series with C2 (representative of a genuine low-ESR electrolytic) damps this to **~20 mV**, confirming the datasheet's note that very low output-capacitor ESR can destabilize the feedback loop.

**Model file:** [`sim/LM2596_5P0_TRANS.LIB`](sim/LM2596_5P0_TRANS.LIB)
See [`sim/SIMULATION_RESULTS.md`](sim/SIMULATION_RESULTS.md) for the full write-up, pin mapping, and settings.

> The model is TI's own release, provided "as is" with no warranty (see header comments in the file). It is not officially validated for ngspice, but ran without errors under ngspice's PSpice/LTspice compatibility mode.

## Manufacturing Checklist

1. Run ERC and DRC with zero errors.
2. Inspect the board in KiCad 3D Viewer.
3. Verify diode polarity, capacitor polarity, connector labels, and U1 orientation.
4. Verify every selected footprint matches the purchased component datasheet.
5. Generate Gerber and drill files from KiCad's Plot dialog.

## License

This project is provided for learning and personal use. Review the design independently before manufacturing or using it with valuable equipment.
