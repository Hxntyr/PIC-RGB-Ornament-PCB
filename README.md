# PIC RGB Ornament PCB

A reusable RGB ornament PCB design built around a small PIC microcontroller, a coin cell, and a bunch of low-current RGB LEDs.

The idea is to keep one base circuit around and reuse it for different ornament shapes, artwork, LED arrangements, and future designs without having to reinvent the electronics every time.

## What It Uses

The current design is based around:

* 24 low-current common-anode RGB LEDs
* Microchip PIC12F1572
* Microchip MCP1640 boost converter
* One CR2450R coin cell
* C&K edge-mounted slide switch
* Fixed low-current LED drive
* Three PWM channels for red, green, and blue
* Resistor networks to cut down on part count and routing clutter
* Mostly low-profile SMD parts selected with turnkey PCBA in mind

The LEDs all share three color buses, while each individual LED die still gets its own current-limiting resistor.

The PIC directly sinks the RGB channels since the whole design is intentionally kept pretty dim and low-current.

## Power

The CR2450R feeds an MCP1640 boost converter that generates about 3.58 V.

That gives the green and blue LED dies a little more voltage headroom as the battery runs down and keeps the colors more consistent than running everything directly from the coin cell.

There is also a small resettable fuse on the battery input for basic fault protection.

## Firmware

The PIC handles the RGB animation using its three hardware PWM channels.

The default idea is a slow rainbow cycle with conservative PWM duty so the ornament stays dim, pleasant, and reasonably battery-friendly.

The PIC is intended to be programmed by the assembly house before it is installed. ICSP pads can still be included on the PCB for development or recovery, but the person receiving the ornament should never need to flash or configure anything.

Insert battery, flip switch, lights happen.

## Manufacturing

The design is being made with turnkey PCBA in mind, especially PCBWay.

KiCad symbols include manufacturer and part-number information where it matters so the BOM can be generated with minimal cleanup.

A few parts use manufacturer-specific footprints instead of generic ones, especially:

* RGB LEDs
* resistor networks
* edge-mounted switch
* CR2450 holder

Those should always be checked against the current manufacturer drawings before ordering boards.

## Notes

This is still a hobby hardware project, so battery life, LED brightness, firmware behavior, footprints, and assembly details should all be checked on prototypes before making a large batch.

Coin cells are also a swallowing hazard, so any finished ornament should keep the battery reasonably secure and inaccessible to small children.

## License

This project is released under the **CC0 1.0 Universal Public Domain Dedication**.

Use it, modify it, manufacture it, remix it, or turn it into something completely different.

Attribution is not required.

See [`LICENSE`](LICENSE)
