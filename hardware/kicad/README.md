# LuminaBlossom KiCad carrier (Rev A draft)

This is a **new carrier / interconnect PCB** for the existing LuminaBlossom architecture. It is not a custom NeoPixel ring board and is not claimed to be fabricated or tested.

## Files

- `luminablossom_carrier.kicad_pro` — KiCad project settings.
- `luminablossom_carrier.kicad_sch` — editable schematic with cached symbols.
- `luminablossom_carrier.kicad_pcb` — editable two-layer board layout with nets and routed connections.
- `board_preview.svg` — illustrative preview generated from the draft board source, not a KiCad screenshot.
- `schematic_preview.svg` — quick wiring overview; the native schematic is the source of truth.

## Board contents

- J1/J2: two 1×20 female socket strips for the Pico 2 W, with 17.78 mm row spacing.
- U1: SN74AHCT125N through-hole DIP-14 buffer.
- R1: 330 Ω series resistor between the buffer output and LED DIN.
- C1: 100 nF bypass capacitor at U1.
- C2: 470 µF / 10 V radial bulk capacitor near the LED output. Confirm polarity.
- J3: 1×3 output header, pad 1 = +5 V, pad 2 = GND, pad 3 = buffered LED DIN.

## Electrical notes

- GP16 is physical Pico pin 21 and provides 3.3 V logic. U1 is powered from +5 V to translate the signal to a 5 V data level.
- Pico physical pin 40 (VBUS) supplies the +5 V rail in this draft; all grounds must be common.
- U1 uses gate 1 for the data path. Unused inputs are held low; unused active-low output enables are held high.
- A 330 Ω series resistor and 470 µF bulk capacitor are included as practical interface components. Confirm actual ring requirements and USB supply capacity.

## Before manufacturing

**Do not order this Rev A draft without review.** Open the project in KiCad 9 and:

1. Check the Pico socket orientation and spacing against the exact module; check USB connector clearance and actual enclosure fit.
2. Confirm footprints match the exact socket strips, DIP-14 IC, resistor, capacitors, and 1×3 header.
3. Run schematic ERC and PCB DRC. Resolve errors and inspect silkscreen/courtyard overlaps.
4. Confirm the SN74AHCT125N pinout, J3 pin order, capacitor polarity and supply path against datasheets.
5. Only after validation, export Gerber and drill files. No Gerber/Excellon outputs are included yet.

## Validation status

KiCad CLI was not available in the authoring environment. The files have been checked for balanced source delimiters and obvious different-net route intersections, but a KiCad load, ERC, DRC, fabrication and physical test are **not** claimed. The project’s original enclosure is a 2D laser-cut design; no Fusion 360, STEP or STL model is included.
