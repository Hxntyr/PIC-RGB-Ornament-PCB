# PIC RGB Ornament PCB

A template for making — and a collection of — small RGB LED PCB ornaments.

The core circuit uses a PIC12F1572, CR2450R coin cell, and MCP1640 boost converter to drive 24 low-current RGB LEDs through three shared PWM channels. It is intended to be reused across different board shapes, artwork, and LED layouts without redesigning the electronics each time.

The basic workflow is: copy the core project, rearrange it into an ornament, generate the manufacturing files, and send it off for PCBA — or [purchase the components and assemble it yourself](https://www.digikey.com/en/mylists/list/D7LT6KEKSW).

<p align="center">
  <img src="PIC%20RGB%20Ornament%20Core/PIC%20RGB%20Ornament%20Core.png" alt="PIC RGB Ornament Core" width="40%">
</p>

## What's Included

The [`PIC RGB Ornament Core`](PIC%20RGB%20Ornament%20Core/) folder contains the reusable KiCad project.

Reference files:

* [`PIC RGB Ornament Core_Schematic.pdf`](PIC%20RGB%20Ornament%20Core/PIC%20RGB%20Ornament%20Core_Schematic.pdf) — schematic
* [`PIC RGB Ornament Core_PCB.pdf`](PIC%20RGB%20Ornament%20Core/PIC%20RGB%20Ornament%20Core_PCB.pdf) — component layout with a millimeter scale for quick size reference
* [`PIC RGB Ornament Core.png`](PIC%20RGB%20Ornament%20Core/PIC%20RGB%20Ornament%20Core.png) — 3D viewer reference

Custom footprints are stored in the repository-level [`HX.pretty`](HX.pretty/) library. Each included KiCad project references this library through its local `fp-lib-table`.

The core [`PCBA`](PIC%20RGB%20Ornament%20Core/PCBA/) folder contains files that can generally be reused between designs:

* `BOM.xlsx`
* `FIRMWARE.zip`

The supplied firmware continuously cycles through a slow rainbow at conservative brightness. The PIC is intended to be programmed during assembly, so the finished ornament requires no configuration.

## Making an Ornament

Clone or download the repository and make a copy of the `PIC RGB Ornament Core` project, or use one of the existing ornaments as a starting point.

The electrical design can generally remain unchanged. Modify the board outline, component placement, LED arrangement, artwork, mounting features, and routing as needed for the new design.

If additional custom footprints are required, add them to the root `HX.pretty` library. Projects located one directory below the repository root can use the same `fp-lib-table` entry:

```scheme
(fp_lib_table
  (version 7)
  (lib (name "HX")(type "KiCad")(uri "${KIPRJMOD}/../HX.pretty")(options "")(descr "Project custom footprints"))
)
```

## Preparing a Layout for PCBA

The BOM and firmware can normally be reused as long as the circuit and component selections remain unchanged.

The remaining manufacturing files are layout-specific and should be regenerated for each ornament.

### Gerbers and Drill Files

From KiCad PCB Editor:

`File → Fabrication Outputs → Gerbers`

Export the required copper, solder mask, silkscreen, paste, and `Edge.Cuts` layers, then generate the Excellon drill files.

Zip the Gerber and drill outputs together for fabrication.

### CPL / Pick-and-Place

From KiCad PCB Editor:

`File → Fabrication Outputs → Component Placement`

Export the placement file in millimeters with reference designator, X/Y coordinates, rotation, and board side.

PCBWay refers to this as the **CPL** or centroid file.

### Assembly Drawings

Plot `F.Fab` and `B.Fab` as PDFs with the board outline visible.

These provide a simple component-location and orientation reference for assembly.

### BOM

The baseline BOM is included at:

`PIC RGB Ornament Core/PCBA/BOM.xlsx`

Regenerate or edit it if component values, part numbers, or designators change.

### PIC Firmware

Production firmware is included at:

`PIC RGB Ornament Core/PCBA/FIRMWARE.zip`

For turnkey assembly, program:

`U2 — PIC12F1572T-I/MF`

using the supplied `.hex` file before assembly.

Example production note:

> Program U2 before assembly using the supplied HEX file. After assembly, power the board and verify that all 24 RGB LEDs smoothly cycle through the rainbow.

## Example

[`HappyBirthdayMickey_A`](HappyBirthdayMickey_A/) is an example ornament built from the core design.

Its `PCBA` folder contains a complete set of layout-specific production files:

* Gerber and drill ZIP
* BOM
* CPL / pick-and-place file
* assembly drawing PDFs
* firmware

These are included as a reference for what a completed manufacturing package looks like rather than as production files for the generic core.

## Notes

The default firmware intentionally runs the LEDs fairly dim to reduce coin-cell current and keep the ornament comfortable to view in a dark room.

The CR2450R battery should be installed **after** PCB assembly and should not go through reflow.

## License

This project is released under the **CC0 1.0 Universal Public Domain Dedication**.

Use it, modify it, manufacture it, remix it, or turn it into something completely different.

See [`LICENSE`](LICENSE).
