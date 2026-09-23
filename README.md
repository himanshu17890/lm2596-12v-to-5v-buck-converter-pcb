# LM2596 12 V to 5 V Buck Converter PCB

A two-layer PCB for converting a 12 V DC input into a regulated 5 V DC output using an LM2596S-5 switching regulator.

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

## Manufacturing Checklist

1. Run ERC and DRC with zero errors.
2. Inspect the board in KiCad 3D Viewer.
3. Verify diode polarity, capacitor polarity, connector labels, and U1 orientation.
4. Verify every selected footprint matches the purchased component datasheet.
5. Generate Gerber and drill files from KiCad's Plot dialog.

## License

This project is provided for learning and personal use. Review the design independently before manufacturing or using it with valuable equipment.
