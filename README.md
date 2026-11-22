# Daily Bench

A daily electrical-engineering practice app plus an interactive circuit simulator, in one HTML page.

**Live app:** https://claude.ai/artifact/BS3DuEooWavmUj3wdNYkcQ
(On iPhone: open in Safari → Share → Add to Home Screen.)

## Today
- 4 new questions a day, drawn from a bank of 66 (fundamentals, diodes, transistors, op-amps, AC/RC, power, ADCs/digital, sensors and measurement).
- Multiple choice and numeric "work it out" problems, each with a worked explanation and a key idea.
- Circuit questions show the schematic and can be opened in the simulator.
- Streak, daily score, all-time accuracy, extra practice and retrying missed questions. Progress is stored in the browser (`localStorage`).

## Simulator
- Drag between grid dots to place wires, resistors, batteries, AC sources, capacitors, inductors, diodes, LEDs, switches and ground.
- Moving dots show conventional current (speed ∝ current). Wire color shows node voltage; part bodies shade from one end's voltage to the other.
- Tap a part for voltage across, current, power, end voltages and a live trace; tap a junction for its voltage to ground.
- Examples: voltage divider, series, parallel, LED + resistor, RC charging, Wheatstone bridge, half-wave rectifier.

### How it solves
Modified nodal analysis on every time step: wires and closed switches are 1 mΩ, every node has a 1 nΩ⁻¹ leak to ground so it can always be solved, capacitors and inductors use backward-Euler companion models, and diodes/LEDs use a Shockley model solved with Newton iteration (with SPICE-style junction voltage limiting).

## Editing
`index.html` is the whole app. Add questions to the `BANK` array and example circuits to `CIRCUITS`. Circuit rows are `[type, x1, y1, x2, y2, value]`; battery/AC go from the − terminal to the +, diodes/LEDs from anode to cathode.
