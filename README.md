# Eurorack Breakouts

Small breadboard-friendly PCBs. One board per reusable circuit. Milled at home
on the Makera Carvera Air.

Each board is the physical form of a circuit in
[eurorack-blocks](https://github.com/carr-james/eurorack-blocks). Drop a board
into a breadboard to prototype a module.

## Why these are separate from the circuits

The two forms want opposite things.

| | circuit | breakout |
|---|---|---|
| Exists as | schematic and layout fragment | a physical PCB |
| Wants | no connectors, small area | headers, outline, labels |

One artifact cannot serve both. They share the circuit definition.

A breakout is also the reference design and the test vehicle for its circuit.
The circuit works in hardware before a module depends on it.

## Layout

```
boards/<circuit-name>/     one KiCad project per breakout
templates/breakout/        start a new breakout from here
docs/                      conventions
```

## Conventions

Headers use 0.1in pitch on a 0.1in grid. The board then fits a breadboard. Put
signal pins on the long edges. Put pin 1 at the bottom left, seen from the top.

Power comes in on its own header. Use the same pin order on every board.
Eurorack uses +/-12V. Breadboard work often does not.

Put `<circuit-name> v<x.y.z>` in copper. Laser silkscreen prints small text
badly.

Add test points to inputs, outputs, and any node that shows how the circuit
behaves.

## Fabrication

Use the house rules in
`eurorack-blocks/design-rules/house-mill.kicad_dru`.

Choose parts in this order:

1. Use a part you have in stock. Check PartsBox.
2. If the value is not in stock, choose SMD.

SMD suits a milled board. An SMD pad solders from one face. An unplated
through-hole pad does not, and the top pad under a DIP body is out of reach.
Cut stencils on the same machine and reflow on a hotplate.

Boards are double sided. Route on both layers.

Nothing is plated at home, so each via is a rivet you set or a wire you solder
on both faces. Count vias, not layers. A tidy two-layer route with few vias
beats a congested one-layer route.

Double-sided milling needs alignment. Put four 2mm dowel holes in the corners,
3mm in from the edges. Keep the dowels in the board for every operation. Leave
this margin free of copper and parts.
