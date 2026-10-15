# Coherent DWDM / 400ZR Reach Planner

Plan a coherent DWDM route span by span and get a straight answer: will plain
400ZR work, do you need OpenZR+, or does the route fail — and which limit
(OSNR, chromatic dispersion, PMD, or receive power) bites first?

**Live version:**
[allaboutitinfrastructure.com/tools/dwdm-reach-planner/](https://allaboutitinfrastructure.com/tools/dwdm-reach-planner/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## What it does

- **Per-span OSNR cascade** — each amplifier's ASE noise contribution is
  combined in linear units (never by adding dB), with the OSNR shown after
  every span.
- **Margin waterfall** — transmitter OSNR → ASE cascade → ROADM filtering
  penalty → simplified nonlinear (GN-style) penalty → final margin against
  the selected module's required OSNR and your design-margin target.
- **CD / PMD budgets** — total chromatic dispersion and mean differential
  group delay checked against the selected module's tolerances, each with
  its own pass/fail (a route can pass OSNR and still fail on CD alone).
- **ZR vs ZR+ advisor** — presets for 400ZR amplified / unamplified (OIF
  400ZR Implementation Agreement values) and a representative OpenZR+
  module's 400 / 300 / 200 modes. The verdict names the first failing limit
  and, when a step up fixes it, says which mode to step up to.

## Honesty note

This is a simplified GN-model-style estimate for planning and learning.
Amplifier gain is assumed to equal span loss; the nonlinear penalty is a
deliberately simple model, not a full GNPy simulation. Real designs use
vendor tools (OptSim / TransportPlanner class) and measured fiber data.
