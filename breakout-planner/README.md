# 400G/800G Port Breakout Planner

Pick a port speed (800G or 400G), a breakout mode and a switch size — get the
lane map, a plain valid/invalid verdict with the reason, cable and connector
guidance per reach, and full-switch port counts.

**Live version:**
[allaboutitinfrastructure.com/tools/breakout-planner/](https://allaboutitinfrastructure.com/tools/breakout-planner/)

**Run it:** open `index.html` in any browser. Single file, no dependencies,
works offline. Everything is computed locally — nothing leaves the page.

## How to use

1. Choose the native port speed: 800G (8 lanes × 100G PAM4) or 400G
   (8 lanes × 50G PAM4).
2. Pick how many legs you want and the speed of each leg. Invalid
   combinations are allowed on purpose — the planner explains exactly why
   they fail (lane remainder, stranded lanes, or a non-standard mode).
3. Read the lane map (which lanes form which leg), the cable/connector
   guidance for your reach (DAC/AEC, SR or DR), and the full-switch totals:
   a 64-port 800G switch broken out 8×100G gives 512 × 100G ports.

## Honesty notes

- This is a **generic lane model**. Aggregate bandwidth alone does not make
  a supported breakout mode — your switch ASIC, optic, cable and the far
  end must all support the mode. Check your platform's breakout guide
  before ordering cables.
- Cable and connector guidance is typical for each reach class; verify
  against your optic's datasheet.
