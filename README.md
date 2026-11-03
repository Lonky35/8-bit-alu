# 8-bit-alu
# 8-Bit ALU (No Microprocessor)

An 8-bit adder/subtractor built entirely from discrete logic chips, with no microcontroller, no firmware and no programmable logic. Set two 8-bit numbers on DIP switches, flip the add/subtract switch, and the result appears on LEDs and a decimal display. A hardware multiplier is the planned next stage.

![Full 3D assembly](images/assembly.png)

## What it does and how to use it

| Control / output | What it does |
|---|---|
| Input bank A (8 switches) | First operand, binary |
| Input bank B (8 switches) | Second operand, binary |
| Add / Subtract switch | Selects `A + B` or `A − B` |
| 8 red LEDs | Result in binary |
| 9th red LED | Carry out, which is the "256" bit in add mode |
| Blue LED | Lights when a subtraction result is negative |
| 7-segment display | Result in decimal `[describe once working]` |

**To use it:**
1. Power the board with `[voltage, e.g. 5 V]`.
2. Set operand A and operand B on the two switch banks (up = 1).
3. Pick add or subtract.
4. Read the result on the LEDs and the display.

**Example:** `A = 00001111 (15)`, `B = 00000001 (1)`, Add → `00010000 (16)`.

## Why I made it

`[Write 2–3 honest, personal sentences. What made you want to build this? Possible angles: you wanted to understand how a CPU's arithmetic actually works at the gate level, and building it without a microprocessor means you can't hide behind code.]`

Every bit of the result is made by physical gates you can probe with a multimeter. It's also designed as a teaching tool: anyone looking at the board can see carry propagation happen.

## How it works

- **Addition:** two cascaded **74HC283** 4-bit full adders form an 8-bit ripple-carry adder. The right chip handles the low 4 bits and passes its carry into the left chip, which handles the high 4.
- **Subtraction:** two **74HC86** XOR chips conditionally invert operand B, and the add/subtract switch feeds the carry-in. This gives two's-complement subtraction using the same adder.
- **Overflow/negative flags:** a **74HC04** and **74HC08** drive the 256 carry LED (add mode) and the blue negative LED (subtract mode).
- **Decimal output:** a magnitude block feeds a binary-to-BCD converter built from add-3 modules, then **CD4511** decoders drive the 7-segment digits.

![Schematic](images/schematic.png)

## Project status

| Stage | Status |
|---|---|
| 8-bit adder | ✅ Working (Tinkercad) |
| Subtractor + carry/negative LEDs | ✅ Working (Tinkercad) |
| Decimal output: magnitude block | ✅ Working (Tinkercad) |
| Decimal output: binary→BCD and display | 🔧 `[in progress / working]` |
| 8-bit multiplier | 🔜 `[planned / in progress]` |
| Custom PCB | 🔜 `[Design Submission: layout in progress]` |
| Casing (Onshape) | 🔜 `[to be designed once the circuit is final]` |

## Screenshots

| Full 3D assembly | PCB |
|---|---|
| ![Assembly](images/assembly.png) | ![PCB](images/pcb.png) |

| Schematic / wiring diagram | 3D render (optional) |
|---|---|
| ![Schematic](images/schematic.png) | ![Render](images/render.png) |

## Repository layout

```
8-bit-alu/
├── README.md
├── bom.csv              # parts list with links and requested funding
├── cad/                 # Onshape link + .step files for the casing
├── pcb/                 # .kicad_pro, .kicad_sch, .kicad_pcb, .kicad_prl, gerbers.zip
├── tinkercad/           # exported circuit files / links
└── images/
```

**Firmware:** none, by design. The project has no microprocessor, so there is no code to upload.

## Bill of materials

See [`bom.csv`](bom.csv). Every line has a supplier link, and I've marked parts I already own. Total requested: **`[amount]`**.

Main parts: 2× 74HC283, 2× 74HC86, 1× 74HC04, 1× 74HC08, CD4511 decoders, 7-segment displays, 2× 8-position DIP switches, 1 add/subtract switch, LEDs and resistors, `[PCB fabrication, casing materials]`.

## Why it's worth funding

`[Fill in what the money actually lets you do, for example: a real PCB instead of a breadboard, so it's a durable one-off you can demo; parts for the multiplier stage; casing materials.]`

## Credits and license

Built by [Lonky35](https://github.com/Lonky35) as part of Hack Club's **Fallen** program. Licensed under `[MIT / CERN-OHL / etc.]`.
