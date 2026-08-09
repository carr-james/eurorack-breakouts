# Eurorack Breakouts

Small, breadboard-friendly PCBs — one per reusable circuit — milled in-house on
the Makera Carvera Air.

Each breakout is the physical counterpart of a block in
[eurorack-blocks](https://github.com/carr-james/eurorack-blocks): same circuit,
wrapped with headers, an outline and labels so it can be dropped straight into a
breadboard while prototyping a new module.

## Why these exist separately from the blocks

A design block and a breakout board pull in opposite directions:

| | design block | breakout |
|---|---|---|
| exists as | schematic + layout fragment, absorbed into a host board | a physical PCB |
| wants | no connectors, minimal area, edge-agnostic | 0.1" headers, defined outline, labels, test points |

One artifact cannot serve both well. What they share is the **circuit** — the
schematic and part choices. The breakout is a thin wrapper around the block.

The useful by-product: **a breakout is the reference design and test vehicle for
its block.** Before a circuit is standardised on, there is a physical board that
proves it works.

## Layout

```
boards/<block-name>/       one KiCad project per breakout, named after its block
templates/breakout/        starting point for a new breakout
docs/                      the conventions below, in detail
```

## Conventions

**Headers.** 0.1" pitch, on a 0.1" grid, so the board seats in a standard
breadboard. Signal pins on the long edges; keep pin 1 bottom-left when viewed
from the top.

**Power.** Eurorack runs on ±12V, breadboard work usually does not. Every
breakout brings power in on a dedicated header, labelled, with the same pin
order across the whole set. Decide it once, never think about it again.

**Version in copper.** Each board carries `<block-name> v<x.y.z>` milled into
copper, matching the block version it was built from. Not silkscreen — laser
silkscreen on the Carvera renders text poorly at this size.

**Test points** on anything you would otherwise be probing blind: inputs,
outputs, and any internal node the circuit's behaviour hinges on.

## Fabrication

Milled in-house, so the house rules in
`eurorack-blocks/design-rules/house-mill.kicad_dru` apply — 0.2mm track and
clearance, 0.9mm vias, nothing plated.

**Surface-mount by default.** Counterintuitive for hand assembly, but with no
plated through-holes an SMD pad solders from one face and a through-hole pad
does not — and you cannot reach the top-side pad under a DIP body. SMD also
suits stencils cut on the same machine and a hotplate or reflow oven.

**Vias are hand labour.** Every one is a rivet you set or a wire you solder both
sides of. Prefer single-layer routing with a back-side pour; treat each stitch
as a deliberate cost.
