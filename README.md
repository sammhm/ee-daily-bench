# Daily Bench

A daily electrical-engineering practice app with a built-in circuit simulator, in one HTML page.

**Live app:** https://claude.ai/artifact/BS3DuEooWavmUj3wdNYkcQ
(On iPhone: open in Safari → Share → Add to Home Screen.)

## Today: learn it, don't memorize it
- 4 questions a day from a bank of 80: fundamentals, diodes, transistors, op-amps, AC/RC, power, ADCs/digital, sensors and measurement, plus "Read the schematic" questions where you answer by tapping a part or junction.
- Every day includes one schematic-reading question and works through questions you haven't seen yet before repeating.
- **Hint before guessing:** "Stuck? Show a hint" reveals the first reasoning step without giving the answer away.
- **Why not your answer:** each wrong choice has its own explanation of the misconception behind it.
- **Walk me through it:** a step-by-step explanation. Each step lights up the parts of the circuit it's talking about, shows node voltages, or advances a concept diagram.
- **Live circuit:** after you answer, the schematic becomes a running simulation you can tap, edit and restart.
- **Predict, then test:** experiments ask you to predict what a change will do, then apply it to the live circuit and explain the result.
- **Spaced review:** missed questions, and correct ones you mark as guessed, come back two days later.
- Concept diagrams: diode I-V curves, RC charging, RMS, Bode plot, aliasing, ADC steps, NTC vs RTD, switch bounce, MOSFET R_DS(on) vs V_GS, op-amp gain-bandwidth, buck duty cycle, rectifier ripple, 4–20 mA.
- Progress is stored in the browser (`localStorage`).

## Simulator
- Parts: wire, resistor, battery, AC source, current source, capacitor, inductor, diode, Schottky, Zener, LED, switch, op-amp, N-channel MOSFET, NPN BJT, ground.
- Two-terminal parts: drag between grid dots. Op-amps and transistors: tap a dot to place.
- Moving dots show conventional current (speed ∝ current). Wire color shows node voltage; part bodies shade from one end's voltage to the other.
- Tap a part for voltage, current, power and a live trace. Transistors also show their region (cutoff / active / saturation / triode); op-amps show linear vs. saturated.
- About 35 example circuits grouped by topic, including the ones used in the questions.

### How it solves
Modified nodal analysis on every time step. Wires and closed switches are 1 mΩ. Every node has a 1 pS leak to ground so floating nodes stay solvable. Capacitors and inductors use backward-Euler companion models. Diodes, Zeners and LEDs use a Shockley model solved with Newton iteration and SPICE-style junction limiting. The MOSFET is a square-law model (V_th 2 V, k 2.5 A/V², 1 nF gate capacitance). The BJT is Ebers–Moll with β = 100. The op-amp is an ideal amplifier with gain 10⁵ that clamps at its rails.

## Editing
`index.html` is the whole app.
- Questions live in `BANK`. Each can have `why` (one line per wrong choice), `steps` (walkthrough: `hl` highlights part indices, `v` shows node voltages, `sel` inspects a part, `p` sets the diagram stage) and `try` (predict-then-test experiments whose `set` ops change the circuit).
- Circuits live in `CIRCUITS`. Rows are `[type, x1, y1, x2, y2, value, label]`. Battery, AC and current sources go from − to +; diodes go from anode to cathode. Three-terminal parts are `["op", x, y, lo, hi]`, `["nmos", x, y]` and `["npn", x, y]`. Questions refer to parts by row index, so keep row order stable.
